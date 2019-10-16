# 18. 프로토타입

자바스크립트는 객체 기반의 프로그래밍 언어이며 자바스크립트를 이루고 있는 거의 "모든 것"이 객체이다. 



클래스 - 클래스와 생성자함수가 모두 프로토타입 기반의 인스턴스를 생성하지만 정확히 동일하게 동작하니느 않는다.



#### 객체지향 프로그래밍

프로그램을 명령어 또는 함수의 목록으로 보는 전통적인 명령형 프로그래밍의 절차지향적 관점에서 벗어나 프로그램을 여러개의 독립적 단위,즉 객체들의 집합으로 표현하려는 프로그래밍 패러다임을 말한다.어떠한 사물이나 개념을 이해할 때 **속성**을 본다.

그 중에 필요한 속성만을 간추려 내어 표현하는것을 **추상화**라한다.



이번에는 원이라는 개념을 객체로 만들어보자.원에는 반지름이라는 속성이 있다.이 반지름을 가지고 원의 지름,둘레,넓이를 구할 수 있다.이때 반지름은 원의 **상태를 나타내는 데이트**이며 원의 지름,둘레,넓이를 구하는 것은 **동작**이다.

```
const circle = {
  radius: 5,
  getDiameter(){
    return 2 * this.radius;
  },
  getPerimeter(){
    return 2 * Math.PI * this.radius;
  },
  getArea(){
    return Math.PI * Math.pow(this.radius, 2);
  }
};

console.log(circle);

console.log(circle.getDiameter()); //10
console.log(circle.getPerimeter()); //31.41592
console.log(circle.getArea()); //78.53981
```

이처럼 객체지향 프로그래밍은 객체의 상태를 나타내는 데이터와 상태 데이터를 조작할 수 있는 동작을 하나의 논리적인 단위로 묶어 생각한다.이때 **쌍태 데이터와 동작을 하나의 논리적인 단위로 묶은 복합적인 자료 구조를 객체라 한다**객체의 상태를 데이터를 프로퍼티,동자을 메소드라 부른다.



#### 상속과 프로토타입

상속은 객체지향 프로그램의 핵심개념으로 어떤 객체의 프로퍼티 또는 메소드를 다른 객체가 상속받아 그대로 사용할 수 있는 것을 말한다.

####  `__proto__`접근자 프로퍼티

**모든 객체는 `__proto__`접근자 프로퍼티를 통해 자신의 프로토타입,즉[[Prototype]]내부 슬롯에 접근할 수 있다.**



#### 내부 메소드`[[GetPrototypeOf]]와 [[SetPrototypeOf]]`

`get __proto__`은 [[GetPrototypeOf]]내부 메소드를 호출하여 자신의 프로토타입을 취득하고,set__proto__은 [[SetPrototypeOf]]내부 메소드를 호출하여 새로운 프로토타입을 할당한다.

| 리터럴표기법       | 셍성자함수 | 프로토타입         |
| ------------------ | ---------- | ------------------ |
| 객체 리터럴        | Object     | Object.protptype   |
| 함수 리터럴        | Function   | Function.prototype |
| 배열 리터럴        | Array      | Array.prototype    |
| 정규 표현식 리터럴 | RegExp     | RegExp.protptype   |

#### 생성자 정의 생성자 함수와 프로토타입 생성 시점

내부 메소드[[Construct]]를 갖는 함수 객체,즉 화살표 함수나 ES6의 메소드 축약표현으로 정의하지 않고 일반함수로 정의한 함수 객체는 new연산자와 함께 생성자 함수로서 호출할 수 있다.

생성자 함수로서 호출할 수 있는 함수,즉 construct는 함수 정의가 평가되어 함수 객체를 생성하는 시점에 프로토타입도 더불어 생성된다.



#### 빌트인 생성자 함수와 프로토타입 생성 시점

