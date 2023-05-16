# CSS, SCSS, SASS

## CSS, SCSS, SASS란?

- CSS: Cascading Style Sheet (종속형 시트)
- SASS: Syntactically Awesome Style Sheets (문법적으로 멋진 CSS)
- SCSS: Sassy CSS (멋진 CSS)

<br>

## CSS의 단점

CSS는 복잡한 언어는 아니지만 작업이 크고 고도화 될수록 불편함이 생긴다.

예를들어 선택자(Selector)의 과용과 연산 기능의 한계, 구문(Statement)의 부재 등 프로젝트가 커지면 코드 중복이 많아지고 복잡해지어 유지보수가 어려워지게 된다.

반복문 조차도 문법을 지원하지 않아 비슷한 코드의 나열로 인해 가독성이 떨어지고 코드가 지저분하다.

- 요약

1. 선택자(Selector)을 만들때 매번 불필요한 부모요소 선택자를 적어야 한다.
2. 규모가 큰 프로제트의 경우 자동화하기 어렵고 모든 것을 수동으로 변경해야 한다.
3. 중복되는 코드가 많아 코드 줄수가 길어져 유지보수에 마이너스적인 요소가 된다.

<br>

## SASS의 등장

`SASS`는코드의 재활용성을 올리고, 가독성을 올리는 등 CSS에서 보이던 단점을 보완하고, 개발의 효율을 올리기 위해 등장한 `CSS 전처리기 언어`이다.

- CSS 전처리기(CSS Preprocessor) 언어란?
    - 전처리기 언어는 CSS 문법과 굉장히 유사하지만 선택자의 중첩(Nesting)이나 조건문, 반복문, 다양한 단위(Unit)의 연산 등… 표준 CSS 보다 훨씬 많은 기능을 사용해서 편리하게 작성할 수 있다.
    따라서 코드 작성에 드는 시간을 줄여주고, 코드를 유지 관리하는데 도움이 된다.

    - 전처리기 언어가 제공하는 문법을 기반으로 코드를 작성한 다음, 이를 컴파일해 CSS 파일을 빌드하는 것이 전처리기 언어를 통해 스타일시트를 생산하는 절차이다.

<br>

## SASS의 장점

1. CSS 보다 심플한 표기법으로 CSS를 구조화하여 표현할 수 있다.
2. 가독성과 재사용성을 높여주어 유지보수가 수월하다.
3. CSS의 태생적 한계를 보완하기 위해 Sass는 다음과 같은 추가 기능과 유용한 도구들을 제공한다.
    - 변수의 사용
    - 조건문과 반복문
    - import (모듈화)
    - Nesting
    - Mixin
    - Extent/Inheritence (확장/상속)
4. 선택자의 중첩(Nesting)을 통해 반복되는 부모요소 선택자 사용을 줄일수 있다.
5. 변수(Variable)을 사용해서 CSS 속성값을 통일해서 관리할 수 있다.
6. 조건문, 반복문을 통해서 동적으로 CSS 관리가 가능하다.
7. 상속되는 선택자를 계층적으로 명시하여 불필요한 반복적 사용을 줄일 수 있다.

<br>

## SASS의 단점

1. 전처리기를 위한 도구 필요
2. CSS로 컴파일하기 위한 시간 소요

<br>

## SCSS란?

scss는 Sass의 3버전에서 등장한 언어이다.

SASS도 시간이 지나면서 버젼업되며 불편한점이 개선되었고, 기존의 문법 방식이 너무 불편하고 익숙치 않아 퍼블리셔에게 익숙한 CSS와 비슷한 구문을 가지고 있으며, CSS와 완전히 호환되도록 새로운 구문을 도입한 CSS의 상위 호환 스타일시트이다.

SCSS는 기존 SASS 구문에 비해 좀 더 CSS 코드와 유사한 형태를 띄고 있어 퍼블리셔들에게 가장 각광 받고 있는 전처리기 언어이다.

- SASS, SCSS에서 기존의 CSS의 기능 부재 단점을 보완한 다양한 기능 추가
- SASS는 들여 쓰기+줄 바꿈 형식, SCSS는 중괄호+세미콜론 형식

공식 레퍼런스에서는 SASS보다는 CSS와 더 비슷하고 호환성이 좋은 SCSS를 선호한다고 한다.

<br>

## 차이점?

큰 차이점은 구문 스타일인데, SASS는 중첩으로 들여 쓰기를 사용하고 속성 구분은 줄 바꿈을 이용하지만, SCSS의 경우 중괄호로 중첩을 표현하고 세미콜론으로 속성을 구분한다.

```
//css
a {
    color: red;
}
a:hover {
    color: lime;
}
```
```
// SASS
$color: red
$color2: lime

a
    color: $color
    &:hover
        color: $color2
```
```
// SCSS
$color: red;
$color2: lime;

a {
    color: $color;
    &:hover {
        color: $color2;
    }
}
```

<br>

두번째 차이점은 믹스인(mixin) 문법이다.

minin 문법은 재사용 가능 기능을 의미하는데 SASS의 경우에는 = 로 선언하고 +로 적용시키고, SCSS의 경우에는 @mixin으로 선언하고 @include로 적용시킨다.

```
// SASS
$main-font: "Baskervville"

=title($font)
    font-size: 30px
    font-family: $font

#header
    +title ($main-font)
```
```
// SCSS
$main-font: "Baskervville";

@mixin title($font) {
    font-size: 30px;
    font-family: $font;
}

#header {
    @include title($main-font);
}
```