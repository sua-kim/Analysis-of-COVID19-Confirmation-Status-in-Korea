'''
1870021 휴먼기계바이오공학부 김수아
Analysis-of-COVID19-Confirmation-Status-in-Korea (우리나라 COVID-19 확진 현황 분석 프로그램)
'''


# 모듈 import
import csv
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt


# csv 파일로부터 누적 확진 정보 데이터를 저장하는 함수(매개변수: region)
def number_info_load(region):
    # 확진자수(confirm), 사망자수(death), 격리해제(released) 정보를 저장할 리스트 초기화
    confirm = []
    death = []
    released = []

    if region == '대한민국':
        f = open('kr_daily.csv')  # 파일 열기
        data = csv.reader(f)  # csv.reader 객체 생성
        next(data)  # 필요한 숫자 정보를 읽어오기 위해 next 함수 사용
        # 시계열 정보를 각 리스트에 추가(append 함수 활용)
        for row in data:
            confirm.append(int(row[1]))
            death.append(int(row[2]))
            released.append(int(row[3]))
    else:
        f = open('kr_regional_daily.csv')  # 파일 열기
        data = csv.reader(f)  # csv.reader 객체 생성
        next(data)  # 필요한 숫자 정보를 읽어오기 위해 next 함수 사용
        for row in data:
            # 입력한 지역명에 해당하는 시계열 정보를 각 리스트에 추가(append 함수 활용)
            if region in row[1]:
                confirm.append(int(row[2]))
                death.append(int(row[3]))
                released.append(int(row[-1]))

    # 확진자수, 사망자수, 격리해제 정보 반환
    return confirm, death, released


# 위키피디아로부터 지역별, 소재별 코로나 확진 정보 데이터를 저장하는 함수(매개변수: region)
def cluster_info_load(region):
    # wikipedia의 각 지역에 대한 소재별 코로나 확진 정보 url 데이터를 pandas 라이브러리로 불러온다.
    df = pd.read_html('https://en.wikipedia.org/wiki/COVID-19_pandemic_in_South_Korea', header=0, index_col=0)[6]

    # iloc 함수를 통해 'df'에서 필요한 데이터(지역별)만 추출하여 case에 데이터 프레임으로 저장
    case = df.iloc[2:20, 1:8]
    # columns과 index 이름 설정
    case.columns = ['해외유입', '소계', '신천지', '소모임', '확진자접촉', '기존해외유입', '그외']
    case.index = ['대구', '경북', '서울', '경기', '공항', '인천', '충남', '부산', '경남', '충북',
                  '강원', '울산', '세종', '대전', '광주', '전북', '전남', '제주']
    # 소계 열 삭제
    del case['소계']

    # 이 때, DataFrame 'case' 내 모든 값의 데이터 타입이 문자이므로 numpy 배열로 변환
    if region == '대한민국':
        # case를 numpy 배열로 저장하여 정수형으로 변환
        country_case = np.array(case, dtype=int)
        # sum 함수를 통해 열방향으로 모든 값을 더한 결과를 final_case numpy 배열에 저장
        final_case = np.sum(country_case, axis=0)
    else:
        # case의 행 인덱스가 입력한 지역인 데이터를 numpy 배열로 저장하여 정수형으로 변환
        final_case = np.array(case.loc[region], dtype=int)

    # 소재별 확진 정보 반환
    return final_case


# 꺾은선 그래프를 통해 누적 확진자 수 데이터를 그래프로 시각화하는 함수
# 매개변수: 누적 확진자수, 누적 사망자수, 누적 격리해제 수, 지역명
def number_visualization(c_data, d_data, r_data, extent):
    plt.rc('font', family='Malgun Gothic')  # 그래프에 한글 표시
    plt.xlabel("경과일")  # x, y축 레이블 설정
    plt.ylabel("사람 수")
    # 확진자수, 사망자수, 격리해제수에 대한 꺾은선 그래프
    plt.plot(c_data, label='누적확진자수')
    plt.plot(d_data, label='누적사망자수')
    plt.plot(r_data, label='누적격리해제')
    # 전국적인 데이터를 확인하고 싶은 경우
    if extent == '대한민국':
        plt.title(extent + '의 누적 확진자 추이 변화(6월 15일 기준)')  # 제목 지정
    # 지역별 데이터를 확인하고 싶은 경우
    else:
        plt.title(extent + '지역의 누적 확진자 추이변화(6월 15일 기준)')  # 제목 지정
    plt.legend()  # 범례 표시
    plt.show()


