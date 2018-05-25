# 리액트네이티브 시작하기

> `react-native-cli`를 이용해 리액트네이티브 프로젝트를 처음부터 시작할 수 있는 방법을 설명해두었습니다.
> typescript 등 몇 가지 필수사항이 아닌 라이브러리의 설치 방법도 포함되어 있으므로 상황에 맞게 사용하시기 바랍니다.

## ReactNative cli 설치

가장 먼저 [nodenv](https://github.com/nodenv/nodenv)를 통해 Node.js 를 설치합니다.

```shell
brew update
brew install nodenv
nodenv init
```

Node package 관리를 위해 [Yarn](https://yarnpkg.com/en/docs/install)도 설치해 줍니다.

```shell
brew install yarn
```

이제 ReactNative CLI를 설치해줍니다.

```shell
yarn global add react-native-cli
```

## ReactNative project 만들기

빈 프로젝트를 만듧니다.

```shell
react-native init AwesomeProject
```

## 빌드 도구 설치(XCode, AndroidStudio)

iOS 앱 제작에 사용할 XCode를 설치합니다.

> 맥 아이콘 -> 앱 스토어 -> XCode 검색 -> 설치

Android 앱 제작에 사용할 [AndroidStudio](https://developer.android.com/studio/index.html)를 설치합니다.

## Hello World

번들러를 시작합니다.

```shell
cd AwesomeProject
yarn start
```

### 시뮬레이터에서 구동

#### iOS

iOS 앱을 빌드하고 시뮬레이터에서 구동합니다

```shell
react-native run-ios
```

시뮬레이터 기기를 선택하고자 하는 경우 아래와 같이 특정 지어줄 수 있습니다.

```shell
react-native run-ios --simulator 'iPhone 6s Plus'
```

#### Android

Android 시뮬레이터를 시작합니다([참조](https://developer.android.com/studio/run/managing-avds.html))

> Tools -> Android -> AVD Manager

Android 앱을 빌드하고 시뮬레이터에서 구동합니다

```shell
react-native run-android
```

### JS 코드 수정 및 반영 과정

`index.ios.js` 및 `index.android.js` 파일을 수정하고 반영 사항을 확인합니다.

CMD + R 을 누르면 화면이 갱신됩니다(Reload). CMD + D를 누르면 개발 관련 메뉴를 볼 수 있습니다.

참조 [Debugging](https://facebook.github.io/react-native/docs/debugging.html)

### 기기에서 구동

#### iOS 기기

1. iPhone을 연결합니다
1. 신뢰할 수 있는 개발자로 등록해줍니다
1. XCode에서 연결된 iOS 디바이스를 선택하고 빌드 버튼을 누릅니다

#### Android 기기

1. Android 폰을 연결합니다.
1. Developer Options 에서 USB Debugging을 활성화해줍니다
1. `react-native run-android`

## TypeScript, ts-lint 등 기타 도구 설치

### TypeScript

타입스크립트는 JavaScript로 컴파일되는 언어로서 정적 타입체크를 제공하여 대단위 프로젝트에서도 자바스크립트를 사용하기 용이하게 해줍니다.

[타입스크립트 홈페이지](http://typescriptlang.org/)

```shell
yarn add --dev typescript
```

또한 타입 파일을 추가해줍니다

```shell
yarn add --dev @types/react @types/react-native
```

`tsconfig.json` 설정 파일을 생성합니다.

```shell
$(npm bin)/tsc --init
```

기본값으로 아래와 비슷한 설정 파일(`tsconfig.json`)이 생성되며 우리 프로젝트에 맞게 수정해줍니다.

```json
{
  "compilerOptions": {
    "jsx": "react-native",
    "module": "es2015",
    "noEmit": true,
    "strict": true,
    "target": "es5"
  },
  "exclude": [
    "node_modules"
  ]
}
```

tsconfig.json 각 옵션에 대한 설명은 [타입스크립트 핸드북](https://www.typescriptlang.org/docs/handbook/tsconfig-json.html)페이지에서 확인 가능합니다.

번들러가 트랜스파일 과정을 자동으로 해줄 수 있도록 [react-native-typescript-transformer](https://github.com/ds300/react-native-typescript-transformer)를 설치해줍니다.

```shell
yarn add --dev react-native-typescript-transformer
```

`rn-cli.config.js` 파일을 만들고 아래 내용을 넣어줍니다.

```javascript
module.exports = {
  getTransformModulePath() {
    return require.resolve('react-native-typescript-transformer')
  },

  getSourceExts() {
    return ['ts', 'tsx'];
  }
}
```

`index.ios.js` 의 내용을 `src/App.tsx` 로 옮기고 `index.ios.js`에서는 이를 불러옵니다

### ts-lint

eslint와 유사하지만 TypeScript 환경에서 사용 가능한 [tslint](https://github.com/palantir/tslint)를 설치합니다.

```shell
yarn add --dev tslint tslint-react
```

`tslint.json` 설정파일을 생성합니다.

```shell
$(npm bin)/tslint --init
```

```JSON
{
    "defaultSeverity": "error",
    "extends": [
        "tslint:recommended", "tslint-react"
    ],
    "jsRules": {},
    "rules": {},
    "rulesDirectory": []
}
```

## Editor extensions 설치

VS Code 기준

1. React Native Tools
1. TSLint

## React DevTools 및 크롬 개발도구 사용법

### React DevTools

[StandAlone 버전](https://github.com/facebook/react-devtools/blob/master/packages/react-devtools/README.md)

```shell
yarn global add react-devtools
```

iOS Simulator -> CMD + D -> Show Inspector

### Chrome DevTools

iOS Simulator -> CMD + D -> Debug JS Remotely

`App.tsx` 에서 `console.log` 내용 출력 확인
