# 인프런 Vue.js 시작하기 - Age of Vue.js
강의 출처 : https://www.inflearn.com/course/Age-of-Vuejs

## MVVM 모델에서의 Vue

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/6f0a4154-408a-4756-966d-58c316c98428/Untitled.png)

- View 사용자가 키보드를 입력하거나 마우스를 클릭했을 때 이벤트를 DOM Listeners 로 잡아서 자바스크립트에 있는  데이터를 바꿔주거나 자바스크립트에 지정한 특정 로직을 실행하게 된다.
- 자바스크립트에 있는 데이터가 변경되었을 때 Data Bindings를 이용해서 화면에 반영하게 된다.

## 기존 웹 개발 방식(HTML, Javascript)

- ! + tab → html 기본 틀 자동 완성

```java
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    
</body>
</html>
```

## Reactivity 구현

### Object.defindProperty

[Object.defineProperty() - JavaScript | MDN](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Object/defineProperty)

- 객체의 특정 속성에 대한 동작을 재정의한다.
- ex) 객체의 특정 속성 중 접근과 할당의 예

    ```java
    var a = 10;
    console.log(a);
    a = 20;
    ```

- 사용방법

    ```java
    Object.defineProperty(대상 객체, 객체의 속성, {
    	// 정의할 내용
    })
    ```

### Reactivity 정의

- 값을 바꿀 때 마다 화면이 계속 바뀌는 것
- 반응성
- 데이터의 변화를 라이브러리에서 감지해서 알아서 화면을 자동으로 그려주는 것
- 데이터바인딩

### 인스턴스

- 인스턴스는 뷰로 개발할 때 필수로 생성해야 하는 코드

### 인스턴스 생성

```java
new Vue();
```

인스턴스를 생성하고 나면 변수안에 인스턴스 내용을 담을 수 있다.

```java
var vm = new Vue();
console.log(vm);
```

### 인스턴스 옵션 속성

```java
new Vue({
	el: ,
	template: ,
	data: ,
	methods: ,
	created: ,
	watch: ,
});
```
![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/d9facf0c-00aa-4cbf-9ea7-700597b938d4/Untitled.png)

- 화면을 영역별로 구분해서 코드로 관리
- 인스턴스를 생성하면 개발자 도구에서 Root 컴포넌트로 인식

### 컴포넌트 등록

- 전역 컴포넌트

```java
Vue.component('컴포넌트 이름', 컴포넌트 내용);
```

- 지역 컴포넌토

```java
new Vue({
	el: '#app',
	components: {
		'컴포넌트 이름': 컴포넌트 내용
	}
});
```

++ 전역은 component 고 지역은 components (method 속성도 같다.)

### 전역 컴포넌트와 지역 컴포넌트의 차이점

- 지역컴포넌트는 하단에 어떤 컴포넌트가 등록되어있는지 알 수 있다.
- 일반적으로는 지역컴포넌트 사용
- 전역컴포넌트는 인스턴스를 생성하지 않아도 모든 인스턴스에 적용되어있다.
지역컴포넌트는 인스턴스마다 새로 생성해줘야 한다.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/c9b6d31f-7976-423e-b097-00c736f7cff4/Untitled.png)

- 컴포넌트는 각각 고유한 유효 범위를 갖는다. (데이터를 각각 관리한다) 따라서 공유하기 위해 props속성, 이벤트 를 이용해야 한다.
- 상위에서 하위로는 데이터를 내려줌, 프롭스 속성
- 하위에서 상위로는 이벤트를 올려줌, 이벤트 발생

## 컴포넌트 통신 규칙이 필요한 이유

- 데이터의 흐름을 추적할 수 있다. 항상 데이터는 내려오고 아래서 위로는 이벤트가 올라가기 때문

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/1fafc0fd-ad84-45b4-bf9d-ce571fd1f16f/Untitled.png)

## props 속성

### 사용방법

```java
<app-header v-bind:프롭스 속성 이름="상위 컴포넌트의 데이터 이름"></app-header>
```

- 상위에서 데이터를 바꾸면 하위에도 그대로 반영된다. → reactivity 가 props에도 그대로 반영

## event emit

- 하위컴포넌트에서 상위컴포넌트로 대화하는 방식

### 사용방법

```java
var appHeader = {
	template: '<button v-on:click="passEvent">click me</button>',
	methods: {
		passEvent: function() {
			this.$emit('pass');
		}
	}
}
```

## 뷰 인스턴스에서의 this

```java
var obj = {
	num: 10,
	getNumber: function() {
		console.log(this.num);
	}
}
```

- 객체의 속성에서 다른 속성을 가리킬 때는 this를 사용하면 된다. this는 해당 object를 가리키게 된다.
- Vue 인스턴스도 마찬가지

