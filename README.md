# nodejs-kube
node.js, docker, kubernetes로 서버 만들어 보기

## 사전준비
node 설치
```
brew install node
```

## 프로젝트 구성
```shell
mkdir myapp
cd myapp
npm init
npm install express --save
```
> --save 옵션을 통해 설치된 node 모듈은 package.json 파일 내의 dependencies 목록에 추가되며, 이후 npm install을 실행하면 종속 항목 목록 내의 모듈이 자동으로 설치됨, default로 세이브 되기 때문에 생략해도 됨 혹은 npm i express

## app.js생성
```javascript
const express = require('express')
const app = express()
const port = 3000

app.get('/', (req, res) => {
  res.send('Hello World!')
})

app.listen(port, () => {
  console.log(`Example app listening at http://localhost:${port}`)
})
```
root directory에 생성

## 실행
```shell
node app.js
```
