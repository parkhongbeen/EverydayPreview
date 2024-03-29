# 제어문

#### 블록문

0개 이상의 문을 중괄호로 묶은것으로 코드 블록 또는 블록이라고 부르기도 한다.

----

#### 조건문

주어진 조건식의 평가 결과에 따라 코드 블럭의 실행을 결정한다.조건식은 불리언 값으로 평가될 수 있는 표현식이다

----

#### if...else문

주어진 조건식의 평가 결과,즉 논리적 참,거짓에 따라 실행할 코드 블록을 결정한다.

````
if (조건식) {
  // 조건식이 참이면 이 코드 블록이 실행된다.
} else {
  // 조건식이 거짓이면 이 코드 블록이 실행된다.
}
````

----

#### switch문

switch 문은 주어진 표현식을 평가하여 그 값과 일치하는 표현식을 갖는 case 문으로 실행 순서를 이동시킨다. case 문은 상황(case)을 의미하는 표현식을 지정하고 콜론으로 마친다. 그리고 그 뒤에 실행할 문들을 위치시킨다.

````
switch (표현식) {
  case 표현식1:
    switch 문의 표현식과 표현식1이 일치하면 실행될 문;
    break;
  case 표현식2:
    switch 문의 표현식과 표현식2가 일치하면 실행될 문;
    break;
  default:
    switch 문의 표현식과 일치하는 표현식을 갖는 case 문이 없을 때 실행될 문;
}
````

----

#### 반복문

주어진 조건식의 평가 결과가 참인 경우 코드 블럭을 실행한다.그 후 조건식을 다시 검사하여 여전히 참인 경우 코드 블록을 다시 실행한다.이는 조건식이 거짓일 떄까지 반복한다.

----

#### for문

조건식이 거짓으로 판별될 때까지 코드 블록을 반복 실행한다.가장 일반적으로 사용되는 반복문의 형태는 아래와 같다.

````
for (변수 선언문 또는 할당문; 조건식; 증감식) {
  조건식이 참인 경우 반복 실행될 문;
}
````

----

#### while문

주어진 조건식의 평가 결과가 참이면 코드 블록을 계속해서 반복 실행한다. 조건문의 평가 결과가 거짓이 되면 실행을 종료한다. 만약 조건식의 평가 결과가 불리언 값이 아니면 불리언 값으로 강제 변환되어 논리적 참, 거짓을 구별한다

````
var count = 0;

// count가 3보다 작을 때까지 코드 블록을 계속 반복 실행한다.
while (count < 3) {
  console.log(count);
  count++;
} // 0 1 2		
````

----

#### do while문

코드블록을 먼저 실행하고 조건식을 평가한다.따라서 코드 블록은 무조건 한번 이상 실행된다.

```
var count = 0;

// count가 3보다 작을 때까지 코드 블록을 계속 반복 실행한다.
do {
  console.log(count);
  count++;
} while (count < 3); // 0 1 2

```

----

#### break문

break 문은 코드 블록을 탈출한다. 좀 더 정확히 표현하자면 코드 블록을 탈출하는 것이 아니라 레이블 문, 반복문(for, for…in, for…of, while, do…while) 또는 switch 문의 코드 블록을 탈출한다.

----

#### continue문

반복문의 코드 블록 실행을 현 지점에서 중단하고 반복문의 증감식으로 이동한다. break 문처럼 반복문을 탈출하지는 않는다. 

----

# 타입변환과 단축평가

자바스크립트의 모든 값은 타입이 있다.값의 타입은 개발자의 의도에 의해 다른 타입으로 변화할 수 있다. 개발자가 의도적으로 값의 타입을 변화하는 것을 **명시적 타입 변환**또는 **타입 캐스팅**이라 한다

----

동적 타입 언어인 자바스크립트는 개발자의 의도와는 상관없이 자바스크립트 엔진에 의해 암묵적으로 타입이 자동 변환되기도 한다. 이를 **암묵적 타입 변환** 또는 **타입 강제 변환(Type coercion)**이라고 한다.

