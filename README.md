## バックエンドの設定
### TypeScriptの設定
```bash
cd backend
npm install typescript ts-node @types/node @types/express
```
## フロントエンドの設定
### TypeScriptの設定
```bash
cd frontend
npm install typescript @types/react @types/react-dom
```
###  Docker Composeの起動
#### Staging環境での実行
```bash
docker-compose --env-file .env.staging up --build
```
- frontendのReactアプリも起動する
#### Production環境での実行
```bash
docker-compose --env-file .env.production up --build
```
#### backendでdistファイルがないというエラーが出る場合は
```bash
cd backend
npm run build
```
#### npm installでなんか言われたら修正。脆弱性
```bash
npm audit fix
```

#### dynamodbのレコード確認(staging限定)
- コンテナ外で以下実行。aws configureはそれぞれ設定できると思うので、他に使ってて設定を変えたい人はググってください。
  - aws configure
    - 以下値をそれぞれ設定
    - dummyAccessKeyId
    - dummySecretAccessKey
    - ap-northeast-1
    - 4つ目は入力せずで良い
- テーブル確認
```bash
aws dynamodb list-tables --endpoint-url http://localhost:8000
```
- レコード確認
```bash
aws dynamodb scan --table-name Users --endpoint-url http://localhost:8000
aws dynamodb scan --table-name TrainingSessions --endpoint-url http://localhost:8000
```
