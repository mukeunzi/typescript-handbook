# 8일차

## 타입스크립트 클래스의 기본 문법
- 타입스크립트의 기본적인 클래스 문법에 대해 살펴보겠습니다. 다음과 같은 형식을 따릅니다.
```js
class Person {
  name: string;
  age: number;

  constructor(name: string, age: number) {
    this.name = name;
    this.age = age;
  }
}
```
- 자바스크립트와 달리 타입스크립트에서는 접근제어자를 사용할 수 있습니다.
```js
class Person {
  private name: string;
  public age: number;
  readonly log: string;

  constructor(name: string, age: number) {
    this.name = name;
    this.age = age;
  }
}
```