# 2일차

## 인터페이스

- 인터페이스란 상호 간의 정의한 약속을 의미합니다. 타입스크립트에서는 다음과 같은 약속들을 정의할 수 있습니다.
    - 객체의 스펙(속성과 속성의 타입)
    - 함수의 스펙(파라미터와 반환 값의 타입)
    - 배열과 객체에 접근하는 방식
    - 클래스

## 인터페이스의 사용
- 함수의 스펙을 정의할 때에도 인터페이스를 사용할 수 있습니다. 하지만 인터페이스를 적용하지 않아도 같은 역할을 하는 코드를 작성할 수 있는데요. 이 둘의 차이를 알아보기 위해 인터페이스를 적용하기 전과 후를 비교해봅시다.

- [인터페이스 적용 전]
```js
const person = { name: 'mukeunzi', age: 12 }; // 객체 선언

function logAge (obj: { name: string }) {
    console.log(obj.name);
}

logAge(person); // mukeunzi
```
- [인터페이스 적용 후] 
```js
interface personData {
    name: string;
}

function logAge(obj: personData) {
    console.log(obj.name);
}

const person = { name: 'mukeunzi', age: 21 };
logAge(person); // mukeunzi
```
- 인터페이스를 적용하니 파라미터가 좀 더 명시적으로 바뀌었습니다. 객체의 속성들이 많을 수록 인터페이스를 사용하는 것이 더 장점으로 다가올 것 같습니다. 객체의 속성이 5개 이상일 때를 생각해봅시다. 인터페이스를 사용하지 않는다면 함수 선언부에 파라미터 스펙을 정의하기 위해 많은 코드를 작성해야 할 것 입니다. 하지만 인터페이스를 사용한다면 보다 간결하게 스펙을 정의할 수 있습니다.
- 위 코드를 통해 한 가지를 더 알 수 있습니다. 인터페이스를 인자로 받아 사용할 때, 인터페이스 속성의 개수와 인자로 받는 객체 속성의 개수가 항상 일치하지 않아도 된다는 것입니다. 다시 말해, 인터페이스에 정의된 속성, 타입의 조건을 만족한다면 인자로 받는 속성의 개수가 더 많아도 된다는 의미입니다. 위 예시에서는 `interface personData`에 `name: string;` 속성만 정의되어 있습니다. 때문에 `logAge(obj: personData)` 함수를 호출할 때 파라미터로 인터페이스에 정의된 `name: string` 값만 전달한다면, 정의되지 않은 속성(`age`)을 포함시켜 전달해도 상관 없다는 의미입니다.(=인터페이스에 정의된 속성은 꼭 포함시켜 전달해야 합니다.)

## 옵션 속성
- 위에서 인터페이스에 정의된 속성은 꼭 포함시켜 전달해야 한다고 했습니다. 하지만 옵션 속성을 사용하면 정의되어 있는 속성을 모두 사용하지 않아도 됩니다. `?` 키워드를 사용합니다.
```js
interface SeoulSubway {
    line: number,
    lastStop?: string
}

const mySubway = {
    line: 7
};

function goToWork (subway: SeoulSubway) {
    console.log(subway.line);
}

goToWork(mySubway); // 7
```
- `goToWork()` 함수에서 인자의 타입을 `SeoulSubway`로 선언했습니다. 함수를 호출할 때 `line` 값만 전달해도 오류가 발생하지 않습니다. `lastStop` 속성은 옵션 속성(`?`)으로 선언했기 때문입니다.
- 옵션 속성의 장점은 인터페이스 속성을 선택적으로 사용할 수 있다는 것 뿐만 아니라, 정의되어 있지 않은 속성에 대해서 인지시켜줄 수 있다는 점 입니다. 위 예시에서 인터페이스에 정의되어 있지 않는 속성에 접근한다면 오류를 표시합니다. 

## 읽기 전용 속성
- 읽기 전용 속성이란, 인터페이스로 객체를 처음 생성할 때만 값을 할당하고 그 이후에는 변경할 수 없는 속성을 의미합니다. `readonly` 키워드를 사용합니다.
```js
interface DobongBus {
    readonly busNumber: string;
}

const myBus: DobongBus {
    busNumber: 146
}
myBus.busNumber = 5516; // error!
```
- js에서 const 키워드로 primitive type 변수를 선언했을 때와 같다고 생각하면 될 것 같습니다. 

## 읽기 전용 배열
- `ReadonlyArray<T>` 타입을 사용하면 읽기 전용 배열을 생성할 수 있습니다.
```js
const arr: Readonly<number> = [1, 2, 3];
arr.push(4); // error
arr[0] = 0; // error
```
- 위처럼 배열을 ReadonlyArray로 선언하면 배열의 내용을 변경할 수 없습니다. 선언한 시점에만 값을 정의할 수 있으니 유의해야 합니다.