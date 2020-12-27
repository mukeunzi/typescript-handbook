# 1일차

## TypeScript를 시작하는 방법
- 터미널에서 아래 명령어를 입력해 ts 모듈을 설치한다.
```
npm i typescript -g
```
-  `index.ts` 파일에 코드를 작성하고 터미널에 `tsc index.js`를 입력하면, ts파일이 컴파일 되면서 `index.js` 파일이 생성된다.
- 매번 `tsc` 명령어를 이용해 컴파일하는 것 보다 웹팩을 활용하는 것이 좋다.
- `tsconfig.json` 파일을 이용해 컴파일할 때 부가적인 옵션들을 지정할 수 있다. 
```json
{
    "compilerOptions: {
        "allowJs": true, // 프로젝트에 JS 허용
        "checkJs": true, // @ts-check와 같은 기능으로, JS 코드에서도 TS처럼 타입을 체크하겠다는 의미
        "noImplicitAny": true // 최소 any 타입이라도 지정해야 함
    }
}
```
- [공식문서](https://www.typescriptlang.org/) - Playground에서 ts를 연습 할 수 있다. 좌우로 화면이 분할되어 있으며, 좌측엔 ts로 코드를 작성할 수 있고, 우측엔 실시간으로 컴파일 된 결과물을 확인할 수 있다.