# 파이차트를 통해 소재별 확진 현황을 그래프로 시각화하는 함수
# 매개변수: 소재별 확진 현황 데이터, 지역명
def cluster_visualization(case_data, extent):
    plt.rc('font', family='Malgun Gothic')  # 그래프에 한글 표시
    size = case_data  # 데이터
    label = ['해외유입', '신천지', '소모임', '확진자접촉', '기존해외유입', '그외']  # 레이블 설정
    color = ['palevioletred', 'royalblue', 'mediumseagreen', 'darkviolet',
             'darkturquoise', 'tan']
    plt.axis('equal')  # 파이차트를 동그란 원으로 표현
    # 비율 및 범례를 표시, 소수점 자리와 색상 지정
    plt.pie(size, labels=label, autopct='%.1f%%', colors=color)
    if extent == '대한민국':
        plt.title(extent + '의 소재별 확진 현황(6월 15일 기준)')  # 제목 지정
    else:
        plt.title(extent + '지역의 소재별 확진 현황(6월 15일 기준)')  # 제목 지정
    plt.legend()  # 범례 표시
    plt.show()


'''
메인 함수(main function)
  :  사용자로부터 입력을 받아 조건문을 통해 사용자가 원하는 정보를 출력할 수 있도록 구성
'''
# 프로그램 안내 메세지 출력을 통한 user-friendly한 프로그램 설계
print("----------------------------------------------------------------------------------")
print("                                COVID 19 통계 프로그램                               ")
print("             코로나 19 누적 확진자 추이 변화 및 소재별 확진 비율 정보를 확인할 수 있습니다.       ")
print("----------------------------------------------------------------------------------\n")
# 보고싶은 지역 범위(대한민국/광역시도별) 입력 받기
print("1. 대한민국 COVID-19 추이     2. 지역별 COVID-19 추이 ")  # 메인메뉴 출력
menu = int(input("궁금한 정보의 번호를 입력해주세요: "))

if menu == 1:
    country = '대한민국'  # 함수의 매개변수로 활용하기 위한 지역범위 변수
    print("\n----------------------------------------------------------------------------------")
    print("                      '1. 대한민국 COVID-19 추이'를 선택하셨습니다!                        ")
    print("----------------------------------------------------------------------------------")
    print("1. 누적 확진자 추이 변화   2. 소재별 확진 현황")  # 서브 메뉴 출력
    sub_menu = int(input(("어떤 정보를 검색하시겠습니까? 번호를 선택해주세요: ")))
    # 누적 확진자 추이 변화
    if sub_menu == 1:
        confirm_info, death_info, released_info = number_info_load(country)
        number_visualization(confirm_info, death_info, released_info, country)
    # 소재별 확진 현황
    elif sub_menu == 2:
        cluster_info = cluster_info_load(country)
        cluster_visualization(cluster_info, country)
    else:
        print("번호 입력 오류! 잘못 선택하셨습니다.")  # 오류 메세지 출력

elif menu == 2:
    print("\n----------------------------------------------------------------------------------")
    print("                     '2. 지역별 COVID-19 추이'를 선택하셨습니다!                         ")
    print("----------------------------------------------------------------------------------")
    # user-friendly한 구성을 위한 입력 예시 안내
    print("지역명을 입력하면 해당 지역의 누적 확진자 추이 변화 및 소재별 확진 비율 정보를 확인할 수 있습니다.")
    print("====> 지역명은 18개의 광역시/도명로 입력해주세요  (예: 서울, 대구, 경남 등)")
    city_name = input("찾고 싶은 지역명을 입력해주세요: ")  # 지역명 입력 받기
    print("\n1. 누적 확진자 추이 변화   2. 소재별 확진 현황")    # 서브 메뉴 출력
    sub_menu = int(input(("해당 지역의 어떤 정보를 검색하시겠습니까? 번호를 선택해주세요: ")))
    # 누적 확진자 추이 변화
    if sub_menu == 1:
        confirm_info, death_info, released_info = number_info_load(city_name)
        number_visualization(confirm_info, death_info, released_info, city_name)
    # 소재별 확진 현황
    elif sub_menu == 2:
        cluster_info = cluster_info_load(city_name)
        cluster_visualization(cluster_info, city_name)
    else:
        print("번호 입력 오류! 잘못 선택하셨습니다.")  # 오류 메세지 출력

else:
    print("번호 입력 오류! 잘못 선택하셨습니다.")  # 오류 메세지 출력
