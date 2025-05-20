# sdfsfd

코드 내용

!pip install pandas matplotlib seaborn openpyxl

import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

# 주별 2020년 인구 데이터
state_populations = {
    'California': 39538223,
    'Texas': 29145505,
    'Virginia': 8631393,
    'Illinois': 12812508,
    'Washington': 7705281
}

# 주별 월별 누적 확진자 수 데이터 (예시 데이터)
# 실제 데이터는 각 주 보건부 또는 신뢰할 수 있는 데이터 소스에서 수집해야 합니다.
# 아래는 예시로 생성한 데이터입니다.
dates = pd.date_range(start='2020-03-01', end='2022-09-01', freq='MS')
data = {
    'Date': dates,
    'California': [1000 * i for i in range(len(dates))],
    'Texas': [900 * i for i in range(len(dates))],
    'Virginia': [300 * i for i in range(len(dates))],
    'Illinois': [500 * i for i in range(len(dates))],
    'Washington': [200 * i for i in range(len(dates))]
}
df_cases = pd.DataFrame(data)

# 인구 대비 누적 확진자 비율 계산
for state in state_populations:
    df_cases[state] = df_cases[state] / state_populations[state] * 100

# 데이터 변환: 시각화를 위해 'long' 형태로 변환
df_melted = df_cases.melt(id_vars='Date', var_name='State', value_name='Cases_Percentage')

# 시각화
plt.figure(figsize=(14, 7))
sns.lineplot(data=df_melted, x='Date', y='Cases_Percentage', hue='State')
plt.title('인구 대비 누적 코로나19 확진자 비율 추이 (2020-03 ~ 2022-09)')
plt.ylabel('확진자 비율 (%)')
plt.xlabel('날짜')
plt.legend(title='주')
plt.grid(True)
plt.tight_layout()
plt.show()
