# serverless-aws-local

## 環境
Node:v16.17.0<br>
npm:8.15.0

## 初期環境構築
```
npm init
npm install -g serverless
sls create -t aws-nodejs
serverless plugin install -n serverless-offline
sls offline
```