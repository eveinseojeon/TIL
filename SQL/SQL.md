# [Udemy <데이터 역량 강화를 위한 SQL 부트캠프 2022>](https://www.udemy.com/course/best-sql-2022/)

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
- 타임스탬프 정보를 처리할 때는 'YYYY-MM-DD' 형식으로 쓰되, 날짜, 시간, 분 이하가 모두 포함됨. PostgreSQL에서 하루의 시간이 0:00에 시작되는지 24:00에 시작되는지 정해야 함. 이것이 논리에 실질적인 영향을 미침. 원하는 결과가 나오는지 꼼꼼하게 확인해봐야 함. **BETWEEN** 연산자에서 이런 문제가 생길 수 있음. 부등호를 사용하면 해결됨.

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

**SELECT** category_col, **AGG**(data_col) **FROM** table **WHERE** category_col != 'A' **GROUP BY** category_col **HAVING** **AGG**(data_col) > 10;

- 집계가 수행된 "이후에" <u>집계 결과를 바탕으로 자료를 필터링</u> (**WHERE**문은 필터링을 먼저 함)
- 실행 순서: **WHERE** -> **GROUP BY** -> 집계 -> **HAVING**
- **GROUP BY**를 통해 집계되는 것에만 적용됨

---

### AS

**SELECT** column **AS** new_name **FROM** table;

**SELECT** **SUM**(column) **AS** new_name **FROM** table;

- 열이나 결과에 별칭(대체 이름)을 부여
- <u>순전히 data output의 가독성을 위한 것</u>으로, 특히 열에 함수를 적용할 때 유용함
- <u>**AS** 연산자는 쿼리의 맨 마지막에 실행됨.</u> 별칭들은 맨 마지막에 할당되기 때문에 별칭으로는 필터링을 할 수 없음 -> <u>**WHERE**, **GROUP BY**, **HAVING**, 조건, 비교 연산자 등에서는 별칭을 사용할 수 없음. 오직 **SELECT**에서만 사용할 수 있음.</u>

---

## JOIN

- 여러 테이블을 하나로 결합하는 연산
- **OUTER JOIN**의 종류에 따라 결합되는 테이블 중 하나에만 있는 정보를 처리하는 방식을 지정

---

### (INNER) JOIN

**SELECT** * **FROM** tableA **INNER JOIN** tableB **ON** tableA.col_match = tableB.col_match;

- 두 테이블 모두에서 매칭되는 값만 결과로 출력.
- 벤다이어그램이 대칭이므로 두 테이블 순서, 열 매칭 순서를 바꿔도 결과는 같음.
- **SELECT** *을 하면 col_match 열이 두 번 중복됨. 중복을 제거하기 위해 **SELECT** 뒤에 원하는 열들을 지정할 때 두 테이블에서 공유하는 col_match 열의 경우 tableA.col_match와 같이 그 열을 참조하는 테이블이 어떤 것인지 지정해야 함.
- **JOIN**만 써있으면 **INNER**가 생략된 **INNER JOIN**

---

### FULL OUTER JOIN

**SELECT** * **FROM** tableA **FULL OUTER JOIN** tableB **ON** tableA.col_match = tableB.col_match;

- 두 테이블에 모두 있든 한 테이블에만 있든 상관없이 모든 것을 포함
- 벤다이어그램이 대칭이므로 두 테이블 순서, 열 매칭 순서를 바꿔도 결과는 같음

**SELECT** * **FROM** tableA **FULL OUTER JOIN** tableB **ON** tableA.col_match = tableB.col_match **WHERE** tableA.colA **IS** null **OR** tableB.colB **IS** null;

- **JOIN**을 실행한 후에 **WHERE**문을 써서 추가로 필터링

---

### LEFT (OUTER) JOIN

**SELECT** * **FROM** tableA **LEFT OUTER JOIN** tableB **ON** tableA.col_match = tableB.col_match;

- 더이상 벤다이어그램이 대칭이 아니며, 순서가 중요
- 테이블A에만 있는 것, 두 테이블 모두에 있는 것을 출력. 테이블B에만 있는 것은 가져오지 않음.

