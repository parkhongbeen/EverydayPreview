## 객체란?

자바스크립트는 객체기반의 프로그래밍언어이며 자바스크립트를 이루고 있는 거의 "모든 것"이 객체이다.원시타입을 제외한 나머지 값들은 모두 객체이다.

**원시타입의값,즉 원시값은 변견 불가능한 값**이지만 **객체 타입의 값,즉 객체는 변경가능한 값**이다.



자바스크립트의 객체는 키와 값으로 구성된 프로퍼티들의 집합이다.

프로퍼티값이 함수일 경우,일반 함수와 구분하기 위해 메소드라 부른다.

- 프로퍼티:객체의 상태를 나타내는 값
- 메소드:프로퍼티를 참조하고 조작할 수 있는 동작



### 객체 리터럴에 의한 객체 생성

c++과 java와 같은 클래스 기반 객체지향 언어는 클래스를 사전에 정의하고 필요한 시점에 new연사자와 함께 생성자를 호출하여 인스턴스를 생성하는 방식으로 객체를 생성한다.

- 객체 리터럴

- object생성자 함수

- 생성자 함수

- Object.create 메소드

- 클래스(ES6)

  **이중에서 가장 일반적이고 간단한 방법은 객체리터럴을 사용하는 방법이다.**

### 프로퍼티

객체는 프로퍼티들의 집합이며 프로퍼티는 **키와 값**으로 구성된다.

프로퍼티를 나열할 떄는 쉼표(,)로 구분한다.

- 프로퍼티 키 : 빈 문자열을 포함하는 모든 문자열 또는 symbol값
- 프로퍼티 값 : 자바스크립트에서 사용할 수 있는 모든 값

### 메소드

프로퍼티값이 함수일 경우,일반 함수와 구분하기 위해 메소드라 부른다.즉 메소드는 객체에 제한되어 있는 함수를 의미한다.



### 프로퍼티 접근

프로퍼티값에 접근하려면 마침표(.)를 사용하는 **마침표 표기법**또는 **대괄호([...])**를 사용하는 대괄호 표기법을 사용한다.

대괄호 표기법을 사용하는 경우,**대괄호 내부에 지정하는 프로퍼티키는 반드시 따옴표로 감싼 문자열이어야 한다.**자바스크립트 엔진은 대괄호 내의 따옴표로 감싸지 않은 이름을 프로퍼티 키로 인식하지 않고 식별자로 취급한다.



### 프로퍼티 값 갱신

이미 존재하는 프로퍼티에 값을 할당하면 프로퍼티 값이 갱신된다.



### 프로퍼티 동적 생성

존재하지 않은 프로퍼티에 값을 할당하면 프로퍼티가 동적으로 생성되어 추가되고 프로퍼티 값이 할당된다.



### 프로퍼티 삭제

delete연산자는 객체의 프로퍼티를 삭제한다.이때 delete연산자의 피연자는 프로퍼티 값에 접근할 수 있는 표현식이어야 한다.만약 존재하지 않는 프로퍼티를 삭제하면 아무런 에러없이 무시된다.

### ES6에서 추가된 객체 리터럴의 확장 기능

ES6에서는 더욱 간편하고 표현력 있는 객체 리터럴의 확장기능을 제공한다.

### 프로퍼티축약표현

객체 리터럴의 프로퍼티는 프로퍼티 키와 프로퍼티 값으로 구성된다. 프로퍼티의 값은 변수에 할당된 값, 즉 식별자 표현식일 수도 있다.

### 프로퍼티키 동적 생성

문자열 또는 문자열로 변환 가능한 값을 반환하는 표현식을 사용해 프로퍼티 키를 동적으로 생성할 수 있다. 단, 프로퍼티 키로 사용할 표현식을 대괄호([…])로 묶어야 한다. 이를 계산된 프로퍼티 이름(Computed property name)이라 한다.

### 메소드 축약 표현

ES6에서는 메소드를 정의할 때, function 키워드를 생략한 축약 표현을 사용할 수 있다.



## 10장 원시 값과 객체의 비교

### 원시값 

변경 불가능한 값이다.변수의 값을 변경하기 위해 원시값을 재할당하면 새로운 메모리 공간을 확보하고 재할당한 값을 저장한 후, 변수가 참조하던 메모리 공간의 주소를 변경한다.원시 값의 이러한 특성을 **불변성**이라 한다.



### 객체

객체는 프로퍼티의 개수가 정해져있지 않으며 동적으로 추가되고 삭제할 수 있다.



### 참조에 의한 전달

```
var person = {
  name: 'Lee'
};

var copy = person;
```

객체를 가리키는 변수를 다른 변수에 할당하면 원본의 참조값이 복사되어 전달된다.이를 **참조에 의한 전달**이라고 한다.