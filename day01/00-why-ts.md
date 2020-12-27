# 1일차 

## TypeScript는?
- TypeScript는 JavaScript에 타입을 부여한 언어이다.
- TypeScript를 브라우저에서 실행하기 위해서는 컴파일 과정이 필요하다.

## TypeScript를 쓰면 좋을까? 타입이 있을 때의 장점은?
- 객체에 잘못 접근하여 undefined가 출력되거나 브라우저 콘솔에 TypeError가 출력되는 것을 사전에 방지할 수 있다.
- 타입이 있을 때의 장점을 알아보기 위해 js에 주석으로 타입을 명시하는 JsDoc을 먼저 사용해 봤다. 함수 선언부에 @returns 키워드로 제네릭 타입(객체)의 리턴 값을 명시하고, @typedef, @property 키워드로 리턴 값의 속성들을 정의한다. 그러면 리턴 값에 접근하려고 할 때 속성 값(객체의 키)이 자동완성 된다. 
함수의 리턴 값을 콘솔로 찍어보거나 유추하지 않고도 객체에 속성들을 한 눈에 확인할 수 있다. 따라서 브라우저로 결과 값을 확인하기 전에 에디터(or IDE)에서 잘못된 코드를 발견하고, 오류를 방지할 수 있다.
- ts를 사용하면 해당 변수에서 사용할 수 있는 API 목록들을 보여주고, 자동완성까지 지원된다. (Intellisense 기능이라 함)좋다..
```ts
function add (a: number, b: number): number {
    return a + b;
}
var result = add(10, 20);
result.toLocaleString(); // result는 number타입임으로, `result.`을 입력했을 때 사용할 수 있는 메소드(API) 목록들을 보여준다.
```