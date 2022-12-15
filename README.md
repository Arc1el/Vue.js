# Vue.js Starting Guide

## Vue�� �����ΰ�?

- <a href = "https://012.vuejs.org/guide/">Concepts Overview</a>

  <img src="./img/01concepts.png" width = "90%">

- MVVM������ ��� ���̾ �ش��ϴ� View ���̺귯��
- DOM Listenters, DataBindings �� ����
- HTML(DOM)���� ���� -> �����ʰ� listen -> JavaScript Obj ����
- JavaScript Obj ���� -> Data binding -> DOM�ݿ�

## ������ �� ����Ʈ ���� ����

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

## Vue�� Reactivity
- <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/defineProperty">Object.defineProperty()</a>
  - The static method Object.defineProperty() defines a new property directly on an object, or modifies an existing property on an object, and returns the object.
  - ��ü�� Ư�� �Ӽ� ������ ������ �ϴ� API
    ```html
    Object.defineProperty('���ü', ��ü�� �Ӽ�, {
      ������ ����
    })
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