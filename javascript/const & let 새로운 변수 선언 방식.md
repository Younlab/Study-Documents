# const & let 새로운 변수 선언 방식

- 블록단위 `{ }`로 변수 범위가 제한되어 있다.
- `const` : 한번 선언한 값에 대하여 변경할 수 없다.(상수)
- `let` : 한번 선언한 값에 대하여 다시 선언언 할 수 없다.

## const
```js
const a = 10;

a = 20;
// !Error

```
> 어떠한 경우에도 const 로 선언한 값은 변경할 수 없다. (상수개념)

## let
```js
let a = 10;

let a = 20;
// !Error

a = 30;
30
```
> 한번 선언한 값은 다시 정의하지 못한다.
> 값 재할당에 대해서는 허용한다.

## ES6 `{ }` 단위로 범위가 제한된다.
```js
let sum = 0;

for (let i = 1; i <= 5; i++) {
	sum = sum +i
}

console.log(sum); // 10

// for 문을 벗어나면 let i 를 접근할 수 없다.
console.log(i);
// !Error
```

## ES6 `const` 로 지정한 값은 변경 할 수 없다.
```js
const a = 10;

a = 20;
// !Error
```

하지만, 객체나 배열의 내부는 변경 할 수 있다.

```js
const a = {};

a.num = 10;

console.log(a);
// {num:10}

const a = [];

a.push(20);

console.log(a);
// [20]
```

## ES5 Hoisting 특징
- Hoisting 이란 선언한 함수와 변수를 해석기가 가장 상단에 있는 것 처러머 인식한다.
- js 해석기는  코드의 라인 순서와 관계 없이 **함수선언식** 과 변수를 위한 공간을 먼저 확보한다.
- 따라서, `function a()` 와 `var` 는 코드의 최상단으로 끌어올려진것(hoisted) 처럼 보인다.

```js
function willBeOveridden() {
	return 10;
}

// 내가 예상한 값은 10
willBeOveridden()
// 결과값은 5

willBeOveridden() {
	return 5;
}
```
> 함수가 선언된 위치, 라인에 상관없이 마지막에 정의된 값으로 끌어올려지는 것으로 이해하면 될 것 같다.

## javascript 해석기가 코드를 해석하는 순서는?
```js
var sum = 5;

sum = sum + i;

function sumAllNumbers() {
	//...
}

var i = 10;
```

해당 코드를 실행했을 때 **오류가 나지 않는다.** 자체적으로 해석기가 해석하는 순서는 아래와 같다.

```js
// #1 함수 선언식과 변수 선언을 hoisting
var sum;

function sumAllNumbers() {
	//...
}

var i;

// #2 변수 대입 및 할당
var sum = 5;

sum = sum +i;

i = 10;
```


