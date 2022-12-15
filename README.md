# Vue.js Starting Guide

# Vue란 무엇인가?

- <a href = "https://012.vuejs.org/guide/">Concepts Overview</a>

  <img src="./img/01concepts.png" width = "90%">

- MVVM패턴의 뷰모델 레이어에 해당하는 View 라이브러리
- DOM Listenters, DataBindings 로 구성
- HTML(DOM)에서 조작 -> 리스너가 listen -> JavaScript Obj 변경
- JavaScript Obj 변경 -> Data binding -> DOM반영

# 기존의 웹 프론트 엔드 개발

- 기존의 웹 프론트엔드 개발은 HTML, CSS, JavaScript를 사용해왔음

  ```html
  <!DOCTYPE html>
  <html lang="en">
    <head>
      <meta charset="UTF-8" />
      <meta http-equiv="X-UA-Compatible" content="IE=edge" />
      <meta name="viewport" content="width=device-width, initial-scale=1.0" />
      <title>Document</title>
    </head>
    <body>
      <div id="app"></div>

      <script>
        var div = document.querySelector("#app");
        var string = "hello world";
        console.log(div);
        div.innerHTML = "hello World!!!";
      </script>
    </body>
  </html>
  ```

- html은 DOM을 구성, JavaScript는 DOM을 조작
- 대부분의 값들은 변수로 이루어져 있으며 해당 값을 참조하게 됨. (하드코딩 X)
- 해당 코드에서 string값을 바꾼다고 하면 내용이 반영될까? -> X
- 아래와 같이 다시 오브젝트를 접근해서 값을 변경해줘야지만 값이 바뀜

  ```html
  <script>
    var div = document.querySelector("#app");
    console.log(div);

    var string = "hello world";
    div.innerHTML = string;

    var string = "hello world!!";
    div.innerHTML = string;
  </script>
  ```

- 이를 해결하자! -> 개발된 수많은 프론트엔드 라이브러리들

# Reactivity

- <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/defineProperty">Object.defineProperty()</a>

  - The static method Object.defineProperty() defines a new property directly on an object, or modifies an existing property on an object, and returns the object.
  - 객체의 특정 속성 동작을 재정의 하는 API
    ```html
    Object.defineProperty('대상객체', 객체의 속성, { 정의할 내용 })
    ```
  - Reactivity 사용
    ```html
    <!DOCTYPE html>
    <html lang="en">
      <head>
        <meta charset="UTF-8" />
        <meta http-equiv="X-UA-Compatible" content="IE=edge" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <title>Document</title>
      </head>
      <body>
        <div id="app"></div>
        <script>
          var div = document.querySelector("#app");
          var viewModel = {};
          /*
            Object.defineProperty('대상객체', 객체의 속성, {
                정의할 내용
            })
          */
          Object.defineProperty(viewModel, "str", {
            //속성에 접근했을때 동작 정의
            get: function () {
              console.log("접근");
            },
            //속성의 값을 할당했을때 동작 정의
            set: function (newValue) {
              console.log("할당", newValue);
              div.innerHTML = newValue;
            },
          });
        </script>
      </body>
    </html>
    ```
    ```log
    viewModel.str = "hi"
    vue-way.html:26 할당 hi
    'hi'
    viewModel.str = "hi!!!"
    vue-way.html:26 할당 hi!!!
    'hi!!!'
    ```
  - Reactivity 라이브러리화

    - 즉시실행 함수를 활용, init과 render를 application logic에 노출되지 않도록 또다른 scope에 넣어줌.
    - 일반적인 오픈소스 라이브러리의 작성법 중 하나.

    ```html
    <body>
      <div id="app"></div>
      <script>
        var div = document.querySelector("#app");
        var viewModel = {};

        //즉시실행
        (function () {
          function init() {
            Object.defineProperty(viewModel, "str", {
              //속성에 접근했을때 동작 정의
              get: function () {
                console.log("접근");
              },
              //속성의 값을 할당했을때 동작 정의
              set: function (newValue) {
                console.log("할당", newValue);
                render(newValue);
              },
            });
          }

          function render(value) {
            div.innerHTML = value;
          }

          init();
        })();
      </script>
    </body>
    ```

# Vue를 활용한 Reactivity

- Vue 라이브러리를 활용하여 Reactivity를 구현

  ```html
  <!DOCTYPE html>
  <html>
    <head>
      <meta charset="utf-8" />
      <meta name="viewport" content="width=device-width, initial-scale=1.0" />
      <title>Getting Started</title>
    </head>
    <body>
      <div id="app">{{ message }}</div>

      <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
      <script>
        new Vue({
          el: "#app",
          data: {
            message: "Hello Vue!",
          },
        });
      </script>
    </body>
  </html>
  ```

# 뷰 인스턴스와 컴포넌트
- <a href="https://012.vuejs.org/api/">인스턴스</a>
  - 생성자 함수
    ```html
    new Vue();
    ```
    - 인스턴스 옵션
    ```html
    new Vue({ 
      el:, 
      template:, 
      data:, 
      methods:, 
      created:, 
      watch: });
    ```
    ```html
    <body>
      <div id="app"></div>
      <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
      <script>
        var vm = new Vue({
          el: "#app",
          data : {
            message: "hi"
          },
          methods: {

          },
        });
      </script>
    </body>
    ```
- 컴포넌트
  - In Vue.js, every component is simply a Vue instance. Components form a nested tree-like hierarchy that represents your application interface.
  - 재사용성이 올라가고 코드를 최소화 가능
    <img src="./img/02components.png" width = "90%">
  
