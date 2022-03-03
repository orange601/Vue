## 시작 ##
1. vue.cmd create vue-todo 명령어 실행
2. 프로젝트 default로 생성
3. 현재위치가 workspace로 돼 있기때문에 vue-todo로 이동
4. npm run serve 실행

## 명령어 ##
1. vue --version 안될때 -> vue.cmd --version 
  - 4.5.xx 버전에서 안됨 몇 버전부터인지 확인 안해봄
  - 참고 : https://hjh0827.tistory.com/51

2. rm -rf vue-todo
  - rm의 -rf 기증을 이용해서 프로젝트를 삭제하는 방법이 많이 나오는데 git 명령어라는 것을 알고있자.


## 버전 ##
"vue": "^2.6.11"

## NVM을 이용한 버전관리 ##
- NVM을 사용한다면 여러개의 Node 를 버전별로 쉽게 관리하고 사용할 수 있다.

### Installing and Updating ###
- https://github.com/nvm-sh/nvm 접속하면 아래 설치방법과 스크립트 변경방법에 대해 자세하게 설명 되어 있다.
1. Installing
````curl
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.1/install.sh | bash
````
2. Update Script
````bash
export NVM_DIR="$([ -z "${XDG_CONFIG_HOME-}" ] && printf %s "${HOME}/.nvm" || printf %s "${XDG_CONFIG_HOME}/nvm")"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh" # This loads nvm
````
3. 참고
  - https://github.com/joshua1988/vue-til-server#nvm-%EC%84%A4%EC%B9%98-%EB%B0%8F-%EB%B2%84%EC%A0%84-%EB%B3%80%EA%B2%BD-%EB%B0%A9%EB%B2%95
  - https://www.inflearn.com/questions/281892 (윈도우)


## 웹팩 개발 서버 ##
- ajax 방식의 api 연동은 cors 정책 때문에 반드시 서버가 필요하다.
- 프론트엔드 개발환경에서 이러한 개발용 서버를 제공해 주는 것이 webpack-dev-server다.

````js
// webpack.config.js:
module.exports = {
  devServer: {
    contentBase: path.join(__dirname, "dist"),
    publicPath: "/",
    host: "dev.domain.com",
    overlay: true, // 에러시 브라우저에 표시 여부
    port: 8081,
    stats: "errors-only",
    historyApiFallback: true,
    open : true // 브라우저 바로 열기
  },
}
````

## ESLint ##
- JavaScript 코드에서 발견 된 문제 패턴을 식별하기위한 정적 코드 분석 도구
- prettier 기능을 이용하면 소스의 일관성을 유지할 수 있음

## 파일을 상대경로에서 절대경로로 찾기 설정 ##
- 변경 전
````vue
import chart from './components/chart'
````
- 변경 후
````vue
import chart from '@/components/chart'
````
- 참고: https://code.visualstudio.com/docs/languages/jsconfig

````js
// jsconfig.json
{ 
  "compilerOptions": {
    "baseUrl": "./",
    "paths": {
        "@/*": ["src/*"] // @이를 사용하게되면 src 폴더를 의미
    }
  },
  "exclude": ["node_modules", "dist"] // 라이브러리 경로 제외
}
````

## vue.js 스타일 가이드 ##
- 안티패턴을 피하는 좋은 참조
- 참고: https://kr.vuejs.org/v2/style-guide/index.html

## router ##
1. 설치
  - npm i vue-router
  - "vue-router": "^3.5.3" // vue-router 4 -> vue3부터 사용가능

## vuex ##
1. 설치
  - npm i vuex

2. npm에서 확인해보면 상단에 현재 버전이 있고, 이전버전 설치를 원하면 version메뉴를 눌러서 확인하면 된다.
  ![이미지 6](https://user-images.githubusercontent.com/24876345/154449112-d1b51c46-e447-4118-83b6-16b7c946ac91.png)
  
3. vuex 설정파일은 관행적으로 store라는 폴더에 생성하고 설정한다.

4. 기술요소
  - state: 여러컴포넌트에 공유되는 데이터 data
  - getters: 연산된 state 값을 접근하는 속성 computed
  - mutaions: state 값을 변경하는 이벤트 로직, 메서드 methods
  - actions: 비동기 처리 로직을 선언하는 메서드 aysnc methods

5. 구조
  - 컴포넌트 -> 비동기로직 -> 동기로직 -> 상태
--------------------------------------------
  ![이미지 7](https://user-images.githubusercontent.com/24876345/154450846-74ea3a72-f789-43f3-bcbf-c234ec5c2ed1.png)

