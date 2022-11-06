# next_laravel_template
Nextjs + Laravel + Mysqlの開発環境テンプレート

<br />

## **環境構築**

- NextjsをLocal、Laravel + MysqlをDockerにて開発　->　`$ make init`
- Nextjs + Laravel + MysqlをDockerにて開発　->　`$ make init-docker`

### **make init**
meke init の処理内容（make init-dockerもnextjsの起動をdockerかlocalかの違いのみです）
1. cp .env.example .env　->　ルートディレクトの.env.exampleから.env複製（DB接続情報と各コンテナport）
2. cp ./next/.env.example.local ./next/.env　->　nextjsの.env.example.localから.env複製（クライアントとサーバーサイドのエンドポイント）
3. docker-compose -f docker-compose.local.yml up -d --build　->　各コンテナビルド
4. docker-compose exec laravel composer install　->　laravel依存関係インストール
5. docker-compose exec laravel cp .env.example .env　->　laravelの.env.exampleから.env複製
6. docker-compose exec laravel php artisan key:generate　->　laravelのAPIキー作成
7. docker-compose exec laravel chmod -R 777 storage bootstrap/cache　->　laravelの権限変更（ログ出力など）
8.  @make cache　->　laravelのキャッシュクリア
9.  @make fresh　->　laravelのmigrationとseeding実行
10. cd next && yarn && yarn dev　->　nextjsの依存関係インストールしてローカルで起動



下記のコンテナ4つが立ち上がる(make initの場合はnextを除く3つ)。
<image src="https://hiz-pictures.s3.ap-northeast-1.amazonaws.com/NL-docker.png" />

<br />

### Next.js
- version : 13
- http://localhost:3000/

<image src="https://hiz-pictures.s3.ap-northeast-1.amazonaws.com/next-top.png" />

<br />

### Laravel
- version : 9
- http://localhost:8080/

<image src="https://hiz-pictures.s3.ap-northeast-1.amazonaws.com/laravel-top.png" />