----

#### 암묵적 타입 변환

자바스크립트 엔진은 표현식을 평가할 떄 코드의 문맥을 고려하여 암묵적 타입 변환을 실행한다.

````
// 피연산자가 모두 문자열 타입이여야 하는 문맥
'10' + 2  // '102'

// 피연산자가 모두 숫자 타입이여야 하는 문맥
5 * '10'  // 50

// 피연산자 또는 표현식이 불리언 타입이여야 하는 문맥
!0 // true
if (1) { }
````

----

#### 문자열 타입으로 변환

`ex) 1 + '2' // "12"`

위 예제의 + 연산자는 피연산자 중 하나 이상이 문자열이므로 문자열 연결 연산자로 동작한다. 문자열 연결 연산자의 역할은 문자열 값을 만드는 것이다. 따라서 문자열 연결 연산자의 모든 피연산자는 코드의 문맥 상 모두 문자열 타입이여야 한다.

----

#### 숫자 타입으로 변환

````
1 - '1'    // 0
1 * '10'   // 10
1 / 'one'  // NaN
````

위 예제에서 사용한 연산자는 모두 산술 연산자이다. 산술 연산자의 역할은 숫자 값을 만드는 것이다. 따라서 산술 연산자의 모든 피연산자는 코드의 문맥 상 모두 숫자 타입이여야 한다.

----

#### 불리언 타입으로 변환

````
if ('') console.log(x);
````

if 문이나 for 문과 같은 제어문 또는 삼항 조건 연산자의 조건식(conditional expression)은 불리언 값, 즉 논리적 참, 거짓을 반환해야 하는 표현식이다. 자바스크립트 엔진은 조건식의 평가 결과를 불리언 타입으로 암묵적 타입 변환한다.

----

#### 명시적 타입 변환

개발자의 의도에 의해 명시적으로 타입을 변경하는 방법은 다양하다.표준 빌트인 생성자 함수를 new연산자 없이 호출하는 방법과 자바스크립트에서 제공하는 빌트인 메소드를 사용하는 방법,그리고 앞에서 살펴본 암묵적 타입 변환을 이용하는 방법이 있다.

----

#### 문자열 타입으로 변환

- String 생성자 함수를 new 연산자 없이 호출하는 방법
- Object.prototype.toString 메소드를 사용하는 방법
- 문자열 연결 연산자를 이용하는 방법

----

#### 숫자타입으로 변환

- Number 생성자 함수를 new 연산자 없이 호출하는 방법
- parseInt, parseFloat 함수를 사용하는 방법(문자열만 숫자 타입으로 변환 가능)
- \+ 단항 연결 연산자를 이용하는 방법
- \* 산술 연산자를 이용하는 방법

----

#### 단축평가

```javascript
'Cat' && 'Dog' // 'Dog'
```

Cat은 true이기 때문에 뒤에 값이 Dog에 의해서 불리언값이 평가된다.

두번째 피연산자 ‘Dog’은 Truthy 값이므로 true로 평가된다. 이때 두개의 피연산자가 모두 true로 평가되었다. 이때 논리곱 연산의 결과를 결정한 것은 두번째 피연산자 ‘Dog’다.

논리곱 연산자 `&&`는 논리 연산의 결과를 결정하는 두번쨰 피연산자 즉,문자열'Dog'를 그대로 반환한다.

| 단축 평가 표현식  | 평가 결과 |
| ----------------- | --------- |
| true\|\|anything  | true      |
| false\|\|anything | anything  |
| true&anything     | anything  |
| false&&anything   | false     |

````
// 논리합(||) 연산자
'Cat' || 'Dog'  // 'Cat'
false || 'Dog'  // 'Dog'
'Cat' || false  // 'Cat'

// 논리곱(&&) 연산자
'Cat' && 'Dog'  // Dog
false && 'Dog'  // false
'Cat' && false  // false
````

