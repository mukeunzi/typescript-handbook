# 4일차

## 인터페이스의 활용

### 함수 스펙에 인터페이스 활용
- 함수의 스펙(파라미터, 리턴 타입)을 인터페이스로 정의할 수 있습니다. 예시 먼저 살펴보겠습니다.
```js
interface SumFunction {
    (a: number, b: number): number;
}

const sum: SumFunction = function (a: number, b: number): number {
    return a + b;
}
```
- `SumFunction`인터페이스에 함수의 스펙을 정의했습니다. 괄호 안에 파라미터의 개수와 타입을, 우측엔 함수의 리턴 타입에 대해 정의합니다. `SumFunction`인터페이스를 사용하는 함수는 `number` 타입의 두 개의 파라미터를 입력받아야 하고, `number` 타입으로 리턴 값을 설정해야 합니다.
- `SumFunction`인터페이스를 사용한 `sum`은 인터페이스의 규격에 맞추어 함수를 선언합니다.

### 인덱싱 방식을 정의하는 인터페이스
- 인터페이스로 인덱싱 방식을 지정할 수 있습니다. 예시 먼저 살펴보겠습니다.
```js
interface StringArray {
    [index: number]: string;
}

const arr: StringArray = ['a', 'b', 'c', 'd'];
arr[0] = 10; // 오류
```
- `StringArray`인터페이스를 사용하는 `arr` 배열을 생성했습니다. 배열의 접근할 때에는 `number` 타입의 인덱스로 접근해야 하고, 배열의 값은 항상 `string`이어야 합니다.

### 인터페이스 딕셔너리 패턴
- 딕셔너리 패턴은 인덱싱 방식의 인터페이스와 비슷합니다. 예시를 살펴보며 딕셔너리 패턴 인터페이스에 대해 알아보겠습니다.
```js
interface StringRegexDictionary {
    [key: string]: RegExp
}

const obj: StringRegexDictionary = {
    cssFile: /\.css$/,
    jsFile: /\.js$/
}

obj['cssFile'] = 'a'; // 정규표현식(RegExp)이 아닌 string을 할당했기 때문에 오류 발생
obj['ts'] = /\.ts$/; // 정상 동작

Object.keys(obj).forEach(value => { // value 타입 추론 가능
    console.log(value);
})
```
- 위 `StringRegexDictionary`는 필드 명이 string 타입이고, 값은 정규표현식(`RegExp`) 타입인 인터페이스 입니다. 위 규격을 지켜 `obj`변수에 값을 할당해야 합니다. 
- 인터페이스를 사용하면 규격에 맞지 않는 데이터가 추가되는 것을 방지할 수 있습니다.
- `Object.keys()` 메소드에서 확인할 수 있듯이, 인터페이스를 사용하면 타입 추론이 가능해 값을 유추할 수 있습니다.