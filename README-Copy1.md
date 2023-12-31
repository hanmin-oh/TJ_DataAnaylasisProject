# 서울 집값 예측 프로젝트
## 기획단계 
- 2022년 서울의 아파트 실거래가를 분석하여 집값을 예측하고자 하였습니다.
- 하지만 서울은 기본적으로 지역에 따른 집값의 차이가 크고 같은 지역 내에서도 고급 아파트의 실거래가의 차이도 크기 때문에 일률적으로 적용해서 집값을 예측하는 것은 정확도가 많이 낮다고 생각하였습니다.
- 그래서 동북부의 강북구, 도봉구, 노원구와 중랑구, 동대문구, 성북구를 묶어서 비교하려고 하습니다. 한강과 떨어져 있고 중심 업무지구(강남, 광화문, 여의도) 등과 떨어져 있기 때문에 적당하다고 생각하였다. 
- 1차는 기본적으로 면적(㎢)당 학원 수, 고등학교의 수, 지하철 역의 개수 등을 피쳐로 삼아 집값(면적(㎡)당 가격)을 타겟으로 기본적인 지도학습을 수행할 예정이다.

## 1) 데이터 출처
- 우선 집값의 경우 국토교통부 실거래가 공개시스템을 사용했습니다. <br/> http://rtdown.molit.go.kr/
- 지하철의 경우 서울 교통 빅데이터 포탈을 사용했습니다. <br/> https://t-data.seoul.go.kr/category/dataviewfile.do?data_id=10054
- 학원의 경우 공공데이터 포탈의 '소상공인시장진흥공단_상가(상권)정보'를 이용했습니다. https://www.data.go.kr/data/15083033/fileData.do
- 학교 수의 경우 학교알리미의 공개용데이터를 이용했습니다.  <br/> https://www.schoolinfo.go.kr/ng/go/pnnggo_a01_l2.do

## 2) 데이터 전처리
- 집값을 타겟으로 하고 면적(㎢)당 학원 수, 고등학교의 수, 지하철 역의 개수 등을 피쳐로 삼기 위해 서울 열린데이터 광장에서 행정구역 면적을 다운받았습니다. https://data.seoul.go.kr/dataList/412/S/2/datasetView.do
- 각각의 데이터를 판다스 데이터프레임으로 받아서 동별로 그룹화하여 면적으로 나누었습니다.
- 필요에 따라 네이버 API를 이용하여 지오코딩하였습니다.

## 3) 학습
- 우선 선형회귀 학습으로 각각의 피쳐에 대하여 집값을 예측하였습니다.

## 4) 상관관계
- 집값과 역 수, 고등학교의 수, 학원 수와 상관관계를 구하였을 때
|------|---|---|
|역 수|0.077|테스트3|
|고등학교의 수|0.122|테스트3|
|학원 수|테스트2|테스트3|
- 지하철 역 : 
