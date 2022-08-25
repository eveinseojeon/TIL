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

- 집계가 수행된 "이후에" <u>집계 결과를 바탕으로 자료를 필터링</u> (**WHERE**문은 필터링을 먼저 함)
- 실행 순서: **WHERE** -> **GROUP BY** -> 집계 -> **HAVING**
- **GROUP BY**를 통해 집계되는 것에만 적용됨

---

### AS

**SELECT** column **AS** new_name **FROM** table;

**SELECT** **SUM**(column) **AS** new_name **FROM** table;

- 열이나 결과에 별칭(대체 이름)을 부여
- <u>순전히 data output의 가독성을 위한 것</u>으로, 특히 열에 함수를 적용할 때 유용함
- **AS** 연산자는 쿼리의 맨 마지막에 실행됨. 별칭들은 맨 마지막에 할당되기 때문에 별칭으로는 필터링을 할 수 없음 -> <u>**WHERE**, **GROUP BY**, **HAVING**, 조건, 비교 연산자 등에서는 별칭을 사용할 수 없음. 오직 **SELECT**에서만 사용할 수 있음.</u>

---

### JOIN

- 여러 테이블을 하나로 결합하는 연산
- **OUTER JOIN**의 종류에 따라 결합되는 테이블 중 하나에만 있는 정보를 처리하는 방식을 지정

---

#### INNER JOIN

**SELECT** * **FROM** tableA **INNER JOIN** tableB **ON** tableA.col_match = tableB.col_match;

- 두 테이블 모두에서 매칭되는 값만 결과로 출력.
- 벤다이어그램이 대칭이므로 두 테이블 순서, 열 매칭 순서를 바꿔도 결과는 같음.
- **SELECT** *을 하면 col_match 열이 두 번 중복됨. 중복을 제거하기 위해 **SELECT** 뒤에 원하는 열들을 지정할 때 두 테이블에서 공유하는 col_match 열의 경우 tableA.col_match와 같이 그 열을 참조하는 테이블이 어떤 것인지 지정해야 함.
- **JOIN**만 써있으면 **INNER**가 생략된 **INNER JOIN**

---

#### FULL OUTER JOIN

**SELECT** * **FROM** tableA **FULL OUTER JOIN** tableB **ON** tableA.col_match = tableB.col_match;

- 두 테이블에 모두 있든 한 테이블에만 있든 상관없이 모든 것을 포함
- 벤다이어그램이 대칭이므로 두 테이블 순서, 열 매칭 순서를 바꿔도 결과는 같음

**SELECT** * **FROM** tableA **FULL OUTER JOIN** tableB **ON** tableA.col_match = tableB.col_match **WHERE** tableA.colA **IS** null **OR** tableB.colB **IS** null;

- **JOIN**을 실행한 후에 **WHERE**문을 써서 추가로 필터링
- 

---

#### LEFT (OUTER) JOIN

**SELECT** * **FROM** tableA **LEFT OUTER JOIN** tableB **ON** tableA.col_match = tableB.col_match;

- 더이상 벤다이어그램이 대칭이 아니며, 순서가 중요
- 테이블A에만 있는 것, 두 테이블 모두에 있는 것을 출력. 테이블B에만 있는 것은 가져오지 않음.

**SELECT** * **FROM** tableA **LEFT OUTER JOIN** tableB **ON** tableA.col_match = tableB.col_match **WHERE** tableB.colB **IS** null;

- 테이블A에만 고유한 항목을 구할 수 있음

---

#### RIGHT (OUTER) JOIN

**SELECT** * **FROM** tableA **RIGHT OUTER JOIN** tableB **ON** tableA.col_match = tableB.col_match;

- **LEFT OUTER JOIN**의 테이블 순서를 바꾼 것과 정확히 같음. y축을 따라 뒤집어진 것.
- 테이블B에만 있는 것, 두 테이블 모두에 있는 것을 출력. 테이블A에만 있는 것은 가져오지 않음.

**SELECT** * **FROM** tableA **RIGHT OUTER JOIN** tableB **ON** tableA.col_match = tableB.col_match **WHERE** tableA.colA **IS** null;

- 테이블B에만 고유한 항목을 구할 수 있음

---

### UNION

**SELECT** col_name(s) **FROM** table1 **UNION** **SELECT** col_name(s) **FROM** table2;

- **UNION** 연산자를 사용하면 2개 이상의 **SELECT**문의 결과 세트를 결합할 수 있음. **JOIN**과 **UNION**의 기본적인 차이는 **UNION**은 두 결과를 직접 붙인다는 것. 두 **SELECT**문의 결과를 서로의 바로 위에서 붙여줌.
- 서로의 바로 위에 결과를 쌓을 수 있도록 열이 일치해야 함

**SELECT** col_name(s) **FROM** table1 **UNION** **SELECT** col_name(s) **FROM** table2 **ORDER BY** col;

- 특정 열을 기준으로 자료 정렬도 가능

---











---

## 메모

41. FULL OUTER JOIN 다시 듣기 (8:19~)

45~



