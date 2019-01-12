# Enhanced Object Literals 향상된 객체 리터럴
- 객체의 속성을 메서드로 사용할 때 `function` 예약어를 생략하고 생성 가능하다.

```js
var dictionary = {
	words: 100,
	// ES5
	lookup: function() {
		console.log("find words");
	},
	
	// ES6
	lookup() {
		console.log("find words");
	}
}
```

## 속성명의 축약 특징
- 객체의 속성명과 값 명이 동일할 때 아래와 같이 축약 가능하다.

```js
var figures = 10;
var dictionary = {
	figures
}
```

