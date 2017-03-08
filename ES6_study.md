# Javascript ECMAScript 2015(_ES6_)
## 변수, 상수
  - __let__ : 블록 스코프 변수 선언
  - __const__ : 블록 스코프 상수 선언
       - 참조 타입시 주소값이 변경 불가능하지 참조 내부의 값(배열, 객체)은 변경 가능하다.
  - __var__ : ~~함수 스코프 변수 선언~~

## 파라미터 기본 값
파라미터의 기본 값으로 함수 선언시 아래와 같이 선언가능(값, 표현식)
```Javascript
function paramTest(x = 1, y = 2 + 3){ ... }
```

## 펼침 연산자
이터러블 객체앞에 ...를 붙여 객체의 개별 값으로 나눌 수 있다.
###### 배열 조합에 사용

- 기존방식
  ```javascript
  let aData = ['react', 'angular', 'backbone'];
  let bData = ['JQUERY', 'UNDERSCORE'];

  aData.concat(bData);
  // ['react', 'angular', 'backbone', 'JQUERY', 'UNDERSCORE']

  Array.prototype.push.apply(aData, bData);
  // ['react', 'angular', 'backbone', 'JQUERY', 'UNDERSCORE']
  ```
- ES6
  ```javascript
  let aData = ['react', 'angular', 'backbone'];
  let bData = ['JQUERY', 'UNDERSCORE'];

  aData.push(...bData);
  // ['react', 'angular', 'backbone', 'JQUERY', 'UNDERSCORE']
  ```

- ES6
  ```javascript
  let aData = ['react', 'angular', 'backbone'];
  let cData = [1,2, ...aData];
  // [1,2,'react', 'angular', 'backbone']
  ```

## 배열 값을 함수의 인자로 사용
- 기존방식
  ```javascript
  var aData = ['react', 'angular', 'backbone'];
  var paramTest = function(x, y){
    console.log(x + y); // default 4
  }

  paramTest.apply(null, aData);
  // reactangular;
  ```
- ES6
  ```javascript
  let aData = ['react', 'angular', 'backbone'];
  let paramTest = function(x = 1, y = 1 + 2){
    console.log(x + y); // default 4
  }

  paramTest(...aData);
  // reactangular;
  ```

## 나머지 파라미터
기존방식의 arguments객체는 유사 배열이라 배열로 변환 후 배열 메소드를 사용할 수 있지만 나머지 파라미터인 ...args는 그 자체로 배열이라 배열 메소드를 바로 사용할 수 있다.
- 기존방식
  ```javascript
  var printParam = function(a, b){
    var args = Array.prototype.slice.call(arguments, printParam.length);
    console.log(args);
  };

  printParam(1, 2, 3, 4);
  // 3,4;
  ```
- ES6
  ```javascript
  let printParam = function(a, b, ...args){
    console.log(args);
  };

  printParam(1, 2, 3, 4);
  // 3,4;
  ```

## 해체 할당
###### 배열 해체 할당
- ES6
  ```javascript
  let aRawData = ["A", "B", {key : "val"}];

  let [a, b, c] = aRawData;
  console.log(a); // "A"
  console.log(b); // "B"
  console.log(c); // Object {key: "val"}

  let [a, , c] = aRawData;
  console.log(a); // "A"
  console.log(c); // Object {key: "val"}

  let [a, …b] = aRawData;
  console.log(a); // "A"
  console.log(b); // ["B", Object]
  b[1].key; // "val"

  let [a, b, c, d = "D"] = aRawData;
  console.log(a); // "A"
  console.log(b); // "B"
  console.log(c); // Object {key: "val"}
  console.log(d); // "D"

  let [a, b, [c, d]] = [1, 2, [3, 4]];
  console.log(a); // 1
  console.log(b); // 2
  console.log(c); // 3
  console.log(d); // 4

  // 파라미터 기본 값에 해체 할당 사용시 함수 호출시 undefined넣으면 해체 할당이 적용되지만
  // printParam(1, 2) 넣으면 TypeError : undefined is not a function 발생
  let printParam = function([a, b, c = 3] = ["A", "B", "C"]){
    console.log(a, b, c);
  };

  printParam();
  // A B C
  ```

###### 객체 해체 할당
- ES6
  ```javascript
  let htDealInfo = {
    sName : "상품명",
    sSrl : 07110392,
    nPrice : 100000
  };

  // 객체의 키값과 변수명이 일치하면 해체시 키에 해당하는 값을 할당한다.
  let sName, sSrl, nPrice;
  ({sName, sSrl, nPrice} = htDealInfo);

  console.log(sName); // "상품명"
  console.log(sSrl); // 07110392
  console.log(nPrice); // 100000

  // 해체시 해체 대상 객체의 키와 동일한 키의 값을 할당한다.
  // 객체의 키와 다른 이름으로 받을 때 사용할 수 있다.
  let x, y, z;
  // let {sName : x, sSrl : y, nPrice : z} = htDealInfo;
  ({sName:x, nPrice:z, sSrl:y} = htDealInfo);

  console.log(x); // "상품명"
  console.log(y); // 07110392
  console.log(z); // 100000

  let defaultObjectParam = function({sTitle : "라면", sSrl : 0000, nPrice : 0 } = {}){
    console.log(sTitle, sSrl, nPrice);
  };

  defaultObjectParam();
  // 라면 0 0

  defaultObjectParam({sTitle : "생수", sSrl : 1387});
  // 생수 1387 0
  ```

## 화살표 함수
- ES6
  - 화살표 함수는 Function 생성자의 인스턴스로 구문, this값, new 연산자를 제외하면 일반 함수와 차이가 없다.
  - 화살표 함수는 객체 생성자로 사용할 수 없다.

  ```javascript
  let sumNum = (a, b) => { return a + b; };

  sumNum(1,2);
  // 3
  ```
  화살표함수 this값,
  - 컨텍스트는 현재 실행중인 코드를 소유한 객체의 참조값
  - 스코프는 어떤 함수를 호출할 때 마다 변수를 접근할 수 있는 범위
  - 자바스크립트에서는 내부 함수 호출 패턴을 정해 놓지 않아 함수 호출로 취급되어 함수 호출 패턴 규칙에 따라 this가 전역객체 window에 바인딩된다.

  ```javascript
  var object = {
    f1:function(){
      console.log(this);
      var f2 = function(){
        console.log(this);
      }
      f2();
      setTimeout(f2, 1000);
    }
  };

  object.f1();
  // Object window window

  var object = {
    f1:()=>{
      console.log(this);
      var f2 = () => {
        console.log(this);
      }
      f2();
      setTimeout(f2, 1000);
    }
  };

  object.f1();
  // window window window
  ```

## 메소드 정의

- ES6
  ```javascript
  let fnObj = {
    myfn(){ console.log("my") },
    urfn(){ console.log("your") }
  };
  ```
