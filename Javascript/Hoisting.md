# Hosting

## Hoisting 이란?

> 함수 안에 있는 선언들을 모두 끌어올려서 해당 함수 유효 범위의 최상단에 선언하는 것

- 자바스크립트 함수는 실행되기 전에 함수 안에 필요한 변수값들을 모두 모아서 유효 범위의 최상단에 선언한다.
    - 자바스크립트 Parser가 함수 실행 전 해당 함수를 한 번 훑는다.
    - 함수 안에 존재하는 변수/함수선언에 대한 정보를 기억하고 있다가 실행시킨다.
    - 유효 범위: 함수 블록 {} 안에서 유효

- 즉, 함수 내에서 아래쪽에 존재하는 내용 중 필요한 값들을 끌어올리는 것이다.
    - 실제로 코드가 끌어올려지는 건 아니며, 자바스크립트 Parser 내부적으로 끌어올려서 처리하는 것이다.
    - 실제 메모리에서는 변화가 없다.

<br>

## Hoisting이 발생하는 대상

var 변수 선언과 함수선언문에서 발생

> 간단한 예제들을 통해 알아보자

- var 변수 선언으로 hoisting이 발생한 경우
    ```
    console.log(number);    // undefined
    var number = 1;
    console.log(number);    // 1
    ```

    1번줄의 number가 undefined가 나온 이유는 javascript parser가 변수의 선언만 최상단에 선언 했을뿐, 값을 할당을 최상단으로 둔것은 아니기에 변수의 선언인 `var number`만 최상단에 선언 되어서 undefined가 출력된 것이다.

    ```
    console.log(number);    // error
    let number = 2;
    ```

- 함수 선언문으로 hoisting이 발생한 경우

    > 함수 선언문이란? 

    ```
    function helloWorld() {
        console.log("hello world");
    }
    ```

    > 함수 표현식이란?

    javascript에서 함수는 값으로 취급 가능

    ```
    const helloWorld = () => {
        console.log("hello world");
    }
    ```

    > hoisting이 일어나는 경우

    ```
    helloWorld();   // "hello world"

    function helloWorld() {
        conosole.log("hello world");
    }
    ```

<br>

- Hoisting의 우선순위

    > 기본적으로 var 변수 선언이 함수 선언보다 우선순위가 높다

    실제 코드
    ```
    var sayHi = "hi";

    function sayHi() {
        console.log("hi");
    }
    function sayBye() {
        console.log("bye");
    }

    var sayBye = "bye";

    console.log(typeof sayHi);
    console.log(typeof sayBye);
    ```

    javascript parser가 읽어들이는 순서
    ```
    var sayHi; 
    var sayBye; 

    function sayHi() {
        console.log("hi");
    }
    function sayBye() {
        console.log("bye");
    }

    sayHi = "hi";
    sayBye = "bye";

    console.log(typeof sayHi); //   "string"
    console.log(typeof sayBye); //  "string"
    ```

<br>

- Hoisting 사용시 주의

    > 코드의 가독성과 유지보수를 위해 호이스팅이 일어나지 않도록 한다.
    - 호이스팅을 제대로 모르더라도 함수와 변수를 가급적 코드 상단부에서 선언하면, 호이스팅으로 인한 스코프 꼬임 현상은 방지할 수 있다.
    - 가급적 let/const를 사용

    > var를 쓰면 혼란스럽고 쓸모없는 코드가 생길 수 있다. 그럼 왜 var와 호이스팅을 이해해야 할까?
    - ES6를 어디에서든 쓸 수 있으려면 아직 시간이 더 필요하므로 ES5로 트랜스컴파일을 해야한다.
    - 따라서 아직은 var가 어떻게 동작하는지 이해하고 있어야 한다.