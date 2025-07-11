# EmoTra Backend
- メンタルヘルスのための感情トラッキングアプリケーション
- 日記のように感情を記録し、振り返ることができる
- GoとGinによるバックエンドAPI

## 実装済み機能
- 日記の登録、編集、削除、閲覧
- グラフによる感情の可視化
- LLMにメンタルスコアを分析させる

## TODO
- JWT認証のログインを実装
- jsonbカラムを追加してスキーマレスにメンタル以外のスコアも記録できるようにする
- 設定系

## 環境構築
- ローカルにGo、golang-migrateのインストール
- リポジトリをクローン
- リポジトリのディレクトリに移動
- `cp .env.example .env` で環境変数ファイルを作成
- `docker compose up -d --build` でコンテナを立ち上げ
- ブラウザで`http://localhost:8080/ping`にアクセス
- ビルド`go run main.go`

## ホットリロードで立ち上げ
- `go install github.com/air-verse/air@latest`でairをインストールしていること
- `air init`で設定ファイルを生成
- `air`で起動

## DBマイグレーションのコマンド(db接続情報は要変更)
- `migrate -path ./infra/migrations -database "postgres://ginuser:ginpassword@localhost:5432/emotra?sslmode=disable" up`
- `migrate -path ./infra/migrations -database "postgres://ginuser:ginpassword@localhost:5432/emotra?sslmode=disable" down`

## テスト 
- `go test ./...`

## Swagger UI
- `http://localhost:8080/swagger`にアクセスしてSwagger UIで手動でAPIをテストできる
- `http://localhost:8080/openapi.yml`にアクセスしてOpenAPI仕様書を確認できる

## VSCode REST ClientによるAPIの手動テストのやり方
- .vscode/api-manual-test.http を開く
- Send Request ボタンを押す

## アーキテクチャなどの構想
- 軽量DDDを採用
- オニオンアーキテクチャを採用
- テストを書きやすく
  - ユースケース層とリポジトリ層はインターフェース経由で依存関係を注入
  - コントローラ層はインターフェースを作成しないことにしてみる


## GoとGinの初期構築メモ
- `make emotra-backend`
- `cd emotra-backend`
- `go mod init emotra-backend`
- `go get -u github.com/gin-gonic/gin`
- `main.go`を作成
- `go run main.go`で起動
- `http://localhost:8080/ping`にアクセスして確認
- `{"message":"pong"}`が返ってくれば成功

## メモ
- 8080ポートのプロセスを強制killしたい時
 - `kill -9 $(lsof -t -i:8080)`
- データベースのテーブルを削除したい時