Object, String, Number, Function, Array, RegExp, Date, Promise 등과 같은 빌트인 생성자 함수도 일반 함수와 마찬가지로 빌트인 생성자 함수가 생성되는 시점에 프로토타입이 생성된다. 모든 빌트인 생성자 함수는 전역 객체가 생성되는 시점에 생성된다. 전역 객체는 누구보다도 먼저 생성된다.전역 객체는 누구보다도 먼저 생성된다. 이때 빌트인 생성자 함수와 더불어 프로토타입이 생성된다. 생성된 프로토타입은 빌트인 생성자 함수의 prototype 프로퍼티에 바인딩된다.



#### 프로토타입 체인

자바스크립트는 객체의 프로퍼티에 접근하려고 할 때 해당 객체에 접근하려는 프로퍼티가 없다면 `__proto__`접근자 프로퍼티가 가리키는 링크를 따라 자신의 부모 역할을 하는 프로토타입의 프로퍼티를 순차적으로 검색한다.이것을 프로토타입체인이라고 한다



#### 캡슐화

캡슐화는 정보의 일부를 외부에 감추어 은닉하는 것을 말한다.즉 외부에 공개할 필요가 없는 구현의 일부를 외부에 노출되지 않도록 감추어 적절치 못한 접근으로부터 정부를 보로하고 객체간의 상호 의존성,즉 결합도를 낮추는 효과가 얻는다.



#### 오버라이딩과 프로퍼티 쉐도잉

**오버라이딩** - 상위 클래스가 가지고 있는 메소드를 하위 클래스가 재정의하여 사용하는 방식이다.

**오버로딩** - 함수의 이름은 동일하지만 매개변수의 타입 또는 개수가 다른 메소드를 구현하고 매개변수에 의해 메소드를 구별하여 호출하는 방식이다.자바스크립트는 오버로딩을 지원하지 않지만 arguments객체를 사용하여 구현할 수는 있다.



#### 프로토타입의 교체

프로토타입은 다른 임의의 객체로 변경할 수 있다.이것은 부모 객체인 프로토타입을 동적으로 변경할 수 있다는 것을 의미한다.이러한 특징을 활용하여 객체간의 상속 관계를 동적으로 변경할 수 있다.프로토타입은 생성자 함수 또는 인스턴스에 의해 교체할 수 있다.



#### 인스턴스에 의한 프로토타입의 교체

프로토타입은 생성자 함수의 prototype 프로퍼티 뿐만 아니라 인스턴스의 `__proto__` 접근자 프로퍼티로 접근할 수 있다. 따라서 인스턴스의 `__proto__ `접근자 프로퍼티를 통해 프로토타입을 교체할 수 있다.



#### instanceof 연산자

`객체 instanceof 생성자 함수`



#### object.create에 의한 직접 상속

Object.create 메소드는 명시적으로 프로토타입을 지정하여 새로운 객체를 생성한다. Object.create 메소드도 다른 객체 생성 방식과 마찬가지로 추상 연산 ObjectCreate를 호출한다.

- new연산자가 없이도 객체를 생성할 수 있다.
- 프로토타입을 지정하면서 객체를 생성할 수 있다.이때 생성자 함수와 프로토타입간의 링크가 파괴되지 않는다.
- 객체 리터럴에 의해 생성된 객체도 특정 객체를 상속받을 수 있다.

#### 프로퍼티 존재 확인

in연산자는 객체내에 프로퍼티가 존재하는지 여부를 확인한다.in연산자의 사용방법은 아래와 같다

```
//prp: 프로퍼티 키를 나타내는 문자열
//object: 객체로 평가되는 표현식

prop in object
```

```;
const person = {
	name:'Lee',
	address: 'Seoul'
};

// person 객체에 name프로퍼티가 존재한다.
console.log('name in person') //true
//person 객체에 address 프로퍼티가 존재한다.
console.log('address' in person) //true
//person 객체에 age 프로퍼티가 존재하지 않는다.
console.log('age' in person) //false
```

