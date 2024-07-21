# はじめに
DockerでReactの環境を構築する手順を以下に示します。この例では、Dockerを使用してReactアプリケーションをセットアップし、開発環境を整える方法を説明します。

# プロジェクトのディレクトリ構成
まず、プロジェクトのディレクトリを以下のように構成します。

      my-react-app/

      ├── Dockerfile

      ├── docker-compose.yml

         └── src/

            └── index.js

            └── App.js

    
# Dockerfile の作成

my-react-appディレクトリにDockerfileを作成します。

・ベースイメージとしてnodeを使用

FROM node:14

・作業ディレクトリを設定

WORKDIR /usr/src/app

・package.jsonとpackage-lock.jsonをコピー

COPY package*.json ./

・依存関係をインストール

RUN npm install

・アプリケーションのソースコードをコピー

COPY . .

・アプリケーションをビルド

RUN npm run build

・アプリケーションを起動

CMD ["npm", "start"]

・ホストとコンテナ間でマウントするポートを指定

EXPOSE 3000

# docker-compose.yml の作成

my-react-appディレクトリにdocker-compose.ymlを作成します。


      version: '3'
   
      services:
   
           web:
     
             build: .
       
             ports:
       
               - "3000:3000"
       
             volumes:
       
               - .:/usr/src/app
         
               - /usr/src/app/node_modules
       
             stdin_open: true
       
             tty: true
       
# package.json の作成

my-react-appディレクトリにpackage.jsonを作成します。Reactプロジェクトを生成するには、以下のコマンドを使用します。

      npx create-react-app my-react-app

このコマンドを実行すると、my-react-appディレクトリに必要なファイルが生成されます。既にcreate-react-appを実行している場合は、package.jsonの内容を確認して、そのまま利用できます。

# React アプリケーションの実行

プロジェクトのディレクトリで以下のコマンドを実行します。

      docker-compose up

このコマンドを実行すると、DockerがReactアプリケーションをビルドし、http://localhost:3000 でアクセスできるようになります。

# 停止
アプリケーションを停止するには、以下のコマンドを使用します。

      docker-compose down