```java
new Vue = {
	el: '',
	data: {
		num: 10,
	},
	methods: {
		getNumber: function() {
			this.num
		}
	},
}
```

- 위와는 다르게 num을 data 안에 선언했음에도 this.num 을 잘 가져온다.
실제로 뷰 내부의 동작에 의해 data 내의 num은 속성으로 data 밖으로 나오게 된다.
(Vue 인스턴스를 변수에 넣고 직접 변수를 콘솔에 찍어보면 num이 속성으로 있는걸 볼 수 있다.)

[JavaScript this](https://www.w3schools.com/js/js_this.asp)

[Understanding the "this" Keyword in JavaScript](https://betterprogramming.pub/understanding-the-this-keyword-in-javascript-cb76d4c7c5e8)

## 같은 컴포넌트 레벨 간의 통신 방법

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/7813fe01-3c5f-49a3-87a7-b565ddc22d21/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/c103ce4c-8390-4776-8929-4538fe156dad/Untitled.png)

## 뷰 라우터

뷰 라이브러리를 이용하여 싱글 페이지 애플리케이션을 구현하거나 페이지 간의 이동을 구현할 때 사용하는 라이브러리

[Installation | Vue Router](https://router.vuejs.org/installation.html)

### CDN 방식

<script src="[https://unpkg.com/vue-router/dist/vue-router.js](https://unpkg.com/vue-router/dist/vue-router.js)"></script>

## 뷰 라우터 등록

```java
var router = new VueRouter({
	// 페이지의 라우팅 정보
	routes: [
		// 로그인 페이지 정보
		{
			// 페이지의 url 이름
			path: '/login',
			// 해당 url 에서 표시될 컴포넌트
			component: LoginComponent
		},
		// 메인 페이지 정보
		{
			path: '/main',
			component: MainComponent
		}
	]
});

new Vue({
	el: '#app',
	router: router
});
```

- VueRouter 인스턴스를 Vue 인스턴스에 연결한다.

### router-view 태그

```java
<div id="app">
	<router-view></router-view>
</div>
```

- url 에 따라 뿌려질 영역을 <router-view></router-view> 태그로 정의할 수 있다. (Vue 인스턴스에 Router 인스턴스를 연결해야지 사용할 수 있다.)

### router-link 태그

- 화면에서의 링크를 제공

```java
<router-link to="/login">Login</router-link>
// <a href="/login">Login</a>
```

- router-link 태그는 최종적으로 a 태그로 변한다.

++네비게이션 가드

[(중급) Vue.js 라우터 네비게이션 가드 알아보기](https://joshua1988.github.io/web-development/vuejs/vue-router-navigation-guards/)


뷰에서 권고하는 HTTP 통신 라이브러리이다.  Promise 기반의 HTTP 통신 라이브러리이다. 상대적으로 다른 HTTP 통신 라이브러리들에 비해 문서화가 잘되어 있고 API가 다양하다.

예전에 사용하던 vue-resource를 더이상 사용하지 않고 axios 를 사용한다.

[GitHub - axios/axios: Promise based HTTP client for the browser and node.js](https://github.com/axios/axios)

### CDN 방식

```java
<script src="https://unpkg.com/axios/dist/axios.min.js"></script>
```

## 사용방법

```java
new Vue({
	el: '#app',
	methods: {
		getData: function() {
			axios.get('https://jsonplaceholder.typicode.com/users/')
				.then(function(response) {
					console.log(response);
				})
				.catch(function(error) {
					console.log(error);
				});
		}
	}
});
```

++ axios의 콜백함수 내의 this는 실행컨택스트가 바뀌면서 axios 호출 전 this와 달라진다. 해결방법은 호출 전 this를 var 변수에 담고 콜백내에서 해당 변수에 값을 적용하면 된다.

[자바스크립트의 동작원리: 엔진, 런타임, 호출 스택](https://joshua1988.github.io/web-development/translation/javascript/how-js-works-inside-engine/)

++ restapi 요청할 때 테스트 할 수 있는 사이트 jsonplaceholder

[JSONPlaceholder](https://jsonplaceholder.typicode.com/)

### ++ 자바스크립트의 비동기 처리 패턴

1. callback
2. promise
3. promise + generator
4. async & await

[자바스크립트 비동기 처리와 콜백 함수](https://joshua1988.github.io/web-development/javascript/javascript-asynchronous-operation/)

[자바스크립트 Promise 쉽게 이해하기](https://joshua1988.github.io/web-development/javascript/promise-for-beginners/)

[자바스크립트 async와 await](https://joshua1988.github.io/web-development/javascript/js-async-await/)

++

[프런트엔드 개발자가 알아야하는 HTTP 프로토콜 Part 1](https://joshua1988.github.io/web-development/http-part1/)

[Chrome DevTools - Chrome Developers](https://developer.chrome.com/docs/devtools/)
