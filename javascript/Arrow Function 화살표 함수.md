# Arrow Function 화살표 함수

- 함수를 정의 할 때 `function` 이라는 키워드를 사용하지 않고 `=>` 로 대체
- 흔히 사용하는 **콜백함수** 의 문법을 간결화

```js
// ES5 함수 정의 방식
var sum = function() {
	return a + b;
}

// ES6 함수 정의 방식
var sum = (a, b) => {
	return a + b;
}

sum(10,20);
```

## 화살표 함수 사용 예시

```js
// ES5
var arr = ['a', 'b', 'c'];

arr.forEach(function(value){
	console.log(value);
});
// a, b, c

// ES6
var arr = ['a', 'b', 'c'];

arr.forEach(value => console.log(value));
// a, b, c
```
