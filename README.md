# Jupyter Notebooks로 Web스크레이핑하기

[![Promo](https://github.com/bright-kr/LinkedIn-Scraper/raw/main/Proxies%20and%20scrapers%20GitHub%20bonus%20banner.png)](https://brightdata.co.kr/) 

이 가이드는 대화형 코딩, 데이터 분석 및 시각화를 위해 Jupyter Notebooks를 사용하여 Web스크레이핑을 수행하는 방법을 설명합니다.

- [Jupyter Notebooks란 무엇입니까?](#what-are-jupyter-notebooks)
- [Web스크레이핑에 Jupyter Notebooks를 사용하는 이유는 무엇입니까?](#why-use-jupyter-notebooks-for-web-scraping)
- [Web스크레이핑에 Jupyter Notebooks를 사용하는 방법](#how-to-use-jupyter-notebooks-for-web-scraping)
  - [1단계: 환경 설정 및 의존성 설치](#step-1-set-up-the-environment-and-install-dependencies)
  - [2단계: 대상 페이지 정의](#step-2-define-the-target-page)
  - [3단계: 데이터 가져오기](#step-3-retrieve-the-data)
  - [4단계: 데이터가 올바른지 확인](#step-4-ensure-data-is-correct)
  - [5단계: 데이터 시각화](#step-5-visualize-the-data)
  - [6단계: 모두 합치기](#step-6-put-it-all-together)
- [Jupyter Notebook Web스크레이핑의 사용 사례](#use-cases-of-jupyter-notebook-web-scraping)
- [결론](#conclusion)

## What Are Jupyter Notebooks?

Jupyter Notebook App은 웹 브라우저를 통해 [노트북 문서](https://jupyter-notebook-beginner-guide.readthedocs.io/en/latest/what_is_jupyter.html#notebook-document)를 편집하고 실행할 수 있게 해주는 서버-클라이언트 애플리케이션입니다. Jupyter [notebook](https://docs.jupyter.org/en/latest/)은 “컴퓨터 코드, 일반 언어 설명, 데이터, 차트, 그래프 및 도형, 대화형 컨트롤을 결합한 공유 가능한 문서”입니다. 노트북 애플리케이션은 데스크톱 애플리케이션으로 실행할 수도 있고 원격 서버에 설치할 수도 있습니다.

![The Jupyter Notebook App interface](https://github.com/bright-kr/jupyter-notebooks-web-scraping/blob/main/Images/image-85.png)

Jupyter Notebooks는 노트북 문서 내의 코드를 실행하는 역할을 하는 계산 엔진인 “커널(kernel)”을 중심으로 구성됩니다. 특히 `ipython` 커널은 Python 코드를 실행하며, 다른 언어용 커널도 사용할 수 있습니다.

![Launching a new document via the ipython kernel](https://github.com/bright-kr/jupyter-notebooks-web-scraping/blob/main/Images/image-86.png)

앱의 대시보드는 로컬 파일 표시, 기존 노트북 문서 열기, 문서의 커널 관리 등과 같은 일반적인 작업을 지원합니다:

![The Jupyter Notebooks’ dashboard](https://github.com/bright-kr/jupyter-notebooks-web-scraping/blob/main/Images/image-87.png)

## Why Use Jupyter Notebooks for Web Scraping?

Jupyter Notebooks의 일부 설계 특성은 [web scraping](https://brightdata.co.kr/blog/how-tos/what-is-web-scraping) 목적에 매우 유용합니다:

- **대화형 개발(Interactive Development)**: 셀(cell)이라고 하는 작고 관리하기 쉬운 단위로 코드를 작성하고 실행합니다. 각 셀은 독립적으로 동작하므로 테스트 및 디버깅이 단순해집니다.
- **정리된 문서화(Organized Documentation)**: 셀 내에서 Markdown을 사용해 코드를 문서화하고, 로직을 설명하며, 메모나 지침을 제공할 수 있습니다.  
- **원활한 데이터 분석 통합(Seamless Data Analysis Integration)**: `pandas`, `matplotlib`, `seaborn` 등과 같은 Python 라이브러리로 스크레이핑한 데이터를 즉시 처리하고 분석할 수 있습니다.
- **재현성과 공유(Reproducibility and Sharing)**: Jupyter Notebooks를 `.ipynb` 파일로 쉽게 공유하거나 [ReST](https://docutils.sourceforge.io/rst.html), Markdown 등과 같은 형식으로 변환할 수 있습니다.

### Pros and Cons

다음은 데이터 스크레이핑에 Jupyter Notebooks를 사용할 때의 장단점입니다:

#### **Pros**

- **단계별 디버깅(Step-by-Step Debugging)**: 각 셀이 독립적으로 실행되므로 데이터 추출 코드를 더 작은 섹션으로 나눌 수 있습니다. 이를 통해 개별 셀을 실행하면서 세부 수준에서 문제를 식별하여 디버깅하기가 더 쉬워집니다.  
- **포괄적인 문서화(Comprehensive Documentation)**: 셀 내 Markdown을 사용하여 스크레이핑 코드를 문서화하고, 기능을 설명하며, 설계 결정을 정당화할 수 있습니다.  
- **유연성(Flexibility)**: Jupyter Notebooks를 사용하면 Web스크레이핑, 데이터 정제, 분석을 단일 환경에서 원활하게 통합할 수 있습니다. 이를 통해 스크레이핑을 위한 IDE와 분석을 위한 다른 환경 등 서로 다른 도구 사이를 전환할 필요가 없습니다.  

**Cons**  

- **대규모 프로젝트에는 적합하지 않음(Not Ideal for Large-Scale Projects)**: 노트북은 길어지고 다루기 어려워지는 경향이 있어 대규모 데이터 스크레이핑 프로젝트에는 덜 적합합니다.
- **성능 제한(Performance Limitations)**: 대규모 데이터셋로 작업하거나 긴 스크립트를 실행하면 Jupyter Notebooks가 느려지거나 심지어 멈출 수 있습니다.
- **자동화에 제한적(Limited for Automation)**: Jupyter Notebooks는 예약 또는 자동화된 워크플로보다 대화형 수동 실행을 위해 설계되었습니다. 스크레이퍼를 일정에 따라 실행하거나 더 큰 시스템에 통합해야 한다면 스크립트 기반 접근 방식이 더 적합합니다.

## How to Use Jupyter Notebooks for Web Scraping

### Step 1: Set Up the Environment and Install Dependencies

이 튜토리얼을 재현하려면 Python 3.6 이상이 설치되어 있어야 합니다.

`venv/` [가상 환경](https://docs.python.org/3/library/venv.html) 디렉터리를 생성합니다:

```bash
python -m venv venv
```

Windows에서 활성화하려면 다음을 실행합니다:

```bash
venv\Scripts\activate
```

macOS/Linux에서는 다음을 실행합니다:

```bash
source venv/bin/activate
```

이 튜토리얼에 필요한 모든 라이브러리를 설치합니다:

```bash
pip install requests beautifulsoup4 pandas jupyter seaborn
```

이 라이브러리들은 다음 용도로 사용됩니다:

- [**`requests`**](https://requests.readthedocs.io/en/latest/): HTTP 요청를 수행합니다.
- [**`beautifulsoup4`**](https://beautiful-soup-4.readthedocs.io/en/latest/): HTML 및 XML 문서를 파싱합니다.
- [**`pandas`**](https://pandas.pydata.org/): CSV 파일이나 테이블 같은 구조화된 데이터를 다루기에 이상적인 강력한 데이터 조작 및 분석 라이브러리입니다.
- [**`jupyter`**](https://pypi.org/project/jupyter/): Python 코드를 실행하고 공유하기 위한 웹 기반 대화형 개발 환경으로, 분석 및 시각화에 적합합니다.
- [**`seaborn`**](https://seaborn.pydata.org/): [Matplotlib](https://matplotlib.org/) 기반의 Python 데이터 시각화 라이브러리입니다.

`scraper/` 폴더로 이동합니다:

```bash
cd scraper
```

다음 명령으로 새 Jupyter Notebook을 초기화합니다:

```bash
jupyter notebook
```

이제 `locahost:8888`을 통해 Jupyter Notebook App에 접근할 수 있습니다.

“New > Python 3” 옵션을 클릭하여 새 파일을 생성합니다:

![Creating a new Jupyter Notebook file](https://github.com/bright-kr/jupyter-notebooks-web-scraping/blob/main/Images/image-84.png)

새 파일은 자동으로 `untitled.ipynb`로 생성됩니다. 대시보드에서 이를 `analysis.ipynb`로 이름을 변경합니다:

![Renaming a Jupyter Notebook file](https://github.com/bright-kr/jupyter-notebooks-web-scraping/blob/main/Images/image-83.png)

이 단계가 끝났을 때 프로젝트 구조는 다음과 같습니다:

```
scraper/
    ├── analysis.ipynb
    └── venv/
```

### Step 2: Define the Target Page

웹사이트 [worldometer](https://www.worldometers.info/)에서 데이터를 스크레이핑하겠습니다. 대상 페이지는 연도별 [미국의 CO2 배출량](https://www.worldometers.info/co2-emissions/us-co2-emissions/)과 관련된 페이지로, 다음과 같은 표 형태 데이터를 제공합니다:

![The tabular data about the C02 emissions per year in United States](https://github.com/bright-kr/jupyter-notebooks-web-scraping/blob/main/Images/image-82.png)

### Step 3: Retrieve the Data

다음은 대상 페이지에서 데이터를 가져와 CSV 파일로 저장하는 Python 코드입니다:

```python
import requests
from bs4 import BeautifulSoup
import csv

# URL of the website
url = "https://www.worldometers.info/co2-emissions/us-co2-emissions/"

# Send a GET request to the website
response = requests.get(url)
response.raise_for_status() 

# Parse the HTML content
soup = BeautifulSoup(response.text, "html.parser")

# Locate the table
table = soup.find("table") 

# Extract table headers
headers = [header.text.strip() for header in table.find_all("th")]

# Extract table rows
rows = []
for row in table.find_all("tr")[1:]:  # Skip the header row
    cells = row.find_all("td")
    row_data = [cell.text.strip() for cell in cells]
    rows.append(row_data)

# Save the data to a CSV file
csv_file = "emissions.csv"
with open(csv_file, mode="w", newline="", encoding="utf-8") as file:
    writer = csv.writer(file)
    writer.writerow(headers)  # Write headers
    writer.writerows(rows)    # Write rows

print(f"Data has been saved to {csv_file}")
```

이 코드는 다음을 수행합니다:

- `requests` 라이브러리로 `requests.get()` 메서드를 통해 대상 페이지에 GET 요청를 전송한 다음, `response.raise_for_status()` 메서드로 요청 오류를 확인합니다.
- `BeautifulSoup()` 클래스를 인스턴스화하여 HTML 콘텐츠를 파싱하고, `soup.find()` 메서드로 `table` 셀렉터를 찾기 위해 `BeautifulSoup`를 사용합니다. 특히 이 메서드는 데이터를 포함한 테이블을 찾는 데 유용합니다.
- 리스트 컴프리헨션으로 테이블의 헤더를 추출합니다.
- `for` 루프를 사용해 헤더 행을 건너뛰면서 테이블의 모든 데이터를 가져옵니다.
- 마지막으로 새 CVS 파일을 열고 가져온 모든 데이터를 그곳에 추가합니다.

이 코드를 셀에 붙여넣고 `SHIFT+ENTER`를 눌러 실행할 수 있습니다.

셀을 실행하는 다른 방법은 해당 셀을 선택한 다음 대시보드에서 “Run” 버튼을 누르는 것입니다:

![Running a cell in a Jupyter Notebook](https://github.com/bright-kr/jupyter-notebooks-web-scraping/blob/main/Images/image-81.png)

### Step 4: Ensure Data Is Correct

저장된 데이터가 있는 CSV 파일을 열고 변환이 올바르게 되었는지 확인합니다. 이를 위해 새 셀에 다음 코드를 입력합니다:

```python
import pandas as pd

# Load the CSV file into a pandas DataFrame
csv_file = "emissions.csv"
df = pd.read_csv(csv_file)

# Print the DataFrame
df.head()
```

이 코드는 다음을 수행합니다:

- `pandas`의 `pd.read_csv()` 메서드로 CSV 파일을 데이터 프레임으로 엽니다.
- `df.head()` 메서드로 데이터 프레임의 첫 5개 행을 출력합니다.

기대 결과는 다음과 같습니다:

![The first five rows of the data frame](https://github.com/bright-kr/jupyter-notebooks-web-scraping/blob/main/Images/image-80.png)

### Step 5: Visualize the Data

`seaborn`을 사용하여 연도별 C02 배출량 추세를 보여주는 선형 차트를 생성합니다:

```python
import seaborn as sns
import matplotlib.pyplot as plt

# Load the CSV file into a pandas DataFrame
csv_file = "emissions.csv"
df = pd.read_csv(csv_file)

# Clean column names be removing extra spaces
df.columns = df.columns.str.strip().str.replace('  ', ' ')

# Convert 'Fossil CO2 Emissions (tons)' to numeric
df['Fossil CO2 Emissions (tons)'] = df['Fossil CO2 Emissions (tons)'].str.replace(',', '').astype(float)

# Ensure the 'Year' column is numeric
df['Year'] = pd.to_numeric(df['Year'], errors='coerce')
df = df.sort_values(by='Year')

# Create the line plot
plt.figure(figsize=(10, 6))
sns.lineplot(data=df, x='Year', y='Fossil CO2 Emissions (tons)', marker='o')

# Add labels and title
plt.title('Trend of Fossil CO2 Emissions Over the Years', fontsize=16)
plt.xlabel('Year', fontsize=12)
plt.ylabel('Fossil CO2 Emissions (tons)', fontsize=12)
plt.grid(True)
plt.show()
```

이 코드는 다음을 수행합니다:

- `pandas`를 사용하여:
    - CSV 파일을 엽니다.
    - `df.columns.str.strip().str.replace(' ', ' ')` 메서드로 불필요한 공백을 제거하여 열 이름을 정리합니다.
    - “Fossil CO2 Emissions (tons)” 열에 접근하여 `df['Fossil CO2 Emissions (tons)'].str.replace(',', '').astype(float)` 메서드로 데이터를 숫자로 변환합니다.
    - “Years” 열에 접근하고 `pd.to_numeric()` 메서드로 값을 숫자로 변환한 다음, `df.sort_values()` 메서드로 값을 오름차순으로 정렬합니다.
- 실제 플롯을 만들기 위해 `matplotlib` 및 `seaborn` 라이브러리( `seaborn`은 [`matplotlib`](https://matplotlib.org/) 기반이므로 `seaborn`을 설치하면 함께 설치됩니다)를 사용합니다.

기대 결과는 다음과 같습니다:

![The resulting plot](https://github.com/bright-kr/jupyter-notebooks-web-scraping/blob/main/Images/image-79.png)

### Step #6: Put It All Together

Web스크레이핑을 위한 전체 Jupyter Notebook은 다음과 같이 보입니다:

![The entire Jupyter Notebook document](https://github.com/bright-kr/jupyter-notebooks-web-scraping/blob/main/Images/image-78.png)

## Use Cases of Jupyter Notebook Web Scraping

다음은 Jupyter Notebooks의 다른 활용 사례입니다:

- **내부 교육용 튜토리얼**. Jupyter notebooks를 주니어 개발자를 위한 단계별 튜토리얼로 사용할 수 있습니다. 설명에는 Markdown을 사용하고, 독립적으로 실행 가능한 개별 코드 블록에는 셀을 사용합니다.
- **연구 및 개발**. 스크레이핑 프로젝트에 여러 차례의 시행착오가 필요한 경우, 모든 테스트를 단일 Notebook에 유지하고 성공한 테스트를 Markdown으로 강조할 수 있습니다.
- **데이터 탐색**. 위 튜토리얼에서 볼 수 있듯이 Jupyter 라이브러리는 데이터 탐색 및 분석을 위해 특별히 설계되었습니다.

## Conclusion

Jupyter Notebooks는 Web스크레이핑에 강력한 도구가 될 수 있지만, Web스크레이핑 작업을 확장하거나 작업을 자동화하는 측면에서는 가장 효율적인 솔루션은 아닙니다.

Bright Data의 [Web Scrapers](https://brightdata.co.kr/products/web-scraper)는 데이터 수집 노력을 단순화하고 강화합니다. 100개 이상의 도메인에 대한 전용 엔드포인트, 대량 요청 처리, 자동 IP 로테이션, 그리고 [CAPTCHA solving](https://github.com/bright-kr/Captcha-solver) 기능을 제공합니다.

지금 무료 Bright Data 계정을 생성하여 스크레이핑 솔루션을 사용해 보고 프록시도 테스트해 보십시오!