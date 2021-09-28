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
