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

## Gitの扱い　まとめ
1. Github repository のコピーをローカル端末 (⾃分の端末) 上に取得する
`git clone https:,,,.git`
現在の場所に取得したディレクトリができる
2. 編集が済んだら変更をインデックス（まとまり）に追加する
`git add <変更したファイル名>`
その変更されたインデックスをローカルリポジトリに登録する
`git commit -m "コメント（変更点を簡潔に）"`
3. Remote repositoryへ変更を反映する
`git push`でローカルのリポジトリの状態をリモートリポジトリへアップロード（同期）
4. その編集をしていない人はその変更を自分のローカルリポジトリへ反映させる必要がある
`git pull`で同期
5. 複数人が同時に編集を行うためには、ブランチを作成する
ローカル上で異なる世界戦（branch）を作成する
`git switch -c <branch名>`
ブランチ間の移動、現在のブランチの確認は以下
`git switch <移動先branch名>`　`git branch`
6. リモートリポジトリに特定のブランチをアップロードする
`git push -u origin <branch名（HEADで現在のbranch）>`
この作業で、github上でも追加されたブランチが表示される
7. 特定のブランチを採用し、その変更を他のブランチへ取り込む操作（マージ）
例）masterブランチにtest_branchブランチの変更を取り込む
    `git switch master`
    `git merge test_branch`
    これらのコマンドでも可能だが一般にmasterへのマージはgithub上で行い、それ以外のローカルリポジトリ内でのマージをこのコマンド
で行うのが良い    

