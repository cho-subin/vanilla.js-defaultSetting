# 바닐라js 연습을 위한 환경설정
<br>

## 1. pageage.json 생성
$ npm init

## 2. npm 패키지 설치
npm을 사용해 웹팩 등의 필요한 패키지들을 설치
### Webpack
$ npm install -D webpack webpack-cli <br>
$ npm install -D webpack-dev-server <br>
$ npm install -D style-loader css-loader <br>
$ npm install -D html-webpack-plugin <br>
$ npm install -D clean-webpack-plugin <br>

### Babel
$ npm install -D @babel/core @babel/preset-env babel-loader

### Jest
$ npm install -D jest babel-jest

## 3. package.json
<img width="396" alt="스크린샷 2023-06-12 오후 10 47 08" src="https://github.com/whtnqls124578/vanilla.js-defaultSetting/assets/100771469/732ff672-8c09-4bef-9b5f-2db9f41b5b8a">
<br>

## 4. webpack.config.js
프로젝트 루트 경로에 webpack.config.js를 생성 <br>
웹팩은 주로 프론트엔드 번들링과 관련된 작업을 처리하는 도구

<img width="358" alt="스크린샷 2023-06-12 오후 10 48 39" src="https://github.com/whtnqls124578/vanilla.js-defaultSetting/assets/100771469/f80e7ddb-7db9-4e1a-a95d-6953a3810ba0">
<br>
개발 서버의 미들웨어를 사용하여 CSS 파일을 서버에서 직접 읽어와 클라이언트에게 전달하는 방식으로<br>
onBeforeSetupMiddleware를 통해 /css/style.css 경로로의 GET 요청에 대한 서버 코드를 작성한다.<br>
<br>
해당 경로로 요청이 들어오면 CSS 파일을 읽어서 적절한 MIME 타입과 함께 응답을 보낸다.<br>
이 코드는 웹팩 개발 서버(devServer)의 'onBeforeSetupMiddleware' 옵션 내부에 작성되었으므로, 웹팩 개발 서버 실행 시 포함한다.<br>
<br>
개발 서버 환경에서만 작동하고 실제 배포 환경에서는 다른 서버를 사용해야 한다.<br>
개발 서버를 통해 개발 및 디버깅을 하고 실제 배포를 위해서는 별도의 서버 설정이 필요하다.<br>
<br>
<br>
* type: 'text/css'는 css 파일을 직접 가져와서 문자열로 변환 후 스타일 시트로 적용하는 방식 (Webpack 4 이전 버전에서 주로 사용) <br>
<br>
* type: 'asset/resource'는  CSS 파일을 모듈로 처리하고 해당 모듈을 번들링된 결과물로 추출하는 방식 (Webpack 5부터 도입된 새로운 모듈 타입(asset) 중 하나)<br>
  CSS 파일을 자체적으로 모듈로 처리하여 필요한 경우에만 파일로 추출하고, 그렇지 않은 경우에는 스타일 시트로 포함되도록 동작.<br>
  추출된 파일은 output.path에 설정된 경로에 저장된다. 그리고 CSS 파일의 URL 경로는 publicPath 옵션에 설정한 경로로 생성된다.<br>
  따라서 수정된 코드를 사용하면 CSS 파일이 번들링된 결과물로 추출되어 저장되며, HTML에서 해당 CSS 파일을 로드하여 적용할 수 있다.<br>
