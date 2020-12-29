# 3일차

## 이넘(Enums)
- 이넘은 특정 값들의 집합을 의미하는 자료형입니다. ts에서는 숫자형 이넘과 문자형 이넘을 지원합니다.

### 숫자형 이넘
- 숫자형 이넘에서는 초기 값을 선언할 수도, 않을 수도 있습니다. 
- 예시를 먼저 살펴보겠습니다.
```js
// [초기 값 선언 X]
enum Direction {
    Up, // 0
    Down, // 1
    Left, // 2
    Right // 3
}

// [초기 값 선언 O]
enum Direction {
    Up = 1,
    Down, // 2
    Left, // 3
    Right // 4
}
```
- 초기 값을 선언하지 않으면 0부터 차례로 1씩 증가됩니다. 따라서 `Up, Down, Left, Right`에는 순서대로 `0, 1, 2, 3`가 할당됩니다.
- 첫번째 값에 초기 값을 선언하면, 초기 값을 기준으로 1씩 증가됩니다. 따라서 `Down, Left, Right`에는 순서대로 `2, 3, 4`가 할당됩니다.

- 숫자형 이넘은 아래와 같이 사용할 수 있습니다.
```js
enum Response {
    No = 0,
    Yes = 1
}

function question(answer: Response): void {
    console.log(answer);
}

question(Response.Yes);
```

- 숫자형 이넘에서 주의할 점은 선언할 때 이넘 값에 다른 이넘 타입의 값을 사용하면, 선언하는 첫번째 값에 초기화를 해줘야 한다는 점입니다.

### 문자형 이넘
- 문자형 이넘은 숫자형 이넘과 개념적으로는 거의 비슷합니다. 다만, 런타임에서 미세한 차이가 있습니다. 
- 문자형 이넘은 auto-incrementing이 없습니다. 때문에 이넘 값 전부 특정 문자 또는 다른 이넘 값으로 초기화 해줘야 합니다.
```js
enum Direction {
    Up = "UP",
    Down = "DOWN",
    Left = "LEFT",
    Right = "RIGHT"
}
```

### 복합 이넘(Heterogeneous Enums)
- 문자와 숫자를 혼합해 생성한 이넘을 복합 이넘이라고 합니다. 가능하긴 하지만 권고되는 방법은 아닙니다. 같은 타입으로 이루어진 이넘을 권장합니다. 

### 런타임 시점에서의 이넘 특징
- 예시를 먼저 살펴보겠습니다. 
```js
enum Alphabet {
    A, B, C
}

function getAlphabet (obj: { B: number }) {
    return obj.B;
}
getAlphabet(Alphabet); // 1
```
- 위 코드에서 이넘 `Alphabet`에 `A, B, C`는 차례로 `0, 1, 2`가 할당됩니다. `B`에는 `number`타입이 할당되기 때문에 함수를 호출할 때 이넘 값을 넘겨 호출해도 1을 출력하며 정상 종료됩니다. 런타임 시에 이넘은 객체 형태로 존재하는 특징이 있기 때문입니다. 

### 컴파일 시점에서의 이넘 특징
- 이넘이 런타임 시점에서는 실제 객체지만, `keyof`를 사용할 때 주의해야 합니다. 일반적으로 `keyof`를 사용해야 하는 상황에서는 `keyof typeof`를 사용해야 합니다.

### 리버스 매핑(Reverse Mapping)
- 리버스 매핑에는 숫자형 이넘에만 존재하는 특징입니다. 이넘의 key값으로 value를 얻을 수 있고, 그 반대도 가능합니다.
```js
enum Reverse {
    R
}

const value = Reverse.R; // 0(key로 value 획득)
const key = Reverse[value]; // R(value로 key 획득)
```