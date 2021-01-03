# 7일차

## 유니온 타입과 인터섹션 타입(Union Types, Intersection Types)

### 유니온 타입
- 유니온 타입이란 여러개의 타입을 구성할 수 있는 방법 중 하나입니다.
- `any`키워드를 사용하지 않고, OR연산자를 사용해 여러개의 타입을 지정할 수 있습니다.
- 매개변수가 숫자 또는 문자열으로 예상되는 라이브러리를 마주할 때가 있는데요. 이때 유니온 타입을 어떻게 사용할 수 있을지 알아보겠습니다. 
- 먼저 `any`키워드를 사용한 예시를 먼저 살펴보겠습니다.
```js
/**
 * 문자열 value가 주어지면, 왼쪽에 padding을 붙여 리턴하는 함수입니다.
 * padding이 문자열이면, padding을 value 왼쪽에 붙입니다.
 * padding이 숫자이면, padding만큼의 공백을 왼쪽에 붙입니다.
 */
function padLeft(value: string, padding: any) {
  if (typeof padding === "number") {
    return Array(padding + 1).join(" ") + value;
  }
  if (typeof padding === "string") {
    return padding + value;
  }
  // (참고)위와 같이 if문으로 타입을 체크하는 방식을 타입 가드라고 합니다. 
  // (참고)타입 가드란 특정 타입으로 타입의 범위를 좁혀나가는 과정을 말합니다.
  throw new Error(`Expected string or number, got '${typeof padding}'.`);
}

padLeft("Hello", 4); // 결과 : "    Hello"
padLeft("Hello", "Hi"); // 결과 : "HiHello"
```
- 위 코드에서는 `padding`타입을 `any`로 선언했고, 문제없이 작동합니다. 하지만 위 함수는 `padding`의 타입이 숫자이거나 문자가 아닐 경우에는 예외를 발생시킵니다.
- `padLeft("Hello", true);`를 호출했다고 가정해봅시다. 컴파일 시에는 오류가 발생하지 않지만 런타임 시에 오류가 발생합니다. 
- 위 코드에 유니온 타입을 사용하면 컴파일 시에 오류를 컴파일 전에 알 수 있습니다. 유니온 타입을 사용해 위 함수를 수정해보겠습니다.
```js
/**
 * 문자열 value가 주어지면, 왼쪽에 padding을 붙여 리턴하는 함수입니다.
 * padding이 문자열이면, padding을 value 왼쪽에 붙입니다.
 * padding이 숫자이면, padding만큼의 공백을 왼쪽에 붙입니다.
 */
function padLeft(value: string, padding: number | string) {
  if (typeof padding === "number") {
    return Array(padding + 1).join(" ") + value;
  }
  if (typeof padding === "string") {
    return padding + value;
  }
  throw new Error(`Expected string or number, got '${typeof padding}'.`);
}

padLeft("Hello", 4); // 결과 : "    Hello"
padLeft("Hello", "Hi"); // 결과 : "HiHello"
padLeft("Hello", true); // 컴파일 오류
```
- `padding`의 타입을 유니온 타입으로 지정했습니다. 따라서 `number | string`이 아닌 값을 전달하면 컴파일 시에 오류를 발생시켜 런타임 에러를 방지할 수 있습니다.
- 유니온 타입은 여러 타입 중 하나일 수 있는 값을 나타냅니다. OR 연산자와 비슷하며, 각 타입을 구분짓기 위해 `|`를 사용합니다.
- 하나 이상의 타입을 사용하고 싶을 때 사용하면 됩니다.

### 유니온 타입의 장점
- 여러 개의 타입을 사용해야할 때 유니온 타입을 사용하면 ts의 Intellisense기능을 사용할 수 있습니다.
- 예시 코드를 살펴보겠습니다.
```js
// any를 사용하는 경우
function getPrice(price: any) {
  return price.toLocaleString(); // number 타입에서 사용할 수 있는 메소드가 자동완성 되지 않음.
}

// 유니온 타입을 사용하는 경우
function getPrice(price: number | string) {
  if (typeof price === "number") {
    return price.toLocaleString(); // price가 number값으로 추론되기 때문에, number 타입에서 사용할 수 있는 메소드 자동완성 됨.
  }
  if (typeof price === "string") {
    return price.toLocaleString();
  }
}
```

### 유니온 타입의 특징
- 인터페이스에서 유니온 타입을 사용할 때 특징에 대해 살펴보겠습니다. 
```js
interface Person {
  name: string;
  age: number;
}

interface Developer {
  name: string;
  skill: string;
}

function hey(someone: Person | Developer) {
  console.log(someone.name); // 정상 동작
  console.log(someone.age); // 오류
  console.log(someone.skill); // 오류
}
```
- 유니온 타입을 사용할 때는 공통된 속성에만 접근할 수 있습니다. 때문에 함수에서는 `Person, Developer`인터페이스의 공통 속성인 `name`에만 정상적으로 접근할 수 있고, 다른 속성에는 접근할 수 없습니다. 
- 어떤 타입의 파라미터가 들어와도 오류가 발생하지 않도록 하기 위해서 입니다. 공통 속성이 아닌 값에 접근하고 싶다면 타입 가드 방식을 사용해야 합니다.

### 인터섹션 타입 소개
- 인터섹션 타입은 여러 타입을 모두 만족하는 타입을 의미합니다. `&`연산자를 사용합니다.
- 위 `Person, Developer` 인터페이스 예시에 인터섹션을 적용해보겠습니다.
```js
interface Person {
  name: string;
  age: number;
}

interface Developer {
  name: string;
  skill: string;
}

function hey(someone: Person & Developer) {
  console.log(someone.name); // 정상 동작
  console.log(someone.age); // 정상 동작
  console.log(someone.skill); // 정상 동작
}
```
- `someone`파라미터의 타입을 인터섹션으로 설정했습니다. 유니온 타입과 달리 인터섹션 타입은 공통되지 않은 속성에도 모두 접근할 수 있습니다. 
- 따라서 `someone`은 두 인터페이스의 속성을 모두 포함하는 타입입니다.
- 유니온 타입은 교집합인 속성만 접근할 수 있는 반면, 인터섹션 타입은 합집합 속성에 모두 접근 가능합니다.
