# 12일차

## 타입 가드(Type Guards)

- 타입 가드는 일부 스코프에서 특정 타입임을 보장하는지 런타임 검사를 수행하는 표현식입니다. 타입 가드를 정의하려면 리턴 값이 `{parameter} is {type}`인 함수를 생성하면 됩니다.
- 예시를 통해 살펴보겠습니다.

### 타입 가드의 사용

```js
interface Developer {
	name: string;
	skill: string;
}

interface Person {
	name: string;
	age: number;
}

function introduce(): Developer | Person {
	return { name: "Coly", age: 20, skill: "walk" };
}

const coly = introduce();
console.log(coly.skill); // 오류 발생
```

- `introduce`함수의 리턴 타입은 유니온 타입으로 지정되었기 때문에 변수 `coly`에서는 두 타입의 공통 속성에만 접근할 수 있습니다.
- 특정 타입에만 존재하는 속성에 접근하려면, 타입 단언이나 타입 가드를 사용해야 합니다. 두가지 방법 모두 살펴보겠습니다.

```js
interface Developer {
	name: string;
	skill: string;
}

interface Person {
	name: string;
	age: number;
}

function introduce(): Developer | Person {
	return { name: "Coly", age: 20, skill: "walk" };
}

const coly = introduce();

// 타입 단언을 사용한 방식
if ((coly as Developer).skill) {
    const skill = (coly as Developer).skill;
    console.log(skill);
} else if ((coly as Person).age) {
    const age = (coly as Person).age;
    console.log(age);
}

// 타입 가드를 사용한 방식
function isDeveloper (target: Developer | Person): target is Developer {
    return (target as Developer).skill !== undefined;
}

if (isDeveloper(coly)) {
    console.log(coly.skill);
} else {
    console.log(coly.age);
}
```

- 타입 단언(`as`)을 사용할 경우 `if`문을 여러 번 사용해 범위를 좁혀나가야 합니다.
- 타입 가드(`{params} as {type}`) 함수를 사용하면 파라미터의 타입을 한 번에 좁힐 수 있습니다. 위 코드에서는 매번 파라미터의 타입을 체크할 필요 없이 타입 가드 함수를 호출해 한 번에 타입을 보장받을 수 있습니다.
- 타입 가드의 함수 명은 보통 `is{type}`형식으로 사용합니다.
