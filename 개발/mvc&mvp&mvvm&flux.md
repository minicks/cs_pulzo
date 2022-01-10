# 앱 디자인패턴

## 목차

1. [MVC](#MVC)
2. [MTV](#MTV)
3. [MVP](#MVP)
4. [MVVM](#MVVM)
5. [FLUX](#FLUX)
6. [MVI](#MVI)
7. [레퍼런스](#레퍼런스)

## MVC

프로그램을 각각의 역할에 따라 Model, View, Controller로 나누어 설계한 아키텍처 패턴

가장 유명하고 많이 쓰인다

### 구조도

![MVC](https://t1.daumcdn.net/thumb/R1280x0/?fname=http://t1.daumcdn.net/brunch/service/user/1OLd/image/66QY6--aek5zaAuLAsHFWgXwwG0.png)

### 특징

- Controller는 여러개의 View를 선택할 수 있는 1:n 구조
- Controller는 View를 선택할 뿐 직접 업데이트 하지 않습니다. (View는 Controller를 알지 못합니다.)

### 구성요소

#### Model

DB 모델링을 의미한다. 데이터의 타입과 종류를 결정하여, 데이터 정리를 담당한다.

#### View

client가 요청한 결과물을 정리하여 해당 HTML에 렌더링 하는 역할이다. 본질적인 client와 server간의 interface라고 할 수 있다.

#### Controller

client가 요청한 View와 Model을 연결하는 역할이다. client가 어떤 URL을 요청하는지, 어떤 DB를 요청하는지를 확인하여 적절한 연결점을 찾아준다.

### 장점

- 가장 단순한 패턴

### 단점

- View와 Model 사이의 의존성이 높아서 어플리케이션이 커질 수록 복잡해지고 유지보수가 어렵다

## MTV

Python의 Django 프레임워크에서 사용하는 디자인패턴이며, MVC 패턴의 Django 버전이다

Model ⇒ Model

View ⇒ Template

Controller ⇒ View

### 구조도

![MTV](https://media.vlpt.us/images/inyong_pang/post/fb63ce19-c0b9-4dce-90d6-73ba209d857b/image.png)

### 특징

- Django 에서 자체적으로 ORM(Object-Relational Mapping)을 제공

> ORM이란?
>
> Object-Relational Mapping의 약자로, SQL이라는 언어 대신 데이터베이스를 쉽게 연결해주는 방법.

### 구성요소

#### Model

Django에서의 DB 모델링

#### Template

client에게 반환되는 HTML을 Django의 template 시스템 문법에 맞게 렌더링

#### View

웹 요청을 받고 응답을 반환

#### URL conf

client로부터 요청을 받으면 Django는 가장 먼저 요청에 들어있는 URL을 분석하고, 파일에 정의된 URL 패턴과 매칭되는지 분석 후, 해당 매칭되는 View를 호출

## MVP

MVC에서 파생된, Model과 View 간의 의존성이 없는 아키텍처 패턴

Model과 View는 MVC 패턴과 동일하고, Controller 대신 Presenter가 존재

### 구조도

![MVP](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcwKHJS%2Fbtq2HHLdPd6%2FPBIDw0IrUS2KXcaHvY7kNk%2Fimg.png)

### 특징

- Presenter가 M-V 사이에서 관리를 해주기 때문에, MVC 패턴과 달리 M-V 사이에 의존성이 없다
- 하지만 앱이 커지고 복잡해질 수록 V-P간에 의존성이 강해지는 문제점이 발생
- Presenter와 View는 1:1 관계

### 구성요소

#### Model

어플리케이션에서 사용되는 데이터와 그 데이터를 처리하는 부분

#### View

사용자에서 보여지는 UI 부분

#### Presenter

View에서 요청한 정보로 Model을 가공하여 View에 전달해 주는 부분이며 View와 Model을 붙여주는 접착제 역할

### 장점

- Model과 View 사이에 의존성이 없다.

### 단점

- View와 Presenter가 1:1 관계이기 때문에 서로 간의 의존성이 커짐
- 구현에 있어서 필요한 클래스의 수가 많아집니다.

## MVVM

MVP에서 개선한 아이디어이며, Model과 View 간의 의존성뿐만 아니라 Controller와 View 간의 의존성도 고려하여 각 구성 요소가 독립적으로 작성되고 테스트될 수 있도록 설계된 아키텍처 패턴

### 구조도

![MVVM](https://t1.daumcdn.net/thumb/R1280x0/?fname=http://t1.daumcdn.net/brunch/service/user/1OLd/image/0biW4YNB0bAVV4zzOuNBsdV0Fz8.png)

### 특징

- View에 Action이 들어오면, Command 패턴으로 View Model에 Action을 전달
- ViewModel은 View를 참조하지 않기 때문에 독립적
- ViewModel과 View는 1:n 관계
- View는 자신이 이용할 ViewModel을 선택해 바인딩하여 업데이트를 받음
- Model이 변경되면 해당하는 ViewModel을 이용하는 View가 자동으로 업데이트
- ViewModel은 View를 나타내 주기 위한 Model이자, View의 Presentation Logic을 처리

### 구성요소

#### Model

어플리케이션에서 사용되는 데이터와 그 데이터를 처리하는 부분

#### View

사용자에서 보여지는 UI 부분

#### ViewModel

View를 표현하기 위해 만든 View를 위한 Model이며, View를 나타내 주기 위한 Model이자 View를 나타내기 위한 데이터 처리를 하는 부분

### 장점

- Model과 View사이의 의존성이 없다
- ViewModel과 View사이의 의존성이 없다
- 중복되는 코드를 모듈화 할 수 있다

### 단점

- ViewModel의 설계가 어렵다

## FLUX

어디서 어느 방향으로 데이터가 전달될지 알지 못할 정도로 혼란한 MVC 패턴의 복잡성을 해소하기 위해 데이터가 한 방향으로만 흐르게 하는 패턴

![FLUX](https://miro.medium.com/max/700/1*pgxTL69KXTYjupzGO015Ew.png)

### 특징

- MVC의 문제를 해결할 목적으로 고안한 애플리케이션 아키텍쳐
- 단방향 데이터 흐름(unidirectional data flow)
- 디스패처(Dispatcher), 스토어(Store), 뷰(View) 등 세 부분으로 구성
- 뷰는 단순히 화면에 보여지는 것을 넘어 자식 뷰로 전달도 하는 컨트롤 역할도 병행, 따라서 컨트롤러 뷰 라고 불림

### 구성요소

#### Dispatcher

모든 데이터 흐름을 관리하며 분배해주는 역할

#### Store

모든 상태와 로직을 담고 있다. Dispatcher에 콜백함수로 등록하여 액션이 호출되면 실행된다. 상태가 변경되면 View에 알려준다.

#### Action

Store 업데이트는 Dispatcher에서 콜백함수로 이뤄지는데 이때 파라미터로 들어가는 객체

#### View or Controller View

Flux에서의 View는 컨트롤러의 성격또한 가지고 있다. 최상위 View는 자식들에게 Store를 내려보내주는 역할

### 장점

데이터 흐름이 한 방향으로 강제되기 때문에, 양방향 흐름으로 인한 혼선을 줄일 수 있고, 모든 상태가 스토어에 있음으로 변경 사항을 여러 컴포넌트에 전달하기 쉬움

### 단점

코드 복잡도 및 구현 난이도 증가

## MVI

자바스크립트 생태계에서 탄생했으며 MVC에서 파생된, 능동적인 Controller 대신 Intent라고 불리는 Reactive 요소를 이용한 아키텍처 패턴

### 구조도

![MVI](https://t1.daumcdn.net/thumb/R1280x0/?fname=http://t1.daumcdn.net/brunch/service/user/1OLd/image/JHTtx7AD-xlDJHdutxQBnUdnXQo.png)

### 특징

- Intent가 User를 관찰하고, Model이 Intent를 관찰하고, View가 Model을 관찰하고, User가 View를 관찰하는 Reactive 요소로 이루어져 있음
- 단방향 데이터 흐름과 불변성
- 리액티브 패러다임

### 구성요소

#### Model

모델은 상태를 나타냅니다. MVI의 모델은 아키텍쳐의 다른 레이어와의 단방향 데이터 흐름을 보장하기 위해 변경이 불가능

#### View

View를 나타내며 하나 이상의 Activity나 Fragment로 구현

#### Intent

사용자 또는 앱내 발생하는 Action을 나타낸다.

### 장점

- 단방향, 불변성 데이터를 이용해 예측 가능한 상태
- 서로 간 의존성 없음

### 단점

- RxJava와 같은 Observable 한 외부 라이브러리를 이용해야 함

## 레퍼런스

- https://sungjk.github.io/2016/10/03/Whatisflux.html
- https://jforj.tistory.com/147
- https://medium.com/@esung/mvc-%EC%A0%95%EB%A7%90%EC%A0%9C%EB%8C%80%EB%A1%9C%EC%95%8C%EA%B3%A0%EA%B3%84%EC%8B%A0%EA%B0%80%EC%9A%94-875f1323f6c0
- https://funncy.github.io/programming/2021/07/14/mvc-mvp-mvvm-flux/
- https://62che.com/blog/architecture/mvw-redux-viper-%EB%B9%84%EA%B5%90.html#redux-flux
- https://medium.com/@maryangmin/data-uni-directional-architecture-in-android-%EB%8D%B0%EC%9D%B4%ED%84%B0-%EB%8B%A8%EB%B0%A9%ED%96%A5-%EA%B5%AC%EC%A1%B0-fd7ef26e80fc
- https://medium.com/hcleedev/web-react-flux-%ED%8C%A8%ED%84%B4-88d6caa13b5b
- https://dogbirdfoot.tistory.com/14
- https://beomy.tistory.com/43
- https://brunch.co.kr/@oemilk/113
- https://medium.com/@kimdohun0104/mvi-%ED%8C%A8%ED%84%B4%EC%97%90-%EB%8C%80%ED%95%9C-%EA%B3%A0%EC%B0%B0-%EC%9D%B4%EC%9C%A0%EC%99%80-%EB%B0%A9%EB%B2%95-%EA%B7%B8%EB%A6%AC%EA%B3%A0-%ED%95%9C%EA%B3%84-767cc9973c98
- https://yoon-dailylife.tistory.com/117
- https://jaehochoe.medium.com/%EB%B2%88%EC%97%AD-%EC%95%88%EB%93%9C%EB%A1%9C%EC%9D%B4%EB%93%9C%EB%A5%BC-%EC%9C%84%ED%95%9C-mvi-model-view-intent-%EC%95%84%ED%82%A4%ED%85%8D%EC%B3%90-%ED%8A%9C%ED%86%A0%EB%A6%AC%EC%96%BC-%EC%8B%9C%EC%9E%91%ED%95%98%EA%B8%B0-165bda9dfbe7
- https://62che.com/blog/architecture/mvc-mvp-mvvm-%EB%B0%94%EB%A1%9C%EC%95%8C%EA%B8%B0.html#%E1%84%89%E1%85%A5%E1%84%83%E1%85%AE
