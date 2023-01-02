# CRA + yarn berry pnp

You will be get in trouble when run/test/build CRA project with yarn berry pnp.
This repository resolve all problems.


## TroubleShotting
```js
// When run 'yarn start'
Property 'toBeInTheDocument' does not exist on type 'JestMatchers<HTMLElement>'
```
이 타입은 `@types/testing-library__jest-dom` 에 정의되어 있는데 pnpm 에서는 이를 자동으로 가져오지 못하기 때문에 에러가 발생한다.
그래서 install 을 한번 해서 pnp 가 패키지를 인식할 수 있게 해줘야 한다.
- [https://github.com/testing-library/jest-dom/issues/123#issuecomment-1282207728](https://github.com/testing-library/jest-dom/issues/123#issuecomment-1282207728)

```js
// When run 'yarn build'
Creating an optimized production build...
Failed to compile.

[eslint] Failed to load config "react-app" to extend from.
Referenced from: /Users/soodiamond/dev/create-react-app-with-yarn-berry/package.json
```
eslint-config-react-app 도 마찬가지 이유. 따로 설치해줘야 한다. 대신 develop 환경으로 설치해주고, .yarnrc.yml  파일에 다음 설정을 추가해준다.
- [https://github.com/facebook/create-react-app/issues/10463#issuecomment-1022751568](https://github.com/facebook/create-react-app/issues/10463#issuecomment-1022751568)

마지막으로 yarn install 한번 해주면 build 완료 된다.