**SELECT** * **FROM** tableA **LEFT OUTER JOIN** tableB **ON** tableA.col_match = tableB.col_match **WHERE** tableB.colB **IS** null;

- 테이블A에만 고유한 항목을 구할 수 있음

---

### RIGHT (OUTER) JOIN

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

## Timestamp

- TIME, DATE, TIMESTAMP, TIMESTAMPTZ
- 시간, 날짜, 표준시간대 정보들 중 무엇을 기록할지 장기적 관점에서 신중하게 고려하여 결정해야 함. 나중에 정보 추출을 할 수는 있지만 되돌아가서 더할 수는 없기 때문에.
- 타임스탬프 정보에 **MAX**, **MIN**, 비교 연산자 등을 사용할 수 있음

**SHOW** **ALL**;

- name, setting, description 열을 보여줌

**SHOW** TIMEZONE;

- 현재 내가 Asia/Seoul의 표준시간대에서 작업하고 있음을 보여줌

**SELECT** NOW();

- 표준시간대의 타임스탬프라는 설명과 함께 날짜, 시간, 표준시간대([그리니치 평균시](https://ko.wikipedia.org/wiki/%EA%B7%B8%EB%A6%AC%EB%8B%88%EC%B9%98_%ED%8F%89%EA%B7%A0%EC%8B%9C)) 정보를 보여줌

**SELECT** TIMEOFDAY();

- NOW와 거의 같은 정보를 알려주는데 <u>문자열로 된 정보</u>라서 가독성이 좋고 저장도 더 쉬움. 특정 타임스탬프 형식은 아님.
- 요일, 월, 일, 시간, 연, 표준시간대 정보를 보여줌

**SELECT** **CURRENT_TIME**;

- NOW의 서브셋으로, 현 시간을 보여줌

**SELECT** **CURRENT_DATE**;

- NOW의 서브셋으로, 현 날짜(연, 월, 일)를 보여줌

---

### EXTRACT

**SELECT** **EXTRACT**(**YEAR** **FROM** date_col) **AS** new_name **FROM** table;

- 데이터 값의 서브 컴포넌트를 추출하되 연(YEAR), 월(MONTH), 일(DAY), 주(WEEK), 분기(QUARTER), 요일(dow: day of week)별로 추출할 수 있음

---

### AGE

**SELECT** AGE(date_col) **FROM** table;

- 해당 타임스탬프 내에서 현재까지의 시기를 계산해서 알려줌

---

### TO_CHAR

**SELECT** TO_CHAR(date_col, 'mm-dd-yyyy') **FROM** table;

- 하나의 데이터 유형을 문자 유형으로 바꿔주는 일반 함수
- 타임스탬프 서식 작성을 할 때 매우 유용함
- [데이터 유형 포매팅 함수 PostgreSQL 공식 문서](https://www.postgresql.org/docs/current/functions-formatting.html) 참조

---

### 수리 함수와 연산자

- [수리 함수와 연산자 PostgreSQL 공식 문서](https://www.postgresql.org/docs/current/functions-math.html) 참조

---

### 문자열 함수와 연산자

- [문자열 함수와 연산자 PostgreSQL 공식 문서](https://www.postgresql.org/docs/current/functions-string.html) 참조

---

## 서브 쿼리

- 서브 쿼리를 쓰면 더 복잡한 쿼리를 만들 수 있다. 다른 쿼리의 결과에 대해 쿼리를 실행하거나 다른 쿼리의 결과를 사용할 수 있음. "단독" 쿼리 결과를 얻고자 서브 쿼리 사용 가능

**SELECT** student, grade **FROM** test_scores **WHERE** grade > (**SELECT** **AVG**(grade) **FROM** test_scores);

- 괄호 내 서브 쿼리가 먼저 계산됨
- <u>복잡한 쿼리일수록 길게 쓰기보다 서브 쿼리를 활용할 것!</u>
- 서브 쿼리의 결과가 단독 값으로 도출되면 비교 연산자를 쓸 수 있으나, 서브 쿼리의 결과가 다양한 값으로 도출되면 **IN** 연산자를 써야 함

---

### EXISTS

**SELECT** column **FROM** table **WHERE** **EXISTS**(**SELECT** column **FROM** table **WHERE** condition);

- 서브 쿼리에서 행의 존재를 테스트하는 데 사용됨
- 보통 서브 쿼리가 **EXISTS** 함수 뒤 괄호에 입력되어, 어떤 행이 서브 쿼리로 도출되었는지 확인
- 행의 여부에 따라 참, 거짓으로 결괏값이 나옴

---

### 셀프 조인

**SELECT** tableA.col, tableB.col **FROM** table **AS** tableA **JOIN** table **AS** tableB **ON** tableA.some_col = tableB.other_col;

- 테이블이 그 자체에 JOIN되어있는 쿼리
- 같은 테이블 내에 여러 행의 열 속 값들을 비교할 때 유용함
- 같은 테이블의 두 복사본의 JOIN처럼 보일 수 있으나, 테이블은 사실 복사된 게 아니고 SQL이 그래 보이게 한 것이다.
- 셀프 조인을 위한 특별 키워드 없다. 두 부분에 동시에 있는 동일한 테이블에서 그냥 표준 JOIN 구문.
- 셀프 조인을 사용할 때는 테이블에 별칭을 꼭 사용해라.

---

## 데이터베이스 및 테이블 만들기

### 데이터베이스 및 테이블을 만들 때 고려 사항

- 데이터가 어떻게 저장될지를 고려해 데이터 유형을 선택하는 데에 유의해야 함

- 어떤 데이터 유형이 있는지, 데이터 유형의 한계는 무엇인지 [데이터 유형 PostgreSQL 공식 문서](https://www.postgresql.org/docs/current/datatype.html)에서 확인하고 고르기!

- <u>온라인에서 최선의 관행을 찾는 것이 가장 좋음</u>

  Ex) 'How to store phone number PostgreSQL' 구글링

- 데이터베이스를 만들고 오래 보관하려고 한다면 사용하지 않는 히스토리 정보를 삭제할 것. 그러나 백업은 불가능. 지우고 나면 돌아가서 정보를 추가할 수 없다.

---

### 데이터 유형

- Boolean
  - True, False
- Character
  - char, varchar, text
- Numeric
  - integer, floating-point, serial
- Temporal
  - time, date, timestamp, timestamptz, interval
- UUID(Universally Unique Identifiers)
- Array
  - 문자열, 숫자의 배열을 저장
- JSON
- HStore key-value pair
- 그 외 network address, geometric data 등의 특수 유형

---

### 기본키 및 외래키

- 기본키(primary key)
  - 테이블에서 모든 열을 고유하게 식별하기 위해 사용하는 열(또는 열 그룹)
  - integer based, unique and non-null column
  - 데이터 유형은 항상 **SERIAL**(smallserial, serial, bigserial 있음)
  - 열에 [PK]라고 적혀 있음
  - <u>테이블을 JOIN할 때 어떤 열을 사용해야 할지 쉽게 알려주기 때문에 중요!</u>
- 외래키(foreign key)
  - 다른 테이블의 행을 고유하게 식별하는, 테이블의 필드(또는 필드 그룹)
  - 다른 테이블의 기본키를 참조(reference)함
  - 외래키는 반복될 수 있음

- <u>referencing table 또는 child table</u>: 외래키를 포함하는 테이블

- <u>referenced table 또는 parent table</u>: 외래키가 레퍼런스하는 테이블

- 한 테이블은 다른 테이블과 얼마나 많은 관계를 맺고 있는지에 따라 여러 개의 외래키를 가질 수 있다.

- 테이블 간의 종속성을 확인하는 방법

  : Schemas -> public -> Tables -> 테이블 선택 -> Constraints -> 해당 테이블의 PK(금색)와 FK(회색)를 확인할 수 있음

  - 첫 번째 방법

    : FK 선택 -> 상단의 탭을 Dependencies로 바꾸면 해당 열의 종속성을 보여줌. 어떤 테이블의 PK를 참조하고 있는지.

  - 두 번째 방법

    : FK 선택 -> 우클릭 -> Properties -> Columns -> 참조하는 테이블과 PK 열을 보여줌

---

### Constraints(제약 조건)

- 테이블에서 열에 적용되는 규칙. 테이블의 어떤 것에든 제약 조건을 걸 수 있다.
- 데이터베이스에 유효하지 않은 데이터가 쓰이지 않도록 방지할 수 있음 -> 데이터베이스의 데이터에 대한 정확도와 신뢰도를 보장
- column constraints: 개별 열에 적용됨
  - **NOT NULL**, **UNIQUE**, **PRIMARY KEY**, FOREIGN KEY, **REFERENCES**, CHECK, EXCLUSION 등
- table constraints: 전체 테이블에 적용됨
  - CHECK (condition), REFERENCES, UNIQUE (column list), PRIMARY KEY (column list) 등

---

### CREATE

- 왼쪽 단에서 Servers -> PostgreSQL 14 -> Databases 우클릭 -> Create -> Database -> 이름 입력하고 저장 -> 방금 생긴 데이터베이스 우클릭하여 Refresh
- Query Tool 열어서 SQL 명령으로 테이블을 만들 수 있다.

**CREATE** **TABLE** table_name(

​    column_name **TYPE** column_constraint,

​    column_name **TYPE** column_constraint1 column_constraint2 column_constraint3,

​    table_constraint1 table_constraint2

)

**INHERITS** existing_table_name;

---

### INSERT















---

## MEMO

- 테이블이 들어있는 Schemas가 public이 아닌 경우, Schemas의 이름과 온점(.)을 테이블 앞에 붙여줘야 함

  Ex) **SELECT** * **FROM** cd.bookings;

---

## 다시 들을 부분

41. FULL OUTER JOIN (8:19~)

53. 서브 쿼리 (12:13~)

61~





제약 조건 예시들 굵은 글씨 수정

CREATE 일반 구문 확인





---

## 평가 시험 2

### Q1

SELECT * FROM cd.facilities;

### Q2

SELECT name, membercost FROM cd.facilities;

### Q3

SELECT * FROM cd.facilities

WHERE membercost != 0;

### Q4

SELECT facid, name, membercost, monthlymaintenance

FROM cd.facilities

WHERE membercost != 0

AND membercost < monthlymaintenance/50;

### Q5

SELECT * FROM cd.facilities

WHERE name LIKE '%Tennis%';

### Q6

SELECT * FROM cd.facilities

WHERE facid IN (1, 5);

### Q7

SELECT memid, surname, firstname, joindate

FROM cd.members

WHERE joindate >= '2012-09-01';

### Q8

SELECT DISTINCT(surname) FROM cd.members

ORDER BY surname

LIMIT 10;

### Q9

SELECT MAX(joindate) FROM cd.members;

### Q10

SELECT COUNT(*) FROM cd.facilities

WHERE guestcost >= 10;

### Q11

SELECT facid, SUM(slots) AS total_slots

FROM cd.bookings

WHERE (SELECT TO_CHAR(starttime, 'yyyy-mm')) = '2012-09'

GROUP BY facid

ORDER BY SUM(slots);

### Q12

SELECT facid, SUM(slots) AS total_slots

FROM cd.bookings

GROUP BY facid

HAVING SUM(slots) > 1000

ORDER BY facid;

### Q13

SELECT starttime, name

FROM cd.bookings AS B

INNER JOIN cd.facilities AS F

ON B.facid = F.facid

WHERE name LIKE 'Tennis Court%'

AND (SELECT TO_CHAR(starttime, 'yyyy-mm-dd')) = '2012-09-21'

ORDER BY starttime;

### Q14

SELECT starttime, firstname, surname

FROM cd.bookings AS B

INNER JOIN cd.members AS M

ON B.memid = M.memid

WHERE firstname = 'David' AND surname = 'Farrell';



