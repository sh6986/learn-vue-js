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


