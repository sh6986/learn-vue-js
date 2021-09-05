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


뷰로 화면을 조작하는 방법을 의미. 크게 데이터 바인딩과 디렉티브로 나뉜다.

## 데이터 바인딩

- 콧수염 괄호

```java
<div>{{ message }}</div>
```

## 디렉티브

- v- 붙는것들

```java
<div>
	Hello <span v-if-"show">Vue.js</span<
</div>
```

## computed 속성

- Vue 인스턴스의 data를 대상으로 data에 의존해서 결과값을 반환한다.
화면에 doubleNum 을 표시할 때 data의 num에 *2를 해서 보여주므로 data 의 num에 의존하게 된다.

```java
new Vue({
	el: '#app',
	data: {
		num: 10,
	},
	computed: {
		doubleNum: function() {
		return this.num * 2;
		}
	}
});
```

- 요소에 클래스에도 접근 가능하다.

```java
<div id="app">
	<p v-bind:class="errorTextColor">Hello</p>
</div>

new Vue({
	el: '#app',
	data: {
		// cname: 'blue-text',
		isError: false
	},
	computed: {
		errorTextColor: function() {
			return this.isError ? 'warning' : null;
		}
	}
});
```

## v-bind

- dom에 대한 정보에 접근해서 변경가능하다.
- ex) 해당 요소에 id를 Vue 인스턴스의 data로 관리하고 싶을때

    ```java
    new Vue({
    	el: '#app',
    	data: {
    		num: 10,
    		uuid: 'abc1234'
    	},
    });
    ```

    ```java
    <div id="app">
    	<p v-bind:id="uuid">{{ num }}</p>
      <!-- <p id="abc1234">{{ num }}</p> -->
    </div>
    ```

- {}를 사용하면  data 값에 따라 class값을 설정할 수 있다.

    ```java
    <p v-bind:class="{ warning: isError }">Hello</p>

    <script>
    	new Vue({
    		el: '#app',
    		data: {
    			// cname: 'blue-text',
    			isError: false
    		}
    	});
    </script>
    ```

## 이외 자주사용하는 디렉티브

- v-if, v-else
- v-show
    - v-if 는 돔을 아예 제거하고 v-show는 css display를 none으로 설정
- v-model (input 박스 등에 값을 연결)
- v-on
    - v-on:click, v-on:keyup 등 다양하다
    ++ event modifier : v-on:keyup.enter 처럼 enter 시 이벤트 발생 가능하다. 종류 다양하므로 찾아보면 좋다.
    - v-on:submit
    form 태그 사용시 submit 이벤트시 Vue인스턴스에 따로 설정해놓은 methods를 연결할 수 있다. 
    보통 form 으로 보낼시 새로고침 되는것을 막기위해 사용하고, 이때 해당 메소드에 event인자를 받아서 event.preventDefault()를 사용해서 폼의 이동, 새로고침을 막는다. →바닐라js, 제이쿼리 방식
    뷰에서는 v-on:submit.prevent를 이용해 이벤트 기본 동작을 막는다.(event modifier)

++ 모르는 문법이 나오면 공식 문서를 보고 해결하면 된다.

