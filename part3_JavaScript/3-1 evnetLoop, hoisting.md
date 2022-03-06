# JavaScript Event Loop

#### Javascript Engine

![javascript_engine](../assets/javascript_engine.png)

- javascript로 작성한 코드를 해석하고 실행하는 __인터프리터__이다.

- Call Stack, Task Queue(Event queue), Heap, Event loop

  - Call Stack :  자바스크립트는 __단 하나의 호출스택(call stack)__을 사용한다. 이는 하나의 함수가 실행되면 이 함수의 실행이 끝날 때까지 다른 어떤 task도 수행될 수 없다는 의미이다. 요청이 들어올 때마다 해당 요청을 __순차적__으로 호출 스택에 담아 처리한다. 메소드가 실행될 때, Call Stack에 새로운 프렝미이 생기고 __push__되고 메소드의 싫애이 끝나면 해당 프레임은 __pop__되는 원리이다. 

  - Heap : 동적으로 생성된 객체(인스턴스)는 힙에 할당됨. 대부분 구조화되지 않은 '더미'같은 메모리 영역을 'heap'이라 표현한다.

  - Task Queue(Event Queue) : 자바스크립트의 런타임환경에서는 처리해야 하는 Task들을 임시 젖아한느 대기 큐가 존재한다. 그 대기 큐를 __Task Queue__ or  __Event Queue__ 라고 한다. 그리고 Call Stack이 __비워졌을 때__ 먼저 대기열에 들어온 순서대로 수행됨.

    ```javascript
    setTimeout(function() {
        console.log("first");
    }, 0);
    console.log("second")
    
    //console >> 
    //second
    //first
    ```

    비동기로 호출되는 함수들은 Call Stack에 쌓이지 않고 __Task Queue__에 __enqueue__된다. 자바스크립트에선 이벤트에 의해 실행되는 함수들이 비동기로 실행된다. __Web API영역__에 따로 정의되어 있는 함수들은 비동기로 실행된다.

    ```javascript
    function test1() {
        console.log("test1")
        test2();
    }
    
    function test2() {
        let timer = setTimeout(function () {
            console.log("test2");
        },0);
        test3();
    }
    
    function test3(){
        console.log("test3")
    }
    
    test1();
    
    //console >> 
    //test1
    //test3
    //test2
    ```

    ```javascript
    while (queue.waitForMessage()){
        queue.processNextMessage();
    }
    ```



#### Hoisting

`hoist`라는 단어의 사전적 정의는 끌어올리기 라는 뜻이다. 자바스크립트에선 변수가 끌어올려진다. `var` keyword 로 선언된 모든 변수 선언은 __호이스트__ 된다. 

호이스트란 변수의 정의가 그 범위에 따라 `선언` 과 `할당` 으로 분리되는 것을 의미한다. 즉, 변수가 함수 내에서 정의되었을 경우, 선언이 함수의 최상위로, 함수 바깥에서 정의되었을 경우, 전역 컨텐스트의 최상위로변경이 된다.

- 선언 (Declaration) 과 할당(Assignment)

  - 끌어 올려지는것은 선언이다.

  ```javascript
  function getX() {
      console.log(x); // undefined
      var x = 100;
      console.log(x); // 100
  }
  getX();
  ```

  다른 언어의 경우엔, 변수 x를 선언하지 않고 출력하려하면 오류가 발생함. 하지만 자바스크립트에선 `undefined`라고 넘어간다. `var x = 100;`이 구문에서 `var x;`를 호이스트 하기 때문이다. 작동 순서에 맞게 코드를 재구성하면 다음과 같다

  ```javascript
  function getX(){
      var x;
      console.log(x);
      x = 100;
      console.log(x);
  }
  getX();
  ```

  선언문은 항시 자바스크립트 엔진 구동시 가장 __최우선__적으로 해석하므로 호이스팅되고, __할당 구문은 런타임 과정에서 이루어지기 때문에__ 호이스팅 되지 않는다.

  ```javascript
  foo();
  function foo() {
      console.log('hello');
  };
  // console > hello
  ```

  foo 함수에 대한 선언을 호이스팅하여 global 객체에 등록시키기 때문에 `hello`가 제대로 출력됨

  ```javascript
  foo( );
  var foo = function( ) {
    console.log(‘hello’);
  };
  // console> Uncaught TypeError: foo is not a function
  ```

  함수 리터럴을 할당하는 구조이기 때문에 호이스팅 되지 않으며 그렇기 때문에 런타임 환경에서 `Type Error`를 발생시킨다.


