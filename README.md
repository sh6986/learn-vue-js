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
