# 11일차

## 타입 단언(Type Assertion)

- 타입 단언이란 개발자가 타입스크립트보다 정확한 데이터 타입을 알 수 있을 때, 직접 변수의 타입을 단언하는 것을 말합니다. 타입 추론보다 구체적인 타입을 지정해야 할 경우에 사용할 수 있습니다.

### 타입 단언이란

- 간단한 예시를 먼저 살펴보겠습니다.

```js
let before; // before는 any로 추론
before = 20;
before = "age";
const after = before; // after도 any로 추론
```

- `before`를 선언할 때 값을 할당하지 않았기 때문에 타입은 `any`로 추론됩니다.
- 이후 값이 `string`으로 변경되었지만, `after` 역시 `any`로 타입이 추론됩니다.
- 이와 같은 경우에 타입 단언으로 `after`의 타입을 `string`으로 변경할 수 있습니다.

```js
const after = before as string; // 방법 1
const after = <string>before; // 방법 2
```

- `as`와 `<>` 두 가지 방법을 사용하면 개발자가 명시적으로 타입을 단언할 수 있습니다.
- 두 가지 방법이 제공되지만, 보통 `as`를 사용합니다.(참고. `jsx`에서 타입스크립트를 사용할 경우에는 `as`방식만 가능합니다.)
- 타입 단언의 방식은 타 언어와 비슷하지만 컴파일러가 데이터의 타입을 별도로 체킹하진 않습니다. 런타임에는 영향을 미치지 않으며 컴파일러에 의해서만 사용됩니다.

### 타입 단언의 사용

- 타입 단언은 DOM API를 조작할 때에도 많이 사용됩니다. DOM API 예시를 살펴보겠습니다.

```js
const div = document.querySelector("div"); // div는 {HTMLDivElement | null}로 추론
div.innerHTML = "타입단언"; // 오류 발생
```

- 위 코드에서 `div`에 접근할 경우 오류가 발생합니다. `div`는 유니온 타입으로 지정되어 값이 `null`일 수도 있기 때문인데요. 정상적으로 동작하게 하려면 `null`이 아니라는 것을 보장해주는 코드가 필요합니다.

```js
// 방법 1
const div = document.querySelector("div"); // div는 {HTMLDivElement | null}로 추론
if (div) {
	div.innerHTML = "타입단언"; // 정상 동작
}

// 방법 2 - 타입 단언
const div = document.querySelector("div") as HTMLDivElement; // div는 HTMLDivElement로 추론
div.innerHTML = "타입단언"; // 정상 동작
```

- 두 가지 방법으로 오류를 해결해보았습니다.
- 타입 단언이 아니어도 오류를 해결할 수 있지만, 항상 `div`엘리먼트가 존재할 경우에는 타입 단언의 방식이 더 적합합니다.
- 확실하게 `null`값을 배제할 수 있을 때에는 `as`로 타입 단언할 수 있습니다.
