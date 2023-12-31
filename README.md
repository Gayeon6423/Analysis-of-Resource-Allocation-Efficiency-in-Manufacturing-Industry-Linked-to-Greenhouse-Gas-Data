---

# 1. 배경 & 목적

---

**[분석 주제명]**

- 온실가스 데이터와 연계한 지역 간 제조업 자원 배분 효율성 분석

**[분석 배경]** 

- 최근 기후변화와 관련된 문제로서 에너지 자원배분과 에너지 불평등이 강조되고 있는데, 이는 지역별 자원배분이 경제와 사회적 발전에 미치는 영향을 고려해야 함을 시사합니다.
- 특히 한국의 경제성장은 총요소생산성(TFP) 변화와 밀접한 관련이 있으며, 경제 격차도 지역 간에 크게 벌어지고 있다. 이에 본 연구는 에너지 자원 배분과 함께 지역 간 총요소생산성 차이를 분석하고자 합니다.

**[분석 목적]** 

- 경제 이론을 기반으로 실제로 한국의 지역간 제조업의 자원배분이 효율적으로 이루어지고 있는지 확인하고, 온실가스 배출량 추이를 분석하여 이를 비교하고자 합니다. 이를 통해 기후금융 분야에서의 정책 시사점을 도출하고자 하는 것을 연구 목적으로 두고 있습니다.

**[방법론 요약]**

- 콥-더글라스 생산함수 기반의 한계생산물과 솔로우 잔차 모형을 활용하여 지역별 에너지 자원배분의 효율성을 측정합니다.
- 자본, 노동, 에너지 세 가지 생산요소과 총요소생산성과의 관계를 고려하여 분석하며, 회귀 분석을 통해 자원배분의 영향을 파악하고 해석합니다. 또한, 온실가스 배출량 추이를 조사하여 분석 결과와 비교합니다.

# 2. 주최 & 참가 대상 & 성과

---

- 주최: 한국자원경제학회
- 참가 자격 및 팀 인원 제한 사항: 2023년 9월 현재 국내 대학 및 대학원에 재학 중인 자
- 성과:

# 3. 프로젝트 기간(대회 기간)

---

- 공모 기간 : 2023년 9월 5일 ~ 11월 5일
- 결과 발표 : 2023년 12월 초, 개별통보
- 시상식 : 2023년 12월 15일(금) 예정

# 4. 담당 역할

---

| 성명 | 역할 |
| --- | --- |
| 정가연 | 팀장, 선행 논문 조사, 서론 작성, 회귀분석 이론적 배경 작성, 회귀분석 모델링, 가설 검정 및 결과 작성 |
| 최효빈 | 선행 논문 조사, 콥-더글라스 생산함수 이론적 배경 작성, 회귀분석 결과 해석 |
| 최서연 | 선행 논문 조사, 솔로우 잔차모형 이론적 배경 작성, 회귀분석 결과 해석 |
| 전가은 | 선행 논문 조사, 온실가스 이론적 배경 작성, 온실가스 데이터 해석 |
| 조예원 | 선행 논문 조사, 서론 작성, 온실가스 데이터 해석 |
- 팀장으로써 논문의 전체적인 구조를 짠 후 팀원 분들에게 각자 파트를 분배해주었습니다. 팀원 분들이 자료를 조사해오면 검토한 후 논문에 옮겨 적는 작업을 진행했습니다. 회의 시작 전 진행 사항에 대해서 정리하여 발표하였고 팀이 원할하게 돌아가도록 노력하였습니다.
- 회귀분석 관련 내용을 조사한 후 수업을 진행함으로써 팀원분들의 이해를 도왔습니다.
- 경제 이론을 기반으로 제조업 데이터에서 피쳐를 조합하여 경제 변수를 생성하였습니다. 이를 기반으로 콥-더글라스 생산함수의 생산요소와 총요소생산성을 계산하였습니다. 그 후 실질 변수 변환, 산업 가중 평균 계산, 로그 변환 등의 전처리 작업을 진행해주었습니다.
- 파이썬을 이용해서 회귀분석 모델링과 데이터 그래핑 작업을 진행했습니다. 생산함수를 로그변환 시켜서 선형화 시킨 후 다중회귀 분석을 진행하였고 가설 검정 및 유의성 검정 등 해석 결과를 작성하였습니다.

# 5. 분석 과정

---

## ch1. 데이터 수집 및 변수

- 1999년~2019년까지의 ‘광역제조업조사통계’ 데이터
    - 7개의 시도와 산업으로 분류되어 있으며 부가가치액, 연초잔액, 연말잔액, 제조원가, 판관비 등으로 구성
    - 당해년도에 국내에서 사업을 영위하는 제조업 사업체를 대상으로 조사된
    시계열과 횡단면이 함께 고려된 불균형 패널 형태의 자료

- 1990년~2019년까지의 ‘광역지자체 간 온실가스 인벤토리’ 데이터
    - 17개 행정구역의 연도별 온실가스 배출량, 가스별 배출량, 간접 배출량으로 구성된 패널 형태의 데이터

## Ch2. 데이터 전처리

- 결측치 처리 : dropna 메서드 사용
- 변수 계산
    - ‘Labor’ column : pay1(연간급여액 합계) + pay3(복리후생비)
    - ‘Kapital’ column : (fasset_b(연초잔액) + fasset_e(연말잔액)) / 2
    - ‘Energy’ column : cost_fuel(연료비) + cost_elec(전력비)
    - ‘productivity’ column : vadd(부가가치액)
