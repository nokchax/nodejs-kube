# nodejs-kube
node.js, docker, kubernetes로 서버 만들어 보기

## 사전준비
node 설치
```
brew install node
```
## Node 프로젝트 구성하기
### 프로젝트 구성
```shell
mkdir myapp
cd myapp
npm init
npm install express --save
```
> --save 옵션을 통해 설치된 node 모듈은 package.json 파일 내의 dependencies 목록에 추가되며, 이후 npm install을 실행하면 종속 항목 목록 내의 모듈이 자동으로 설치됨, default로 세이브 되기 때문에 생략해도 됨 혹은 `npm i express`

### app.js생성
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

### 실행
```shell
node app.js
```


## Docker 적용하기
Dockerfile 생성 - [참고](https://nodejs.org/ko/docs/guides/nodejs-docker-webapp/)
```
FROM node:12

# 앱 디렉터리 생성
WORKDIR /usr/src/app

# 앱 의존성 설치
# 가능한 경우(npm@5+) package.json과 package-lock.json을 모두 복사하기 위해
# 와일드카드를 사용
COPY package*.json ./

RUN npm install
# 프로덕션을 위한 코드를 빌드하는 경우
# RUN npm ci --only=production

# 앱 소스 추가
COPY . .

EXPOSE 8080
CMD [ "node", "server.js" ]
```
