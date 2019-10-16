# 20. 전역 객체

전역 객체는 코드가 실행되기 이전 단계에 자바스크립트 엔진에 의해 생성되는 특수한 객체이다. 전역 객체는 클라이언트 사이드 환경(브라우저)에서는 window, 서버 사이드 환경(Node.js)에서는 global 객체를 의미한다.

- 전역객체는 개발자가 의도적으로 생성할 수 없다.
- 전역 객체의 프로퍼티를 참조할 때 window를 생략할 수있다.

let이나 const키워드로 선언한 전역 변수는 전역 객체 window의 프로퍼티가 아니다.

let이나 const키워드로 선언한 전역 변수는 보이지 않는 개념적인 블록내에 존재하게 된다.



#### Infinity

Infinity 프로퍼티는 양/음의 무한대를 나타내는 숫자값 Infinity를 갖는다.(+자바스크립트는 대소문자를 구분하는 언어이기때문에 맨 앞자리 i는 대문자I로 기재한다.)



#### NaN

NaN프로퍼티는 숫자가 아님(Not-a-Number)을 나타내는 숫자값 NaN을 갖는다.NaN프로퍼티는 Number.NaN프로퍼티와 같다.

```
console.log(window.NaN); //NaN
console.log(Number('abc')); //NaN
console.log(1 * 'string'); //NaN
console.log(typeof NaN); //number
```



#### undefined

undefuned 프로퍼티는 원시타입 undefined를 값으로 갖는다.

```
console.log(window.undefined); // undefined

var foo;
console.log(foo); //undefined
console.log(typeof undefined); //undefined
```



#### 빌트인 전역함수

###### eval

문자열을 코드로 인식하게 해주는 함수

전달된 문자열 코드가 여러 개의 문으로 이루어져 있다면 모든 문을 실행 후 마지막 결과값을 반환한다.

##### isFinite

매개 변수에 전달된 값이 정상적인 유한수인지 검사하여 그 결과를 불리언 타입으로 반화한다.매개변수에 전달된 값이 숫자가 아닌 경우,숫자로 타입을 변화한 후 검사를 수행한다.

##### isNaN

매개변수에 전달된 값이 NaN인지 검사하여 그 결과를 불리언 타입으로 반환한다.매개변수에 전달된 값이 숫자가 아닌 경우,숫자로 타입을 변화한 후 검사를 수행한다.

##### parseFloat

매개변수에 전달된 문자열을 부동소수점 숫자로 변화하여 반환한다.

##### parselnt

매개변수에 전달된 문자열을 정수형 숫자로 해석하여 반환한다.반환값은 언제나 10진수다.

###### encodeURI / decodeURI

encodeURI 함수는 매개변수로 전달된 URI를 인코딩한다. URI는 인터넷에 있는 자원을 나타내는 유일한 주소를 말한다. URI의 하위개념으로 URL, URN이 있다.



# 21. this

동작인 메소드는 자신이 속한 객체의 상태를 나타내는 데이터인 상태 데이터,즉 프로퍼티를 참조하고 상태를 변경할 수 있어야 한다.이때 메소드가 자신이 속한 객체으 ㅣ프로퍼티를 참조하려면 먼저 **자신이 속한 객체를 가리키는 식별자를 참조할 수 있어야 한다.**

**this는 객체 자신의 프로퍼티나 메소드를 참조하기 위한 자기 참조 변수이다.**

전역에서 this는 전역객체 window를 가리킨다.

```
console.log(this) //전역에서 this는 전역객체 window를 가리킨다.

function sqiare(number) {
  
  console.log(this); //window
  return number * number;
}
square(2);

const person = {
  name: 'Lee',
  getName() {
    // 메소드 내부에서 this는 메소드를 호출한 객체를 가리킨다.
    console.log(this); //{name: "Lee", getName: f}
    return this.name;
  }
};
console.log(person.getName()); //Lee

function Person(name) {
  //생성자 함수 내부에서 this는 생성자 함수가 생성항 인스턴스를 가리킨다.
  console.log(this);
  this.name = name;
}

const me = new Person('Lee');
```

#### 함수 호출 방식과 this 바인딩

this가 가리키는 값,즉 this 바인딩은 함수의 호출 방식,즉 함수가 어떻게 호출되었는지에 따라 동적으로 결정된다.

````
// this에 바인딩될 객체는 함수 호출 방식에 따라 동적으로 결정된다.
const foo = function () {
  console.dir(this);
};

// 동일한 함수도 다양한 방식으로 호출할 수 있다.

// 1. 일반 함수 호출
// foo 함수를 일반적인 방식으로 호출
// this는 전역 객체 window를 가리킨다.
foo(); // window

// 2. 메소드 호출
// foo 함수를 프로퍼티의 값으로 할당하여 호출
// this는 메소드를 호출한 객체 obj를 가리킨다.
const obj = { foo };
obj.foo(); // obj

// 3. 생성자 함수 호출
// foo 함수를 new 연산자와 함께 생성자 함수로 호출
// this는 생성자 함수가 생성한 인스턴스를 가리킨다.
new foo(); // foo {}

// 4. Function.prototype.apply/call/bind 메소드에 의한 간접 호출
// this는 인수에 의해 결정된다.
const bar = { name: 'bar' };

foo.call(bar);   // bar
foo.apply(bar);  // bar
foo.bind(bar)(); // bar
````

