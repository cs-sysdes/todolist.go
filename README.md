# Todolist(自分用)
このリポジトリは、Todolist アプリケーションを実装するためのベースプロジェクトを提供する。
（githubの練習も兼ねる）

`docker-compose.yml` は、Go 1.17 ビルドツール、MySQL サーバ、phpMyAdmin を提供します。

## 利用するシステム
- [Gin Web Framework](https://pkg.go.dev/github.com/gin-gonic/gin)
- [Sqlx](https://pkg.go.dev/github.com/jmoiron/sqlx)

## アプリケーションの実行方法
まず、Dockerコンテナを起動、開始する
```sh
$ docker-compose up -d
```
コンテナとダウンロードとビルドのため少々時間がかかる

次にアプリケーションの起動
```sh
$ docker-compose exec app go run main.go
```
`go run main.go`ファイルを実行する。Go 開発ツールがある場合は直接実行することもできますが、アプリケーションを MySQL サーバーに接続するための構成をセットアップする必要がある。

作業が終わったらコンテナを終了させるのを忘れずに。
```sh
$ docker-compose down
```

## 発展　データベースの初期化方法
データベースのスキーマに変更を加えた場合は、新たなデータベースを作成するため現在のデータベースを破棄する。DBコンテナのみを再構築するよりもすべて再構築してしまう方が楽。
```sh
$ docker-compose down --rmi all --volumes --remove-orphans
$ docker-compose up -d
```
