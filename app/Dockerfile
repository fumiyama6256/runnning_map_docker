# ベースイメージ
FROM node:20

# 作業ディレクトリの設定
WORKDIR /usr/src/app

# 依存関係のインストール
COPY package*.json ./
RUN npm install

# TypeScriptコンパイラのインストール
RUN npm install -g typescript

# アプリケーションのコピー
COPY . .

# TypeScriptのビルド
RUN npm run build

# ポートの開放
EXPOSE 3000

# アプリケーションの起動
CMD ["sh", "-c", "if [ \"$NODE_ENV\" = \"staging\" ]; then node dist/scripts/create-tables.js && node dist/server.js; else node dist/server.js; fi"]