in 연산자는 확인 대상 객체(위 예제의 경우, person 객체)의 프로퍼티 뿐만 아니라 확인 대상 객체가 상속받은 모든 프로토타입의 프로퍼티를 확인하므로 주의하기 바란다. person 객체에는 toString이라는 프로퍼티가 없지만 아래의 실행 결과는 true이다.

```
console.log('toString' in person); //true
```

이는 in 연산자가 person 객체가 속한 프로토타입 체인 상에 존재하는 모든 프로토타입에서 toString 프로퍼티를 검색했기 때문이다. toString은 Object.prototype의 메소드이다.



Object.prototype.hasOwnProperty 메소드를 사용해도 객체의 프로퍼티의 존재 여부를 확인할 수 있다.

```
console.log(person.hasOwnProperty('name')); //true
console.log(person.hasOwnProperty('age')); //false
```

#### 프로퍼티 열거

객체의 모든 프로퍼티를 순회하며 열거하려면 for…in 문을 사용한다. for…in 문은 프로퍼티를 열거할 때 순서를 보장하지 않는다

````
for(변수선언문 in 객체) { ...}
````

```
const person = {
	name: 'Lee',
	address: 'Seoul'	
};

for(const prrp in person){
console.log(prop+ ':' + person[prop])
}

//name: Lee
//adress: Seoul
```

for…in 문은 in 연산자처럼 순회 대상 객체의 프로퍼티 뿐만 아니라 객체가 상속받은 모든 프로토타입의 프로퍼티를 열거한다. 하지만 위 예제의 경우, toString과 같은 Object.prototype의 프로퍼티가 열거되지 않는다.

```
// in 연산자는 객체가 상속받은 모든 프로토타입의 프토퍼티를 확인한다.
console.log('toString' in person) //true

//for...in문도 객체가 상속받은 모든 프로토타입의 프로퍼티를 열거한다.
//하지만 toString과 같은 Object.prototype의 프로퍼티가 열거되지 않는다.
for(const prop in person) {
console.log(prop + ':' + person[prop]);
}

//name: Lee
//adress: Seoul
```

 이는 toString 메소드가 열거할 수 없도록 정의되어 있는 프로퍼티이기 때문이다. 다시 말해, Object.prototype.string 프로퍼티의 프로퍼티 어트리뷰트 [[Enumerable]]의 값이 false이기 때문이다. 프로퍼티 어트리뷰트 [[Enumerable]]는 프로퍼티의 열거 가능 여부를 나타내며 불리언 값을 갖는다. 



for…in 문은 객체의 프로토타입 체인 상에 존재하는 모든 프로토타입의 프로퍼티 중에서 프로퍼티 어트리뷰트 [[Enumerable]]의 값인 ture인 프로퍼티를 순회하며 열거한다.

for....in문은 프로퍼티 키가 심볼인 프로퍼티는 열거하지 않는다.



# 19장 엄격 모드

#### strict mode란?

자바스크립트언어의 문법을 보다 엄격히 적용하여 기존에는 무시되던 오류를 발생시킬 가능성이 높거나 자바스크립트 엔진의 최적화 작업에 문제를 일으킬 수 있는 코드에 대해 명시적인 에러를 발생시킨다.



#### strict mode의 적용

strict mode를 적용하려면 전역의 선두 또는 함수 몸체의 선두에`use strict;`를 추가한다.전역의 선두에 추가하면 스크립트 전체에 strict mode가 적용된다.

```
'use strict'

function foo() {
	x = 10;
}
foo();
```

함수 몸체의 선두에 추가하면 해당 함수와 중첩된 내부 함수에 strict mode가 적용된다.

```
function foo() {
	'use strict';
	
	x = 10;
}
foo();
```

코드의 선두에 strict mode를 위치시키지 않으면 제대로 동작하지 않는다.

```
function foo() {
	x = 10;
	'use strict';
}
foo();
```

#### 전역에 strict mode를 적용하는 것은 피하자.

전역에 적용한 strict mode는 스크립트 단위로 적용된다.