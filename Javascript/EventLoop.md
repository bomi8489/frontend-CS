# Event Loop

## :clap: :clap:

프로그래머스 데브코스 프론트엔드 과정을 이수하던 중 Event Loop의 동작 과정에 대해 접하게 되었다. 상당히 예전에 Javascript를 처음 공부하던 당시에 접했던 키워드라 기억이 가물가물해서 이번 기회에 다시 한번 정리해보기로 했다.

Event Loop가 Javascript 엔진에 포함되어 있다고 착각하는 경우가 종종 있다고들 하는데, 사실은 그렇지가 않다. Event Loop는 Javascript 엔진에 포함되어 있지않고, 브라우저나 Node.js에서 자체적으로 관리하고 있다.

WebAPI는 브라우저에서 제공하는 API이고, 클릭과 같은 DOM event, 네트워크 호출 혹은 Timer 등을 실행시킬 경우 브라우저에 위임되는데, 보통 이런 WebAPI들은 Callback 함수를 넘기기 마련이다. 이 Callbcak 함수는 비동기 작업이 끝나면 Task Queue에 넣어지고 순차적으로 꺼내서 Javascript 엔진의 Call Stack에 push 된다.

:eyes: 그렇다면 Event Loop의 동작과정을 예시 코드를 보면서 따라가 보자

```
function foo() {
	console.log("foo");
}

function bar() {
    console.log("bar");
}

setTimeout(function a() {
    bar();
}), 1000;

foo();

setTimeout(function b() {
	console.log("baz");
}, 1000);
```

1. Event Loop는 일단 Javascript가 실행되면 전역 스코프에서 실행된다.

2. 코드가 진행되면서 첫 번째 setTimeout 함수가 실행되면 Call Stack에 함수가 쌓임과 동시에 브라우저 내부적으로 webAPI가 실행된다. setTimeout은 별다른 로직이 없기에 종료되면서 Call Stack에서 빠져나온다.

3. 그 후 foo 함수가 실행되면서 Call Stack에 쌓이고, 내부의 console.log가 실행되면서 역시 스택에 쌓인다. 출력이 되고 함수가 종료되면 console.log 와 foo 가 각각 스택에서 빠져나온다.

4. 마지막 setTimeout 함수가 실행되면 스택에 쌓이고 webAPI가 실행된다. setTimeout이 종료되고 스크립트가 종료되면 Call Stack은 비어있는 상태가 된다.

5. 한 편, webAPI에서 실행되고 있던 setTimeout 함수가 1초가 지나 첫 번째와 두 번째 setTimeout 함수의 콜백함수가 Task Queue에 들어가게 되고, Call Stack이 비어있는것이 확인되면 Queue에 들어간 순대로 Call Stack에 쌓이게된다.

6. 마지막 setTimeout 콜백 함수까지 Call Stack에 쌓이고 종료되고 나면 끝이난다.

<br><hr>

사실 이렇게 글로 설명을 하면 이해하기가 쉽지가 않다.

아래의 사이트는 Call Stack, WebApi 그리고 Task Queue의 동작 과정을 시각적으로 간단히 볼 수 있는 테스트 사이트이다. 원활한 이해를 위해서 예시코드를 한번 실행시켜 보면 이해가 빠르게 될 것이다.

http://latentflip.com/loupe/?code=ZnVuY3Rpb24gZm9vKCkgew0KCWNvbnNvbGUubG9nKCJmb28iKTsNCn0NCg0KZnVuY3Rpb24gYmFyKCkgew0KICAgIGNvbnNvbGUubG9nKCJiYXIiKTsNCn0NCg0Kc2V0VGltZW91dChmdW5jdGlvbiBhKCkgew0KICAgIGJhcigpOw0KfSksIDEwMDA7DQoNCmZvbygpOw0KDQpzZXRUaW1lb3V0KGZ1bmN0aW9uIGIoKSB7DQoJY29uc29sZS5sb2coImJheiIpOw0KfSwgMTAwMCk7!!!PGJ1dHRvbj5DbGljayBtZSE8L2J1dHRvbj4%3D
