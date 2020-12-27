# 1일차 

## 타입스크립트 기초(변수와 함수 타입 정의하기)

- ts에는 총 12가지의 타입이 있다. 기본타입, 함수타입에 대해 정리한다.

## 기본 타입 - string, number, array
- 다음은 `string, number, array` 타입의 변수를 선언하는 방식이다.

```js
const str: string = 'hello ts'; // string
const num: number = 10; // number
const arrNum: Array<number> = [1, 2, 3]; // array[number]
const arrStr: Array<string> = ['na', 'eun', 'ji']; // array[string]
const arrStrLiteral: string[] = ['hot', 'dog']; // 리터럴 방식의 선언방법 array[string] 
```

## 기본 타입 - tuple, object, boolean
```js
const address: [string, number] = ['seoul', 1000] // tuple. 배열 타입의 확장으로, 인덱스 별로 타입을 지정할 수 있음. 모든 인덱스의 타입이 정의되어 있는 배열을 튜플이라 함.
const obj: object = {}; // object
const person: { name: string, age: number} = {
    name: 'mukeunzi', age: 10
} // object 속성의 타입들도 정의할 수 있음. object을 구체적으로 정의하는 방법.
const hidden: boolean = true; // boolean
```

## 함수 타입 - parameter, return value
- 함수의 파라미터, 반환 값에 타입을 정의할 수 있다.
```ts
function sum(a: number, b: number): number {
    return a + b;
}
```
- 함수를 호출할 때 파라미터의 개수나 타입이 함수의 스펙에 어긋날 경우 오류를 출력낸다. 아래는 위에서 선언한 `sum()`함수를 호출할 때 필요 이상의 파라미터를 넘겨 오류를 출력하는 경우이다.
```ts
sum(10, 20, 30, 40);
```
- ts에서는 `?` 연산자를 사용해 optional parameter를 사용할 수 있다. 
```ts
function log(a: string, b?: string) {
    console.log(a, b);
}

log('hot dog'); // 두 번째 파라미터는 optional이기 때문에 전달하지 않아도 오류가 출력되지 않는다.
log('hot dog', 'cj'); // 두 개의 파라미터를 전달할 수 있다.
```
