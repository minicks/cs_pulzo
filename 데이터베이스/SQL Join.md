<div align='center'>
    <h1>
        SQL Join
    </h1>
</div>



<h2>
    목차
</h2>

1. [JOIN](#1)
2. [INNER JOIN](#2)
3. [LEFT OUTER JOIN ](#3)
4. [RIGHT OUTER JOIN ](#4)
5. [FULL OUTER JOIN](#5)
6. [CROSS JOIN](#6)
7. [SELF JOIN](#7)
8. [참조](#8)



<div id=1>
    <h2>
        1. JOIN
    </h2>
</div>

두 개이상의 테이블이나 데이터베이스를 연결하여 데이터를 검색하는 방법. 

자신이 검색하고 싶은 컬럼이 다른 테이블에 있을 경우 주로 사용하며 여러 개의 테이블을 마치 하나의 테이블인 것처럼 활용하는 방법. 

보통 Primary key혹은 Foreign key로 두 테이블을 연결. 테이블을 연결하려면 적어도 하나의 칼럼은 서로 공유되고 있어야 함.



![post-thumbnail](https://media.vlpt.us/images/chayezo/post/5403f167-f07f-4dae-87f7-1d123c2f758c/99219C345BE91A7E32.png)

종류로는

- INNER JOIN 
- LEFT OUTER JOIN 
- RIGHT OUTER JOIN 
- FULL OUTER JOIN 
- CROSS JOIN 
- SELF JOIN



주로 사용하는 것은 inner, left, right join



**INNER JOIN** 은 <u>FROM</u> 또는 <u>WHERE</u> 절에서 지정할 수 있음. **OUTER JOIN** 및 **CROSS JOIN** 은 <u>FROM</u> 절에서만 지정할 수 있음. WHERE 및 HAVING 검색 조건과 결합된 조인 조건은 FROM 절에서 참조되는 기본 테이블에서 선택된 행을 제어.



오라클에는 OUTER JOIN 이 있지만, MySQL에는 없기 때문에 LEFT JOIN + RIGHT JOIN 으로 해야함. 



<div id=2>
    <h2>
        2. INNER JOIN
    </h2>
</div>

테이블을 **교집합**.

기준 테이블과 Join 한 테이블의 중복된 값을 보여줌. 

결과값은 A의 테이블과 B테이블이 모두 가지고 있는 데이터만 검색.

```
--문법--
SELECT
테이블별칭.조회할칼럼,
테이블별칭.조회할칼럼
FROM 기준테이블 별칭
INNER JOIN 조인테이블 별칭 ON 기준테이블별칭.기준키 = 조인테이블별칭.기준키...

--예제--
SELECT
A.NAME, --A테이블의 NAME조회
B.AGE --B테이블의 AGE조회
FROM EX_TABLE A
INNER JOIN JOIN_TABLE B ON A.NO_EMP = B.NO_EMP AND A.DEPT = B.DEPT
```



SQL은 **‘명시적 조인 표현’**(explicit)과 **‘암시적 조인 표현’**(implicit) 2개의 다른 조인식 구문을 지정.

**‘명시적 조인 표현’**에서는 테이블에 조인을 하라는 것을 지정하기 위해 JOIN 키워드를 사용하며, 그리고 나서 다음의 예제와 같이 ON 키워드를 조인에 대한 구문을 지정하는데 사용.

```mysql
SELECT *
FROM employee INNER JOIN department
  ON employee.DepartmentID = department.DepartmentID;
```



**‘암시적 조인 표현’**은 SELECT 구문의 FROM 절에서 그것들을 분리하는 컴마를 사용해서 단순히 조인을 위한 여러 테이블을 나열하기만 함. 그리하여 그것은 교차 조인(cross join)을 지정하면, WHERE 절은 추가적인 필터 구문(명시적 구문에서 조인 구문을 비교하는 역할을 하는)을 적용.

```mysql
SELECT *
FROM employee, department
WHERE employee.DepartmentID = department.DepartmentID;
```



내부 조인을 더 세부적으로 분류하여 **동일 조인**(Equi-Join), **자연 조인**(natural join), 또는 **교차 조인**(cross-join)으로도 나눌 수 있음.

### 2-1 Equi JOIN

**동일 조인**(Equi-Join)은 특별한 유형의 *비교자 기반의 조인*이며, 이것은 조인 구문에서 동등비교만을 사용한다. 다른 비교 연산자(`<`와 같은)를 사용하는 것은 동일 조인으로서의 조인의 자격을 박탈하는 것이다.

쉽게 말해 = 를 쓴 조인을 말한다.

```mysql
SELECT *
FROM employee JOIN department
  ON employee.DepartmentID = department.DepartmentID;
```



### 2-2 Natural JOIN

**자연 조인**(natural join)은 동일 조인의 한 유형으로 조인 구문이 조인된 테이블에서 동일한 컬럼명을 가진 2개의 테이블에서 모든 컬럼들을 비교함으로써, 암시적으로 일어나는 구문이다. 결과적으로 나온 조인된 테이블은 동일한 이름을 가진 컬럼의 각 쌍에 대한 단 하나의 컬럼만 포함하고 있다.

대부분의 전문가들은 NATURAL JOIN이 위험한 것이며, 그러므로 이것의 사용을 강력하게 비권장하고 있다.

```mysql
SELECT *
FROM employee NATURAL JOIN department;
```





<div id=3>
    <h2>
        3. LEFT OUTER JOIN 
    </h2>
</div>

기준테이블의 값 + 테이블과 기준 테이블의 중복된 값을 보여줌.

왼쪽 테이블을 기준으로 JOIN.

결과값은 A테이블의 모든 데이터와 A테이블과 B테이블의 중복되는 값이 검색

```mysql
--문법--
SELECT
테이블별칭.조회할칼럼,
테이블별칭.조회할칼럼
FROM 기준테이블 별칭
LEFT OUTER JOIN 조인테이블 별칭 ON 기준테이블별칭.기준키 = 조인테이블별칭.기준키...

--예제--
SELECT
A.NAME, --A테이블의 NAME조회
B.AGE --B테이블의 AGE조회
FROM EX_TABLE A
LEFT OUTER JOIN JOIN_TABLE B ON A.NO_EMP = B.NO_EMP AND A.DEPT = B.DEPT	
```





<div id=4>
    <h2>
        4. RIGHT OUTER JOIN 
    </h2>
</div>

LEFT OUTER JOIN의 반대.

오른쪽 테이블을 기준으로 JOIN.

그럼 결과값은 B테이블의 모든 데이터와 A테이블과 B테이블의 중복되는 값이 검색.

```mysql
--문법--
SELECT
테이블별칭.조회할칼럼,
테이블별칭.조회할칼럼
FROM 기준테이블 별칭
RIGHT OUTER JOIN 조인테이블 별칭 ON 기준테이블별칭.기준키 = 조인테이블별칭.기준키...

--예제--
SELECT
A.NAME, --A테이블의 NAME조회
B.AGE --B테이블의 AGE조회
FROM EX_TABLE A
RIGHT OUTER JOIN JOIN_TABLE B ON A.NO_EMP = B.NO_EMP AND A.DEPT = B.DEPT
```





<div id=5>
    <h2>
        5. FULL OUTER JOIN 
    </h2>
</div>

합집합 개념.

A테이블이 가지고 있는 데이터 , B테이블이 가지고 있는 데이터 모두 검색됩니다.

사실상 기준테이블의 의미가 없음.

```mysql
--문법--
SELECT
테이블별칭.조회할칼럼,
테이블별칭.조회할칼럼
FROM 기준테이블 별칭
FULL OUTER JOIN 조인테이블 별칭 ON 기준테이블별칭.기준키 = 조인테이블별칭.기준키...

--예제--
SELECT
A.NAME, --A테이블의 NAME조회
B.AGE --B테이블의 AGE조회
FROM EX_TABLE A
FULL OUTER JOIN JOIN_TABLE B ON A.NO_EMP = B.NO_EMP AND A.DEPT = B.DEPT
```





<div id=6>
    <h2>
        6. CROSS JOIN 
    </h2>
</div>

크로스 조인은 모든 경우의 수를 전부 표현해주는 방식.

기준 테이블이 A일 경우 A의 데이터 한 ROW를 B테이블 전체와 JOIN 하는 방식.

그러니 결과값도 N * M.

```mysql
--문법(첫번째방식)--
SELECT
테이블별칭.조회할칼럼,
테이블별칭.조회할칼럼
FROM 기준테이블 별칭
CROSS JOIN 조인테이블 별칭

--예제(첫번째방식)--
SELECT
A.NAME, --A테이블의 NAME조회
B.AGE --B테이블의 AGE조회
FROM EX_TABLE A
CROSS JOIN JOIN_TABLE B
======================================================================

--문법(두번째방식)--
SELECT
테이블별칭.조회할칼럼,
테이블별칭.조회할칼럼
FROM 기준테이블 별칭,조인테이블 별칭

--예제(두번째방식)--
SELECT
A.NAME, --A테이블의 NAME조회
B.AGE --B테이블의 AGE조회
FROM EX_TABLE A,JOIN_TABLE B
```





<div id=7>
    <h2>
        7. SELF JOIN
    </h2>
</div>

셀프 조인은 자기자신과 자기 자신을 조인한다는 의미.

하나의 테이블을 여러번 복사해서 조인.

자신이 가지고 있는 칼럼을 다양하게 변형시켜 활용할 경우에 자주 사용.

```mysql
--문법--
SELECT
테이블별칭.조회할칼럼,
테이블별칭.조회할칼럼
FROM 테이블 별칭,테이블 별칭2

--예제--
SELECT
A.NAME, --A테이블의 NAME조회
B.AGE --B테이블의 AGE조회
FROM EX_TABLE A,EX_TABLE B
```





<div id=8>
    <h2>
        참조
    </h2>
</div>

예제 및 wiki https://ko.wikipedia.org/wiki/Join_(SQL)

예시 간단 설명 https://pearlluck.tistory.com/46

코드 예시 https://coding-factory.tistory.com/87

상세 설명 https://docs.microsoft.com/ko-kr/sql/relational-databases/performance/joins?view=sql-server-ver15
