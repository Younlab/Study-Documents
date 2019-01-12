# Vuex 상태 관리 라이브러리
- Vuex 는 Vue.js 에 대한 상태 관리 패턴 + 라이브러리이다. 애플리케이션의 모든 컴포넌트에 대한 중앙 집중식 저장소 역할을 하며 예측 가능한 방식으로 상태를 변경할 수도 있다.
- Vue.js 의 공식devtools [확장 프로그램](https://github.com/vuejs/vue-devtools) 과 통합되어 설정 시간이 필요 없는 디버깅 및 상태 스냅샷 내보내기/가져오기와 같은 고급 기능을 제공한다.

> Vuex 공식문서 발췌

## Vuex란?
- 무수히 많은 컴포넌트의 데이터를 관리하기 위한 상태관리 패턴, 라이브러리
- React의 Flux 패턴에서 기안
- Vue.js 중고급 개발자로 성장하기 위한 필수 관문

## Flux란?
- MVC 패턴의 복잡한 데이터 흐름 문제를 해결하는 개발 패턴
- Action 부터 View 까지 한 방향

> `Action` -> `Dispatcher` -> `Model` -> `View`

1. action : 화면에서 발생하는 이벤트 또는 사용자의 입력
2. dispatcher : 데이터를 변경하는 방법, 메서드
3. model : 화면에 표시할 데이터
4. view : 사용자에게 비춰지는 화면

## MVC 패턴과 Flux 패턴의 비교
1. MVC 패턴

> `Controller` -> `Model` <-> `View`

2. Flux 패턴

> `Action` -> `Dispatcher` -> `Model` -> `View`

## MVC 패턴의 문제점
- 기능 추가 및 변경에 따라 생기는 문제점을 예측할 수가 없다. 데이터의 흐름을 추적하기 힘들다.
- 앱이 복잡해지면 생기는 업데이트 루프

## Vuex 컨셉
- State : 컴포넌트 간에 공유하는 데이터 `data()`
- View : 데이터를 표시하는 화면 `template`
- Action : 사용자의 입력에 따라 데이터를 변경하는 `methods`


> **단방향 데이터 흐름**
> `View` -> `Action` -> `State` -> `View` -> `Action`...Loop

## Vuex 구조
컴포넌트(vue components) -> 비동기 로직(actions) -> 동기 로직(mutaions) -> 상태(state)

## Vuex install
- Vuex는 싱글 파일 컴포넌트 체계에서 NPM 방식으로 라이브러리를 설치하는 것이 좋다.

install script
```sh
// npm install
npm install vuex --save

// yarn install
yarn add vuex
```

CDN
```html
<script src="https://unpkg.com/vuex">
```

## Vuex 기술 요소
- sate : 여러 컴포넌트에 공유되는 데이터 `data`
- getters : 연산된 state 값을 접근하는 속성 `computed`
- mutations : state 값을 변경하는 이벤트 로직/메서드 `methods`
- actions : 비동기 처리 로직을 선언하는 메서드 `aysnc methods`

## state란?
- 여러 컴포넌트 간에 공유할 데이터 `상태`

```js
// Vue
data : {
	message : 'Hello Vue.js!'
},
// Vuex
state : {
	message : 'Hello Vue.js!'
}
```
```html
<!-- Vue -->
<p> {{ message }} </p>

<!-- Vuex -->
<p> {{ this.$store.state.message }} </p>
```

## getters란?
- state 값을 접근하는 속성이자 `computed()`처럼 미리 연산된 값을 접근하는 속성이다.

```js
// store.js
state : {
	num : 10
},
getters : {
	getNumber(state) {
		return state.num;
	},
	doubleNumber(state) {
		return state.num * 2;
	}
}
```
```html
<p>{{ this.$store.getters.getNumber }}</p>
<p> {{ this.$store.getters.doubleNumber }} </p>
```

## mutations란?
- state의 값을 변경할 수 있는 **유일한방법**이자 메서드
- mutations 은 `commit()`으로 동작시킨다.

```js
// store.js
state : { num : 10 },
mutations : {
	printNumbers(state) {
		return state.num
	},
	sumNumbers(state, anotherNum) {
		return state.num + anotherNum;
	}
}

// App.vue
this.$store.commit('printNumbers');
this.$store.commit('sumNumbers', 20);
```

### mutations의 commit() 형식
- state를 변경하기 위해 mutations를 동작시킬 때 인자(payload)를 전달할 수 있다.

```js
// store.js
state : { storeNum : 10 },
mutations: {
	modifyState(state, payload) {
		console.log(payload.str);
		return state.storeNum += payload.num;
	}
}

// App.vue
this.$store.commit('modifyState', {
	str : 'passed from payload',
	num : 20
})
```

## actions란?
- 비동기 처리 로직을 선언하는 메서드, 비동기 로직을 담당하는 mutations
- 데이터 요청, Promise, ES6 async 와 같은 비동기 처리는 모두 actions에 선언한다.

```js
// store.js
state : {
	num : 10
},
mutations : {
	doubleNumber(state) {
		state.num * 2;
	}
},
actions : {
	delayDoubleNumber(context) {
		// context 로 store 의 메서드와 속성 접근
		context.commit('doubleNumber);
	}
}

// App.vue
this.$store.dispatch('delayDoubleNumber');
```

### actions 비동기 코드 예제
- 2초 뒤에 해당하는 mutations 를 실행

```js
// store.js
mutations : {
	addCounter(state) {
		state.counter++
	},
},
actions : {
	dlayedAddCounter(context) {
		setTimeout(() => context.commit('addCounter'), 2000);
	}
}

//App.vue
methods : {
	incrementCounter() {
		this.$store.dispatch('delayedAddCounter');
	}
}
```

- context.commit 으로 state 를 동기화하는 mutstions 를 호출

```js
// store.js
mutations : {
	setData(state, fetchedData) {
		state.product = fetchedData;
	}
},
actions : {
	fetchProductData(context) {
		return axios.get('http://domain.com/products/1')
			.then(response => context.commit('setData', response))
			.catch(error => console.log(error));
	}
}

// App.js
methods : {
	getProduct() {
		this.$store.dispatch('fetchProductData');
	}
}
```

## Vue Helper
- 헬퍼를 사용하고자 하는 vue 파일에서 아래와 같이 해당 헬퍼를 로딩한다.

```js
// App.js
import { mapState } from 'vuex'
import { mapGeters } from 'vuex'
import { mapMutations } from 'vuex'
import { mapActions } from 'vuex'

export default {
	computed() { ...mapState(['num']), ...mapGetters(['countedNum']) },
	methods : { ...mapMutations(['clickBtn']), ...mapActions(['asyncClickBtn']) }
}
```

### mapState
- vuex에 선언한 state속성을 vue 컴포넌트에 더 쉽게 연결해주는 헬퍼다.

```js
// App.js
import { mapState } from 'vuex'

computed() {
	...mapState(['num'])
	// num() { return this.$store.state.num; }
}

// store.js
state : {
	num : 10
}
```
```html
<!-- <p>{{ this.$store.state.num }}</p> -->
<p>{{ this.num }}</p>
```

### mapGetters
- vuex에 선언한 getters 속성을 뷰 컴포넌트에 더 쉽게 연결해주는 헬퍼다.

```js
// App.vue
import { mapGetters } from 'vuex'

computed() { ...mapGetters(['reverseMessage']) }

// store.js
getters: {
	reverseMessage(state) {
		return state.msg.split('').reverse().join('');
	}
}
```
```html
<!-- <p>{{ this.$store.getters.reverseMessage }}</p> -->
<p>{{ this.reverseMessage }}</p>
```

### mapMutations
- vuex에 선언한 mutations 속성을 뷰 컴포넌트에 더 쉽게 연결해주는  헬퍼다.

```js
// App.js
import { mapMutations } from 'vuex'

methods : {
	...mapMutations(['clickBtn]),
	authLogin() {},
	displayTable() {}
}

// store.js
mutations : {
	clickBtn(state) {
		alert(state.msg);
	}
}
```
```html
<button @click="clickBtn">popup message</button>
```

### mapActions
- vuex에 선언한 actions 속성을 뷰 컴포넌트에 더 쉽게 연결해주는 헬퍼다.

```js
// App.js
import { mapActions } from 'vuex'

methods : {
	...mapActions(['delayClickBtn]),
}

// store.js
actions : {
	delayClickBtn(context) {
		setTimeout(() => context.commit('clickBtn'), 2000);
	}
}
```
```html
<button @click="delayClickBtn">delay popup message</button>
```

### 헬퍼의 유연한 문법
-  vuex에 선언한 속성을 그대로 컴포넌트에 연결하는 문법

```js
// 배열 리터럴
...mapMutations([
	'clickBtn',
	'addNumber'
])
```

- vuex에 선언한 속성을 컴포넌트의 특정 메서드에다가 연결하는 문법

```js
// 객체 리터럴
...mapMutations({
	popupMsg : 'clickBtn'
})
```

> 본 문서는 CAPTAIN PANGYO 님이 강의하신 inflearn 강좌 [Vue.js 중급 강과 - 웹앱 제작으로 배워보는 Vue.js, ES6, Vuex](https://www.inflearn.com/course/vue-pwa-vue-js-%EC%A4%91%EA%B8%89/) 을 학습 정리한 내용입니다.