- 실질 변수 변환 : 2015년 제조업 생산자물가지수(119.84)로 명목변수 값을 나눠줬습니다.
- 산업별 평균 변수 계산 : Proxi Variable 가정(산업이 유사하면 물가가 비슷)을 전제로 각 변수를 산업코드로 그룹화한 후 부가가치를 가중치로 사용하여 산업별로 가중평균 값을 도출했습니다. 그 후 기업의 총요소생산성을 산업별 가중평균 값으로 나눠주었습니다.
- 로그 변환 : 마이너스 무한대 방지를 위해 실질변수에 0.01을 더한 후 변환을 진행해주었습니다.

## Ch3. 회귀분석을 위한 가설 및 모델 설정

### **[분석 모형 및 가설 설정]**

- 콥-더글라스 생산함수를 로그변환 시킨 후 선형 함수 형태로 변환해주었습니다. 선형 함수를 기반으로 다중회귀 분석을 진행해주었습니다.
- 계수 추정, 결정계수 확인, 전체 유의성 검정, 독립표본 검정을 진행했습니다.
- 전체 기간 및 지역에 대한 회귀분석 결과 는 0.873으로 모델을 신뢰할 수 있습니다. t-검정 결과 노동, 자본, 에너지의 p-value가 모두 0에 가까우므로 유의하다고 해석했습니다.
이렇게 선정된 3개의 변수 중 에너지를 독립변수, 생산성은 종속변수로 지정한 후 연도별 지역별로 회귀분석을 진행하였고 에너지 생산요소의 자원배분 효율성을 평가하였습니다.

## Ch4. 지역별 에너지 자원배분 분석 및 온실가스 추이

### [지역별 에너지 자원배분]

- 각 변수 도출 계산

![각 변수 도출 계산](https://github.com/Gayeon6423/Analysis-of-Resource-Allocation-Efficiency-in-Manufacturing-Industry-Linked-to-Greenhouse-Gas-Data/assets/113704015/40472a72-696e-48b9-a4a2-f5f2a2b57c44)

- 1999년, 2009년, 2019년 3년간의 에너지 자원배분의 효율성 변화 추이

![에너지 자원배분의 효율성 변화 추이](https://github.com/Gayeon6423/Analysis-of-Resource-Allocation-Efficiency-in-Manufacturing-Industry-Linked-to-Greenhouse-Gas-Data/assets/113704015/637942d6-907e-4564-9d8c-62b977a0801a)

- 1999년~2019년의 실질 부가가치 성장률 및 지역별 제조업 온실가스 추이

![실질 부가가치 성장률 및 지역별 제조업 온실가스 추이](https://github.com/Gayeon6423/Analysis-of-Resource-Allocation-Efficiency-in-Manufacturing-Industry-Linked-to-Greenhouse-Gas-Data/assets/113704015/4172bfc1-5f17-45d1-aa55-1c54276fcbfd)

## Ch5. 한계와 의의

- 한계 : 본 연구에서는 전체 제조업의 평균 데이터를 사용해서 분석을 진행했습니다. 추후 연구에서는 제조업의 산업을 분류해서 산업별 자원배분의 특성과 온실가스 배출량을 파악한다면 더욱 의미있는 결과가 나올 것으로 기대됩니다.
- 의의 : 경제 이론을 기반으로 실제 한국의 지역 간 제조업의 에너지 자원배분이 효율적으로 이루어지고 있는지 확인하였고, 온실가스 배출량 추이를 분석하여 비교하였습니다. 이를 통해 기후변화 대응 분야에서의 정책 시사점을 도출해보았습니다. 특히 지자체별 정책 제안과 에너지 불평등 해소 방안에 대한 실질적인 제언을 통해 사회적 가치를 창출해보았습니다.

## Ch6. 소감 및 피드백

- **소감**

경제 모형과 통계 모형을 활용해서 자원 배분의 효율성을 직접 파악해보았고 중요성을 파악할 수 있었습니다. 데이터 분석을 통해서 실제 지역별 맞춤형 정책 인사이트를 도출하는 과정이 매우 흥미로웠습니다.

기존에는 기후변화 문제를 해결하기 위해서는 온실가스 배출량을 감축시키고 에너지 자원 사용량을 줄이는 것만이 좋은 것이라고 생각했었습니다. 하지만 자료를 조사해보면서 에너지 자원을 효율적으로 배분하며 온실가스 배출량을 감소시키며 탈동조화를 실현해나가는 것이 중요하고 느끼게 되었습니다.

생산함수를 로그변환 시킨 후 회귀분석, 생산함수의 편미분을 통한 한계 생산물 계산 후 회귀분석 등의 분석을 진행하였습니다. 이렇게 기존 경제 모형을 변형하여 통계적인 분석을 진행하는 점이 새로웠고 많이 배워갈 수 있었습니다.

3개월 동안 팀원분들이 잘 따라와주어서 정말 고마웠고 함께 했기에 더욱 많은 것을 얻어갈 수 있었다고 느꼈습니다. 

- **동료 피드백**

| 성명 | 피드백1 | 피드백2 | 피드백3 | 피드백4 |
| --- | --- | --- | --- | --- |
| 정가연 |  |  |  |  |

# 7. 증빙자료

- 보고서 및 발표자료

https://drive.google.com/file/d/1xm32y4Wg1k-_wunLZi2q-ceDnJxa0Vfx/view?usp=sharing

- 코드

https://colab.research.google.com/drive/1RLG5km2-NzU4nDBUy3H3WmLsg2eFPj_o?usp=sharing
