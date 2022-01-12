<div align="center">
  <br />
  <h1>DB 제약 조건</h1>
  <br />
</div>



## 목차

1. [**제약 조건**](#1)
2. [**Not Null**](#2)
3. [**UNIQUE**](#3)
4. [**Primary Key**](#4)
5. [**FOREIGN KEY**](#5)
6. [**CHECK**](#6)
7. [**DEFAULT**](#7)
8. [**참조**](#8)





<div id="1"></div>

## 1. 제약 조건

### 테이블

- 데이터베이스의 기본적인 데이터 저장 단위.
- 테이블은 사용자가 접근 가능한 모든 데이터를 보유함. 레코드& 컬럼으로 구성.
- 시스템 내에서 독립적으로 사용되길 원하는 엔티티를 표현
  ex) 회사에서의 고용자, 제품에 대한 주문
- 두 엔티티 간의 관계를 표현
  ex) 회사에서의 고용자 & 그들의 숙련도 / 제품 & 주문의 관계



### 생성 시 주의할 점

- 테이블 이름 & 컬럼명 : 항상 **알파벳 문자로 시작**. 0-9, A-Z, $, #, _ 사용 가능.
- 컬럼 이름은 **30자** 초과 불가능, **예약어** 사용 불가능
- 한 테이블 안에서 컬럼 이름은 같을 수 없으며, 다른 테이블과의 컬럼 이름은 같을 수 있음.



### 제약 조건이란?
=> 테이블에 부적절한 자료가 입력되는 것을 방지하기 위해서 여러가지 규칙을 적용해 놓는 것.
간단하게 말하면 테이블 안에서 **데이터의 성격을 정의하는 것.**

- 제약 조건은 **데이터의 무결성 유지**를 위해서 사용자가 지정할 수 있는 성질
- 모든 제약 조건은 데이터 사전(Data Dictionary) 에 저장
- 의미 있는 이름을 부여했다면 CONSTRAINT 를 쉽게 참조할 수 있다.
- 제약 조건은 테이블 생성 당시 지정할 수도 있고, 테이블 생성 후 구조 변경(ALTER) 명령어를 통해서도 추가 가능하다.
- NOT NULL 제약 조건은 반드시 컬럼 레벨에서만 정의 가능하다.



<div id="2"></div>

## 2. Not Null

컬럼 생성 시 지정하지 않으면 defaul t로 Null이 허용 가능하게 되어 있습니다. 

따라서 해당 컬럼값을 입력하지 않고 튜플을 삽입 시 Null이 들어가게 되는데 이를 방지하기 위해서는 Not Null을 기술해 주면 됩니다.

- 컬럼을 **필수 필드화** 시킬 때 사용.
- NOT NULL 제약 조건 설정 시 해당 컬럼에는 꼭 데이터를 입력해야 함.

```sql
-- emp3라는 테이블을 만들고, ename 컬럼의 제약조건명을 emp_nm_ename 으로 하여 NOT NULL 제약조건을 설정하자.
CREATE TABLE emp3(
	ename VARCHAR2(30) CONSTRAINT emp_nm_enmae NOT NULL
);

VALUE1 VARCHAR2(10) NOT NULL;
```



<div id="3"></div>

## 3. UNIQUE

중복된 값을 허용하지 않는다. 즉, 유일한 데이터를 갖는다.(NULL은 허용)

- 데이터의 유일성을 보장(=> 중복되는 데이터가 존재할 수 없음)하고, 자동으로 인덱스가 생성.
- unique은 **null허용**하지만, primary key는 null허용 안함
- unique은 **하나의 테이블에 여러개** 올 수 있지만, primary key는 하나만 존재

```sql
-- EMP2 테이블을 생성한 뒤, ALTER 를 이용해서 제약조건을 추가해준다. (제약조건명 : EMP2_UK_DEPTNO)
ALTER TABLE EMP2
ADD CONSTRAINT EMP2_UK_DEPTNO UNIQUE(deptno);

VALUE2 VARCHAR2(10) UNIQUE;
```





<div id="4"></div>

## 4. Primary Key

기본키

기본키란 해당 테이블을 대표하는 컬럼으로 Primary key 로 지정된 컬럼은 Null값을 가지지 못하며, 중복된 값을 가질 수 없습니다.

**NULL을 허용하지 않고 중복된 데이터를 허용하지 않는다**.(**NOT NULL + UNIQUE**가 PRIMARY KEY 이다.) 

따라서 **데이터의** **특정 조건을** **검색하거나 수정 등의 작업을** **할 때** **기본 키로** **구분**한다.(ID, 주민등록 번호, 회원 번호, 글 번호 등이 기본 키에 해당된다.) 주로 테이블에 1개의 기본 키를 갖는다.

- 기본키 : **UNIQUE + NOT NULL 의 결합**과 같음.
- 기본키는 그 데이터 행을 대표하는 컬럼으로서의 역할을 수행하여 다른 테이블에서 외래키들이 참조할 수 있는 키로서의 자격을 가지고 있다. => 참조 무결성
- UNIQUE 제약조건과 마찬가지로 기본키를 정의하면 자동으로 인덱스를 생성, 그 이름은 기본 키 제약조건의 이름과 같다.

```sql
-- PRIMARY KEY 생성 예제. 제약조건명 EMP5_PK_EMPNO
CREATE TABLE EMP5(
    empno NUMBER CONSTRAINT EMP5_PK_EMPNO PRIMARY KEY
);

VALUE3 VARCHAR2(10) PRIMARY KEY;
```



<div id="5"></div>

## 5. FOREIGN KEY

외래키를 의미하는 제약조건

외래키는 참조 무결성을 위해 사용되는데 이 외래키로 지정된 컬럼은 반드시 다른 테이블의 "Primary key(기본키)"와 참조 관계를 가지게 되고 

~~외래키로 지정된 컬럼은 참조관계를 가진 테이블의 기본키에 있는 값만을 가질 수 있습니다.~~

즉, Null 값은 허용하되, 참조하고 있는 테이블의 ~~기본키에~~ 있는 값만 입력될 수 있습니다. 

참조하는 테이블 칼럼의 데이터만을 허용한다. 참조하는 테이블은 PRIMARY KEY나 UNIQUE로 지정된 칼럼만을 FOREIGN KEY로 지정할 수 있다.

- 기본키를 참조하는 컬럼 or 컬럼들의 집합 (외래키는 **기본키나 유니크가 아니면 생성 제약**)
- 외래키를 가지는 컬럼의 데이터 형은 외래키가 참조하는 기본키의 컬럼과 데이터 형이 일치해야 한다. 
  (이를 어기면 **참조 무결성 제약**에 의해 **테이블을 생성할 수 없음 !**)
- 외래키에 의해 참조되고 있는 기본키 : **삭제 불가 !!**
- **on update cascade**하면 **기본키가 수정될 경우 외래키도 같이 수정해준다는 말**
- **ON DELETE CASCADE** 연산자와 함께 정의된 외래키의 데이터는 **그 기본키가 삭제될 때 같이 삭제된다**

```sql
-- emp2 테이블의 deptno 컬럼이 dept 테이블의 deptno 컬럼을 참조하도록 외래키를 생성하자.
ALTER TABLE EMP2 ADD CONSTRAINT emp2_fk_deptno
FOREIGN KEY (deptno) REFERENCES TO DEPT(deptno);

VALUE4 VARCHAR2(10) REFERENCES 참조할_테이블(참조할_테이블의_PRIMARY_KEY);
```





<div id="6"></div>

## 6. CHECK

Mysql enum 데이터 타입과 비슷한 효과를 내주는 거로서, 입력될 수 있는 데이터의 종류를 제한할 수 있습니다.

**데이터의 값의 범위나 조건을 설정**하여 **조건에 해당되는 데이터만 허용**

- 컬럼의 값을 어떤 **특정 범위로 제한**

```sql
-- EMP2 테이블의 comm 컬럼이 1~100 까지의 값만 가질 수 있도록 체크 제약조건 생성.
ALTER TABLE EMP2
ADD CONSTRAINT EMP2_CK_COMM CHECK (comm >= 1 AND comm <= 100);

VALUE5 VARCHAR2(10) CHECK(VALUE5 BETWEEN 1 AND 10);
VALUE6 VARCHAR2(10) CHECK(VALUE6 IN ('A', 'B'));
```





<div id="7"></div>

## 7. DEFAULT

**아무런 데이터를 입력하지 않았을 경우 지정한 데이터가 자동으로 입력**

NULL 값이 들어올 시 지정된 값을 삽입함

- 데이터를 입력하지 않아도 지정된 값이 **기본으로 입력**된다.
- default라고 값을 명시하면 기본값이 들어감
- 열이름이 명시되지 않으면 자동 기본값
- 값이 직접 명기되면 기본값은 무시됨.

```sql
-- hiredate 컬럼에 값을 입력하지 않아도 오늘 날짜가 입력된다.
SQL> CREATE TABLE emp4(
     ... (컬럼생략) ...,
     hiredate DATE DEFAULT SYSDATE );
     
VALUE7 VARCHAR2(10) DEFAULT '홍길동';
```





<div id="8"></div>

## 8. 참조

간단 설명 및 예시

https://blog.naver.com/PostView.nhn?blogId=heartflow89&logNo=220984804599&redirect=Dlog&widgetTypeCall=true&directAccess=false



깔끔 설명 및 예시

https://inpa.tistory.com/387



간단 설명

https://wakestand.tistory.com/83



상세 예시

https://dog-developers.tistory.com/87