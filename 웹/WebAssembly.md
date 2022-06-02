# 웹 어셈블리(WebAssembly)

- 자바스크립트가 아닌 다른 언어로 작성된 코드를 브라우저에서 실행시키기 위한 방법
- 주로 C/C++, Rust 등을 컴파일(AssemblyScript, C#, F#, Go, Kotlin, Swift, D, Pascal, Zig, Grain) 혹은 직접 작성
- Javascript 보다 빠름, Native 보다 느림
- Javascript를 대체하는 것이 아닌 상호 보완하는 관계(WebAssembly의 성능, Javascript의 편리성)

![img](https://d2.naver.com/content/images/2020/09/0a7056be-7346-1961-8173-eacc3e5076ca.png)



## Native 언어를 브라우저에서 실행하는 시도

- NaCl(Native Client)
  - 브라우저에서 C/C++ 코드를 실행하기 위한 샌드박스
  - 구글

- asm.js
  - Javascript의 subset
  - 네이티브 컴파일보다 2배 느림
  - 모질라



## 번역 방식

- Assembly
  - IR(Intermediate Representation, 중간 표현 형식)

![03-07-langs09-500x306.png](https://dongwoodotblog.files.wordpress.com/2017/06/03-07-langs09-500x306.png?w=1100)

- WebAssembly
  - 웹 어셈블리는 물리적인 기계가 아닌 개념상의 기계를 위한 언어
  - LLVM(Low Level Virtual Machine)이라는 toolchain 이용하여 변환

![04-02-langs08-500x326.png](https://dongwoodotblog.files.wordpress.com/2017/06/04-02-langs08-500x326.png?w=1100)

![04-03-toolchain07-500x411.png](https://dongwoodotblog.files.wordpress.com/2017/06/04-03-toolchain07-500x411.png?w=1100)



## 성능 변화

![A graph showing another performance spike in 2017 with a question mark next to it](https://2r4s9p1yi1fa2jd7j43zph8r-wpengine.netdna-ssl.com/files/2017/02/01-02-perf_graph10-500x412.png)

- Javascript 의 탄생(1995)
- JIT(just-in-time compiler)의 등장(2008)
  - 성능 10배 향상
  - Node.js의 등장
- WebAssembly의 등장(2017)

> JIT란?
>
> 인터프리터의 비효율성을 보완하기 위해 등장
>
> 코드가 실행되는 것을 관찰하여 자주 실행되는 코드가 최적화될 수 있도록 전송하여 Javascript를 더 빠르게 실행
>
> 역최적화, 메모리 오버헤드 증가



### 초기 자바스크립트

![05-02-diagram_past01-500x147.png](https://dongwoodotblog.files.wordpress.com/2017/06/05-02-diagram_past01-500x147.png?w=1100)

- Parsing(구문 해석) - 소스 코드를 인터프리터가 실행할 수 있는 형태로 가공
- Execute(실행)
- Garbage Collection



### JIT 등장 이후

![05-01-diagram_now01-500x129.png](https://dongwoodotblog.files.wordpress.com/2017/06/05-01-diagram_now01-500x129.png?w=1100)

- Compile + Optimize
- Re-optimize(재최적화) - 다시 최적화를 하거나, 역최적화
- 순서대로 진행되는 것이 아닌, 부분적으로 진행



### 웹 어셈블리

![05-03-diagram_future01-500x214.png](https://dongwoodotblog.files.wordpress.com/2017/06/05-03-diagram_future01-500x214.png?w=1100)

- Fetching(가져오기) - 서버에서 파일을 가져옴
- Parsing - 이미 IR이므로 변환 과정이 없음, 에러만 검증
- Compile + Optimize - LLVM 에서 이미 최적화가 많이 진행 됨
- Re-Optimizing - 재최적화는 JIT에 의한 것이므로, WebAssembly에서는 필요 없음
- Execute - WebAssembly는 기계에게 더 이상적인 명령셋을 제공(최대 800%까지 더 빠름)
- Garbage Collection - 수동으로 메모리 관리하여 성능 향상



### 결론

- 코드가 간결하여, 네트워크적 이점
- 웹 어셈블리 해독 시간이 자바스크립트 구문 해석 시간보다 적음
- 기계어에 가까우며, 이미 어느정도 최적화가 되어있음
- 자바스크립트 엔진이 실행시점에서 분석할 필요가 없음
- 기계에 적합한 명령셋을 가지므로 실행 시간이 대부분의 상황에서 적음
- 메모리를 직접 관리



## 그래서 성능은?

### WebAssembly vs Javascript

![img](https://tech.kakao.com/wp-content/uploads/2022/01/Img-7.png)

- canvas를 통한 이미지 필터링에서 웹어셈블리가 자바스크립트에 비해 약 2~3배 빠름



### WebAssembly vs Native Code

![그림 4](https://d2.naver.com/content/images/2019/06/helloworld-201904-jaesung-park_2-04.png)

- 평균적으로 Firefox에서는 45%, Chrome에서는 55% 느리게 실행



## References

- A cartoon intro to WebAssembly - https://hacks.mozilla.org/2017/02/a-cartoon-intro-to-webassembl

- FE개발자의 성장 스토리 08 : WebAssembly 개발기 - https://tech.kakao.com/2021/05/17/frontend-growth-08/
- 2019년과 이후 JavaScript의 동향 - WebAssembly - https://d2.naver.com/helloworld/8786166
- 2020년과 이후 JavaScript의 동향 - WebAssembly - https://d2.naver.com/helloworld/8257914
- 
