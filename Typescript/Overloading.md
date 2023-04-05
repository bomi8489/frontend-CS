# Overloading이란?

typescript의 call signature 개념을 공부하다가 overloading이라는 개념을 접하게 되었고, Java를 공부했을 때 제대로 학습해 두지 않아서 다시 한번 개념 정리를 하게 되었다.

<hr>

## overloading의 의미

기본적으로 타입스크립트에서 오버로딩은 함수가 서로 다른 여러개의 call signature를 가지고 있을 때 발생시킨다.

> typescript에서의 오버로딩의 개념은 C, C++, Java 등 여타 다른 언어들과의 오버로딩의 개념과 크게 다르지 않다.

<br><hr>

## 예시

typescript의 overloading에는 두가지 예시가 있다.

- 매개변수의 개수는 동일하지만, 타입이 다른 경우

```
type Add = {
    (a: number, b: number): number
    (a: number, b: string): number
}

const add: Add = (a, b) => {
    return (typeof b === "string") ? a : a + b
}

console.log(add(1, 2))  // 3
console.log(add(1, "2"))    // 1
```

- 타입은 동일하지만 매개변수의 개수가 다른 경우

```
type Add = {
    (a: number, b: number): number
    (a: number, b: number, c: number): number
}

// 매개변수 'c?'의 의미는 optional property
const add: Add = (a, b, c?: number) => {
    return c ? a + b + c : a + b
}

console.log(add(1, 2)); // 3
console.log(add(1, 2, 3));  // 6
```