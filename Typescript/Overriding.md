# Overriding이란?

typescript의 `overloading`의 개념을 공부하고 난 뒤 `overloading`과 `overriding`의 용어 개념의 혼동이 생겨 `overriding`개념을 정리하게 되었다.

 <br><hr>

 ## Overriding

 `overriding`은 부모 클래스에 정의된 메서드를 자식 클래스에서 새로 구현하는 것을 일컫는 개념이다. 
 
 이 때 overriding할 대상이 있는 부모 클래스를 `overriden class`라고 하는데, overriden class에는 overridden method가 존재한다. overridden method는 파생 클래스에 정의된 메서드에 overriding돼서 overridden method로 새롭게 재정의된다. 

overriding으로 method가 재정의되려면 기본적으로 overridden method와 overriding method는 서로 이름이 같아야 한다. 그리고 overriding을 위해 다음 두 조건을 만족해야 한다.

1. overridden method의 매개변수 타입은 overriding method의 매개변수 타입과 같거나 상위 타입이어야 한다.
2. overriden method의 매개변수 개수가 overriding method의 매개변수 개수와 같거나 많아야 한다. (단, 조건 1이 성립된다는 전제가 있어야 함)

```
class Car {
    constructor() { }
    drive(kmDistance = 0, kmSpeed = 0) {
        console.log(`자동차가 ${kmDistance}km를 ${kmSpeed}km의 속도로 주행했습니다.`);
    }
}

class BMW extends Car {
    constructor() {
        super();
    }

    drive(kmDistance2 = 0) {
        console.log(`BMW가 ${kmDistance2}km를 주행했습니다.`);
    }
}

const car = new Car();
car.drive(1000, 100);

const bmw = new BMW();
bmw.drive();
bmw.drive(1000);
```

위의 코드는 조건 1과 조건 2를 모두 만족하는 예제 코드이다. drive 메서드의 이름은 같지만, Car클래스의 drive 메서드는 overriden method이고, Car를 상속받은 BMW 클래스의 drive 메서드는 overriding 메서드이다. 이 떄 overriding method는 overriden method보다 매개변수의 수는 적지만 타입이 같다.