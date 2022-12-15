# Vue.js Starting Guide

# Vue�� �����ΰ�?

- <a href = "https://012.vuejs.org/guide/">Concepts Overview</a>

  <img src="./img/01concepts.png" width = "90%">

- MVVM������ ��� ���̾ �ش��ϴ� View ���̺귯��
- DOM Listenters, DataBindings �� ����
- HTML(DOM)���� ���� -> �����ʰ� listen -> JavaScript Obj ����
- JavaScript Obj ���� -> Data binding -> DOM�ݿ�

# ������ �� ����Ʈ ���� ����

- ������ �� ����Ʈ���� ������ HTML, CSS, JavaScript�� ����ؿ���

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

- html�� DOM�� ����, JavaScript�� DOM�� ����
- ��κ��� ������ ������ �̷���� ������ �ش� ���� �����ϰ� ��. (�ϵ��ڵ� X)
- �ش� �ڵ忡�� string���� �ٲ۴ٰ� �ϸ� ������ �ݿ��ɱ�? -> X
- �Ʒ��� ���� �ٽ� ������Ʈ�� �����ؼ� ���� ������������� ���� �ٲ�

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

- �̸� �ذ�����! -> ���ߵ� ������ ����Ʈ���� ���̺귯����

# Reactivity

- <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/defineProperty">Object.defineProperty()</a>

  - The static method Object.defineProperty() defines a new property directly on an object, or modifies an existing property on an object, and returns the object.
  - ��ü�� Ư�� �Ӽ� ������ ������ �ϴ� API
    ```html
    Object.defineProperty('���ü', ��ü�� �Ӽ�, { ������ ���� })
    ```
  - Reactivity ���
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
            Object.defineProperty('���ü', ��ü�� �Ӽ�, {
                ������ ����
            })
          */
          Object.defineProperty(viewModel, "str", {
            //�Ӽ��� ���������� ���� ����
            get: function () {
              console.log("����");
            },
            //�Ӽ��� ���� �Ҵ������� ���� ����
            set: function (newValue) {
              console.log("�Ҵ�", newValue);
              div.innerHTML = newValue;
            },
          });
        </script>
      </body>
    </html>
    ```
    ```log
    viewModel.str = "hi"
    vue-way.html:26 �Ҵ� hi
    'hi'
    viewModel.str = "hi!!!"
    vue-way.html:26 �Ҵ� hi!!!
    'hi!!!'
    ```
  - Reactivity ���̺귯��ȭ

    - ��ý��� �Լ��� Ȱ��, init�� render�� application logic�� ������� �ʵ��� �Ǵٸ� scope�� �־���.
    - �Ϲ����� ���¼ҽ� ���̺귯���� �ۼ��� �� �ϳ�.

    ```html
    <body>
      <div id="app"></div>
      <script>
        var div = document.querySelector("#app");
        var viewModel = {};

        //��ý���
        (function () {
          function init() {
            Object.defineProperty(viewModel, "str", {
              //�Ӽ��� ���������� ���� ����
              get: function () {
                console.log("����");
              },
              //�Ӽ��� ���� �Ҵ������� ���� ����
              set: function (newValue) {
                console.log("�Ҵ�", newValue);
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

# Vue�� Ȱ���� Reactivity

- Vue ���̺귯���� Ȱ���Ͽ� Reactivity�� ����

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

# �� �ν��Ͻ��� ������Ʈ

- <a href="https://012.vuejs.org/api/">�ν��Ͻ�</a>

  - ������ �Լ�

    ```html
    new Vue();
    ```

    - �ν��Ͻ� �ɼ�

    ```html
    new Vue({ el:, template:, data:, methods:, created:, watch: });
    ```

    ```html
    <body>
      <div id="app"></div>
      <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
      <script>
        var vm = new Vue({
          el: "#app",
          data: {
            message: "hi",
          },
          methods: {},
        });
      </script>
    </body>
    ```

- <a href="https://012.vuejs.org/guide/#Components">������Ʈ</a>

  - In Vue.js, every component is simply a Vue instance. Components form a nested tree-like hierarchy that represents your application interface.
  - ���뼺�� �ö󰡰� �ڵ带 �ּ�ȭ ����
    <img src="./img/02components.png" width = "90%">
  - �ν��Ͻ� ������ �⺻������ root component�� ����
  - ������Ʈ ���
    ```html
    Vue.component("������Ʈ �̸�", ������Ʈ ����);
    ```
  - ���� ������Ʈ

    ```html
    <body>
      <div id="app">
        <app-header> </app-header>
        <app-content></app-content>
      </div>

      <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
      <script>
        //����������Ʈ
        Vue.component("app-header", {
          template: "<h1>Header</h1>",
        });

        Vue.component("app-content", {
          template: "<div>content</div>",
        });

        new Vue({
          el: "#app",
        });
      </script>
    </body>
    ```

  - ���� ������Ʈ

    ```html
    new Vue({ el : "#app", components: { 'app-footer' : { template : "
    <footer>footer</footer>
    " } } });
    ```

  - ����������Ʈ�� �ν��Ͻ��� ����
    - ���� ������Ʈ�� ��� ��� �ν��Ͻ��� ���� ��� ������Ʈ�� ����
    - ���� ������Ʈ�� ��� �ν��Ͻ� �ϳ��� ������ ������Ʈ�鸸 ����
    - ���� ���� ������Ʈ�� �����

- Components Sample Code

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
      <div id="app">
        <app-header> </app-header>
        <app-content></app-content>
        <app-footer></app-footer>
      </div>
      <div id="app2">
        <!-- �������� ������ ������Ʈ ��� -->
        <app-header> </app-header>
        <!-- �������� ������ ������Ʈ�� ��µ��� ���� -->
        <app-footer></app-footer>
      </div>

      <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
      <script>
        //����������Ʈ
        Vue.component("app-header", {
          template: "<h1>Header</h1>",
        });

        Vue.component("app-content", {
          template: "<div>content</div>",
        });

        //���� ������Ʈ
        new Vue({
          el: "#app",
          components: {
            "app-footer": {
              template: "<footer>footer</footer>",
            },
          },
        });

        new Vue({
          el: "#app2",
          components: {},
        });
      </script>
    </body>
  </html>
  ```

# ������Ʈ ��� ���

- �� ������Ʈ�� ������ ������ ������ ��ȿ ������ ����
- ������Ʈ�� �����͸� �ְ�ޱ� ���ؼ��� Ư���� "��Ģ"�� ����� ��
- ��Ģ(rules)
  - ���� -> ���� : ���ӽ� (props)
  - ���� -> ���� : �̺�Ʈ (event)
    <a href="https://dzone.com/articles/how-do-components-interact-in-vue-and-what-is-vuex"><img src="./img/03components_rules.png"></a>
- ������Ʈ ��Ź���� �ʿ��� ����
  - Ư�� ������Ʈ�� ��ȭ�� ���� �ٸ� ������Ʈ�� ���������� �����͸�
    �ְ�޾����� �������� �帧�� �����ϱ� ����� (MVC ����)
  - ���ӽ�, �̺�Ʈ�� ����ϹǷ� �������� �帧�� �����ϱⰡ �������� (����, ������� ������. ���������� ����)

# Props (���� -> ����)
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
    <div id="app">
      <app-header v-bind:propsdata="message"></app-header>
      <app-content v-bind:propsdata="num"></app-content>
      <app-footer v-bind:propsdata="res"></app-footer>
    </div>
    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
    <script>
      var app_header = {
        template: "<h1>{{ propsdata }}</h1>",
        //root data to props
        props: ['propsdata']
      }

      var app_content = {
        template: "<h1>{{ propsdata }}</h1>",
        //root data to props
        props: ['propsdata']
      }

      var app_footer = {
        template: "<h1>{{ propsdata }}</h1>",
        //root data to props
        props: ['propsdata']
      }

      new Vue({
        el: '#app',
        components: {
          'app-header' : app_header,
          'app-content' : app_content,
          'app-footer' : app_footer
        },
        data: {
          //root data
          message : 'hi',
          num : 10,
          res : "ok"
        }
      })
    </script>
  </body>
</html>
```
# Event Emit (���� -> ����)
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
</head>
<body>
  <div id="app">
    <p>{{ num }}</p>
    <!-- <app-header v-on:����������Ʈ���� �߻��� �̸�="����������Ʈ�� �޼��� �̸�"></app-header> -->
    <app-header v-on:pass="logText">
    </app-header>
    <app-content v-on:add="increaseNum"></app-content>
  </div>
  <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
  <script>
    var app_header = {
      template: '<button v-on:click="passEvent">click me</buttion>',
      methods : {
        passEvent : function() {
          this.$emit('pass');
        }
      }
    }
    var app_content = {
      template: '<button v-on:click="addEvent">add</buttion>',
      methods : {
        addEvent : function() {
          this.$emit("add")
        }
      }
    }

    new Vue({
      el: '#app',
      components: {
        'app-header' : app_header,
        'app-content' : app_content
      },
      methods : {
        logText: function() {
          console.log('hi');
        },
        increateNum: function() {
          this.num ++;
          console.log(this.num)
        }
      },
      data : {
        num : 10
      }
    })
  </script>
</body>
</html>
```