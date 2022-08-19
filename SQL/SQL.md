# Udemy <데이터 역량 강화를 위한 SQL 부트캠프 2022>

-> PostgreSQL, PgAdmin 사용

---

### SELECT

**SELECT** column **FROM** table;

**SELECT** c1, c2 **FROM** table1;

- **SELECT** 등 키워드를 소문자로 써도 동작하지만 대문자가 표준화된 표기법
- 맨 끝에 세미콜론(;)은 쿼리가 끝났음을 나타냄. 없어도 동작은 함
- 웬만하면 *보다는 열 이름을 특정하여 쿼리하기

---

### SELECT DISTINCT

**SELECT DISTINCT** column **FROM** table;

**SELECT DISTINCT**(column) **FROM** table;

- 그 테이블이나 그 열에서 (중복을 허용하지 않고) 고유값만 찾는 함수

---

### COUNT

**SELECT COUNT**(column) **FROM** table;

- 행의 개수를 세는 함수
- 괄호 필요!
- 어떤 열 이름을 쓰든 *을 쓰든 결과는 항상 똑같지만 특정 열 이름을 쓰는 것이 좋다. 질문이 뭐였는지 명확히 하기 위해서.

**SELECT COUNT**(**DISTINCT** column) **FROM** table;

- 그 열에 고유값이 몇 개인지 세는 함수

---

### SELECT WHERE

**SELECT** c1, c2 **FROM** table **WHERE** conditions;

- 조건에 맞는 행을 반환하는 함수

- 비교 연산자: =, >, <, >=, <=, !=
- 논리 연산자: **AND**, **OR**, **NOT**
- 문자열을 구분하기 위하여 작은 따옴표 사용
- 조건을 적용하여 필터링할 때는 열을 두 개 이상 요청하는 것이 유용함

---

### ORDER BY

**SELECT** c1, c2 **FROM** table **ORDER BY** c1 **ASC**/**DESC**;

- 쿼리 결과를 특정 순서로 반환하도록 하는 함수
- 아무것도 안 쓰면 디폴트는 **ASC**

**SELECT** c1, c2, c3 **FROM** table **ORDER BY** c1 **DESC**, c3 **ASC**;

- 하나의 열에 중복되는 항목이 있는 경우 **ORDER BY**를 여러 열에 사용할 수 있음
- 오름차순, 내림차순 여부를 각각 지정해줄 수 있음
- **ORDER BY**에서만 열을 지정하고 **SELECT**에서는 지정하지 않을 수도 있음. 그러나 함께 지정하는 것이 좋음

---

### LIMIT

**SELECT** * **FROM** table **ORDER BY** c1 **LIMIT** 5;

- 쿼리에서 반환되는 행의 개수를 제한하는 함수
- **ORDER BY**와 함께 사용하여 상위 몇 개의 행만 표시하여 테이블의 레이아웃을 파악하려고 할 때 유용함
- 쿼리 요청의 가장 마지막에 써줌

**SELECT** * **FROM** table **LIMIT** 1;

- 위 간단한 쿼리문으로 실제 테이블이 어떻게 구성되어 있는지 빠르게 파악할 수 있음
- 열 이름은 SQL 키워드와 일치하지 않도록 주의해야 한다.

---

### BETWEEN

value **BETWEEN** low **AND** high

- 값을 값 범위와 비교할 때 사용
- **WHERE**문 뒤에 사용하는 조건문으로 쓰임
- 양쪽의 엔드포인트 low값과 high값 모두 포함
- value >= low **AND** value <= high와 같음
- 타임스탬프 정보를 처리할 때는 'YYYY-MM-DD' 형식으로 쓰되, 날짜, 시간, 분 이하가 모두 포함됨. PostgreSQL에서 하루의 시간이 0:00에 시작되는지 24:00에 시작되는지 정해야 함. 이것이 논리에 실질적인 영향을 미침. 원하는 결과가 나오는지 꼼꼼하게 확인해봐야 함

---

### IN

value **IN** (option1, option2, ...)

- **OR**을 여러번 사용하는 대신 **IN**을 사용

---

### LIKE, ILIKE

- 패턴 매칭 연산자
- 와일드카드 문자(%, _ 등)를 사용해서 문자열 데이터에 대해 패턴 매칭 수행
- 문자의 순서나 수에 관계없이 매칭되는 %, 단 하나의 문자하고만 매칭되는 _
- **LIKE**는 대소문자를 구분하고, **ILIKE**는 구분 안 함

---

### 집계 함수(Aggregate functions)

- **AVG**(), **COUNT**(), **MAX**(), **MIN**(), **SUM**()

- 오직 **SELECT**절이나 **HAVING**절에서만 호출됨
- **AVG**()는 소수점까지 길게 반환하므로 **ROUND**()와 함께 사용
- **COUNT**()는 행의 개수를 반환하므로 열 이름을 안 넣고 **COUNT**(*)를 해도 항상 같은 결과

---

### GROUP BY

**SELECT** category_col, **AGG**(data_col) **FROM** table **WHERE** category_col != 'A' **GROUP BY** category_col;

- **GROUP BY**절은 **FROM**문 바로 뒤 또는 **WHERE**문 바로 뒤에 와야 함
- **GROUP BY**로 묶이는 열들의 순서는 중요하지 않음. 그러나 대부분의 경우 **SELECT**문과 **GROUP BY**문의 순서를 동일하게 지정
- **DATE**()는 타임스탬프 정보 중 날짜 부분만 추출하는 함수

---

### HAVING