[Form Input Bindings - Vue.js](https://vuejs.org/v2/guide/forms.html#ad)

## watch 속성

- vue 인스턴스 내 데이터를 대상으로 하고 데이터의 변화에 따라서 특정 로직을 실행할 수 있는 뷰의 속성

```java
new Vue({
	el: '#app',
	data: {
		num: 10
	},
	watch: {
		num: function(newValue, oldValue) {
			this.logText();
		}
	},
	methods: {
		logText: function() {
			console.log('changed');
		}
	}
});
```

- num 이 변화할때마다 watch 안에 num 의 함수안에 정의한 코드가 실행된다.

## watch 속성 vs computed 속성

- coumputed - 단순한 값에 대한 계산. validation 뷰 라이브러리들이 대부분 computed로 만들어져 있다.
- watch - 주로 무거운 로직. 매번 실행되기 부담스러운 로직. axios 요청 등
- 공식문서에 왠만하면 computed 를 사용하는것이 좋고, watch 보다는 computed 가 대부분에 경우에 적합하다라고 나와있다.

[Computed Properties and Watchers - Vue.js](https://vuejs.org/v2/guide/computed.html#ad)


- Vue Commend Line Interface - 명령어를 통한 특정 액션 수행하는 도구
- 명령어 보조 도구, 명령어 실행 도구

[Vue CLI](https://cli.vuejs.org/)

## 설치

- vsCode 에 새 터미널을 열고 bash 터미널에 입력

### 버전 확인

```java
node -v
```

- 10 버전 이상 가능

```java
npm -v
```

- 6버전 이상 가능

### vue cli 설치

```java
npm install -g @vue/cli
```

- 라이브러리가 위치하는 폴더에 파일 쓰기 권한이 없어서 오류가 났을 경우

    ```java
    sudo npm install -g @vue/cli
    ```

    [Where does npm install packages?](https://stackoverflow.com/questions/5926672/where-does-npm-install-packages)

## 프로젝트 생성

```java
vue create '프로젝트 폴더 위치'
```

- preset은 defalut 선택, 4.x버전이면 Vue2로 선택

### CLI 2.x 와 3.x 의 차이점

- 이전 2.x 버전

    vue init '프로젝트 템플릿 유형' '프로젝트 폴더 위치'

    ex) vue init webpack-simple '프로젝트 폴더 위치'

- 3.x 버전

    vue create '프로젝트 폴더 위치'

## 서버 실행

```java
cd vue-cli
npm run serve
```

---

## CLI로 생성한 프로젝트 폴더 구조 확인

### package.json

- 디펜던시나 라이브러리에 대한 설명
- scripts 속성 밑에 serve 를 통해 명령어를 정의할 수 있고 npm(node package manager)을 이용해 명령어를 편하게 작성할 수 있다.

    npm run serve

### public/index.html

- npm run serve 를 통해 실행되는 파일
- app 이라는 id를 가진 div 아래에 빌드된 파일들이 자동으로 추가된다.

    추가되는 내용들은 src 폴더 밑에 정의해놓은 파일들을 종합해서 하나의 파일로 변환하여 묶어서 주입한다. (webpack 참고)

### main.js

### src/App.vue - 싱글 파일 컴포넌트

```java
<template>
    <!-- HTML -->
</template>

<script>
export default {
    // Javascript - 인스턴스 옵션
}
</script>

<style>
    /* CSS */
</style>
```

- 화면에 영역을 나눴을 때 특정 영역에 해당하는 HTML, Javascript, CSS 를 한 파일에 관리한다.
- 컴포넌트 등록 방법

```java
<!-- 컴포넌트 등록 방법 -->
<hello-world></hello-world><!-- vsCode의 파일 바로가기 기능을 사용하려면 이 방법을 사용해야한다. -->
<HelloWorld></HelloWorld>
<HelloWorld/><!-- 진보된 방식 -->
```

### src/components/HelloWorld.vue

++ vue 자동완성 사용하면 vue 기본 구조를 잡아준다.

++ 리눅스 기본 명령어

[웹 개발할 때 알아두면 좋은 리눅스 기본 명령어](https://joshua1988.github.io/web-development/linux-commands-for-beginners/)


- template 속성은 항상 html 요소가 최상위에 하나만 있어야 한다.

```java
<template>
  <div>
    
  </div>
</template>
```

- data 속성 정의 시 함수를 정의하고 새 객체를 리턴해줘야 한다.

    컴포넌트를 재사용할 확률이 높은데 여러 컴포넌트에서 동일한 값을 참조하면 안되기 때문에

```java
<script>
export default {
  data: function() {
    return {
      
    }
  }
}
</script>
```

## 컴포넌트 등록

- 해당 vue 파일의 컴포넌트를 import 를 사용해서 들고 온다.
- 들고 온 컴포넌트를 components 속성에 연결한다.

```java
import AppHeader from './components/AppHeader.vue';

export default {
  data: function() {
    return {
      str: 'hi'
    }
  },
  components: {
    'app-header': AppHeader
  }
}
```

- template 에 연결한 컴포넌트를 등록해준다.

```java
<template>
  <div>
    <app-header></app-header>
  </div>
</template>
```

## axios를 이용한 데이터 전송

### axios 설치

- 서버를 끈 상태에서 터미널에 코드 입력(해당 프로젝트 폴더 내에서)

```java
npm i axios
```

- 설치 후 axios 를 import 한다.

```java
import axios from 'axios';
```

++ vue 파일명

- 파스칼case로 맨앞은 대문자로 시작해서 두단어 이상 합쳐서 만든다.

    컴포넌트로 가져와서 태그로 등록할 때 헷갈릴 수 있으므로 
    ex) main 컴포넌트 등록시 <main></main>으로 등록하는데 컴포넌트인지 태그인지 알 수 없다.
