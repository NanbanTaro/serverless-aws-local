# serverless-aws-local

## 環境
* Node:v16.17.0
* npm:8.15.0
* packageバージョンは本プロジェクトと同等

## 初期環境構築
```
npm init
npm install -D serverless dynamodb-admin npm-run-all
npx sls create -t aws-nodejs
npx sls plugin install -n serverless-offline
npx sls plugin install -n serverless-dynamodb
```
`serverless.yml`のpluginsの`serverless-dynamodb`を`serverless-offline`上側にする<br>
下記を`serverless.yml`に追加(必要箇所は適宜修正)
```
custom:
  dynamodb:
    start:
      migrate: true
    stages:
      - dev
  serverless-dynamodb:
    port: 8000
    docker: false
    start: 
      migrate: true
      host: 127.0.0.1
    stages:
      -dev
```
下記実行で`.dynamodb`のフォルダができる(git管理しない)
```
npx sls dynamodb install
```
`package.json`のscriptに下記を追加する
```
"start": "run-p localdb:* dev",
"dev": "sls offline",
"localdb:start": "sls dynamodb start --sharedDb",
"localdb:admin": "export DYNAMO_ENDPOINT=http://localhost:8000 && dynamodb-admin"
```
下記実行で、ローカル起動できる。
```
npm run start
```