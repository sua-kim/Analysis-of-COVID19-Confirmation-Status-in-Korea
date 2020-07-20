# Analysis-of-COVID19-Confirmation-Status-in-Korea 
(대한민국 COVID-19 확진 현황 분석 프로그램)


Editor: 이화여자대학교 휴먼기계바이오공학부 1870021 김수아

이 프로그램은 대한민국 COVID-19 확진 현황에 대한 분석 결과를 그래프로 시각화 하는 기능을 제공합니다.  



# Data

## CSV file

- 대한민국 누적 확진 현황 데이터
- 광역시/도별 누적 확진 현황 데이터
- 이 때, region열의 한글 깨짐 현상을 해결하기 위해 메모장을 활용하여 인코딩을 UTF-8에서 ANSI 형식으로 변환하였다.

- 코로나 19(COVID-19) 실시간 상황판 사이트 (https://coronaboard.kr/)

## Wikipedia data

- 광역시/도별 소재별 확진 현황 데이터

- Wikipedia (https://en.wikipedia.org/wiki/COVID-19_pandemic_in_South_Korea)




# TOOL (MODULE USED)

## csv
: csv.reader

## pandas
: pandas.read_html, dataframe.iloc, dataframe.loc dataframe.index, dataframe.index, del dataframe['column_name']

## numpy
: numpy.array, numpy.sum

## matplotlib.pyplot (plt)
: plt.rc, plt.xlabel, plt.ylabel, plt.plot, plt.pie, plt.axis, plt.title, plt.legend, plt.show



# PROGRAM STRUCTURE

## number_info_load function
: csv 파일로부터 누적 확진 정보 데이터를 받아오는 함수

## cluster_info_load function
: Wikipedia로부터 지역별, 소재별 코로나 확진 정보 데이터를 저장하는 함수

## number_visualization function
: 꺾은선 그래프를 통해 누적 확진자 수 데이터를 그래프로 시각화하는 함수

## cluster_visualization function
: 파이차트를 통해 소재별 확진 현황 데이터를 그래프로 시각화하는 함수

## main function
: 사용자로부터 입력을 받아 사용자가 원하는 데이터를 출력할 수 있도록 구성


# HOW TO USE
1. 분석하고자 하는 지역 범위를 선택합니다. 
: 1 - 대한민국 COVID-19 추이
  2 - 광역시도별 COVID-19 추이

2-1. '1. 대한민국 COVID-19 추이'를 선택했다면
: 누적 확진자 추이 변화/소재별 확진현황 중 알고 싶은 정보를 선택하여 결과 출력

2-2. '2. 광역시도별 COVID-19 추이'를 선택했다면
: 알고싶은 지역명을 입력하고 해당 지역에 대한 누적 확진자 추이 변화/소재별 확진현황 중 알고싶은 정보를 선택하여 결과 출력


# **유의 사항:**

> - 2-1의 대한민국 누적 확진자 추이 변화는 데이터가 1월 21일부터 존재하는 반면, 2-2의 지역별 누적 확진자 추이 변화는 데이터가 2월 17일부터 존재하므로 두 그래프를 출력하여 비교했을 때, x축 좌표(누적일자) 차이가 존재할 수 있다.
> 
> - 2-2에서 지역명을 입력할 때는 간단한 광역 시도명을 입력해야한다.
     ( 예: 서울특별시 -> 서울 / 경상남도 -> 경남)
