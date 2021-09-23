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
