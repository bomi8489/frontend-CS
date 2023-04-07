# Polymorphism

`Polymorphism`은 여러가지 구조물이라는 의미로 typescript에서는 다형성이라는 의미를 지니고 있다.

Typescript에서의 Polymorphism은 기본적으로 함수는 여러가지 다른 모양, 다른 형태를 가지고 있으며, `overloading`처럼 다른 2~3 개의 파라미터을 가질 수 있다. 또는, Typescript에서의 함수는 string이나 object를 첫 번째 파라미터로 가질 수 있다.

<br><hr><br>

다음 코드는 각각 number array와 boolean array를 함수의 파라미터로 받고 리턴값이 없는 함수의 call signature를 선언한 후 array의 item을 출력하도록 구현한 코드이다.

```
// call signature
type SuperPrint = {
	(arr: number[]): void
    (arr: boolean[]): void
}

// 함수 구현
const superPrint: SuperPrint = (arr) => {
	arr.forEach((item) => console.log(item))
}

// 함수 실행
superPrint([1, 2, 3, 4])
superPrint([true, true, false, false])
superPrint(["1", "2", "3", "4"]) // 에러
superPrint([1, true, "2", 4]) // 에러
```


call signature 선언 구문에서 string array타입에 대해 선언하지 않았기 때문에 함수 실행 코드에서 string array를 출력하려고하면 에러가 발생한다. 이 경우 마다 call signature에 타입 선언을 해주어야 할까?

이 경우 우리는 `generic type`을 이용하여 이런 불편함을 해결할 수 있다.

<hr>

## Generic type

<br>

다음 코드는 call signature 선언 구문에서 number[]나 string[] 등 직접적으로 타입을 명시해주는 `concrete type`을 대신해서 타입을 추론할 수 있는 generic type을 사용한 코드이다.

즉 call signature를 선언할 때, 어떤 타입이 들어올지 확실하게 모를 때 generic type을 사용한다.

```
// call signature
type SuperPrint = {
	<TypePlaceHolder>(arr: TypePlaceHolder[]): void
}

// 함수 구현
const superPrint: SuperPrint = (arr) => {
	arr.forEach((item) => console.log(item))
}

// 함수 실행
superPrint([1, 2, 3, 4])
superPrint([true, true, false, false])
superPrint(["1", "2", "3", "4"]) 
superPrint([1, true, "2", 4])
```

typescript의 `다형성(polymorphism)`은 함수의 call signature를 입력할 때 placeholder를 제공한 셈인 것이다.


<br><hr><br>

## Any vs Generic

generic의 정확한 의미를 모르고 사용하다가는 any와 크게 다를바 없다고 혼동할 수도 있다.

다음 코드는 call signature에서 함수의 파라미터와 리턴값을 any 타입으로 선언하고 배열의 첫 번째 요소를 대문자로 변경하는 코드이다. 그런데 배열의 첫 번째 요소는 number type인데도 불구하고 코드는 에러를 표시하지않고 실행하게 된 후에야 결국 타입에러를 발생시킨다.

```
type SuperPrint = {
	(arr: any[]): any
}

const superPrint: SuperPrint = (arr) => arr[0]

let a = superPrint([1, "b", true]);

a.toUpperCase(); // no error
```

다음 코드는 generic type을 사용하여 구현을 한 것이다. any타입으로 선언한 코드랑은 다르게 컴파일을 하기 전 에러를 발생시켜 타입스크립트의 보호를 받을 수 있다.

```
type SuperPrint = {
    <T>(arr: T[]): T
}

const superPrint: SuperPrint = (arr) => arr[0]

let a = superPrint([1, "b", true]);

a.toUpperCase(); // error
```

any type을 사용한다는 것은 typescript의 보호를 받지않는다는 것으로 typescript를 사용하는 의미가 퇴색되게 되므로 any type을 사용하는것은 지양하는것이 좋다.