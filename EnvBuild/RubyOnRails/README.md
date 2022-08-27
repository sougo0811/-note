# Ruby on Railsの環境構築

* [Macはこちらから](./mac.md)

## 目次

1. [Ubuntuを導入するための準備をしよう](#ubuntuを導入するための準備をしよう)

1. [Ubuntuの導入とアップデート](#ubuntuの導入とアップデート)

1. [Ubuntuに各種ライブラリの導入](#ubuntuに各種ライブラリの導入)

1. [Node.jsの導入](#nodejsの導入)

1. [rbenvの導入&Rubyの導入&Railsの導入](#rbenvの導入rubyの導入railsの導入)

1. [MySQLの導入](#mysqlの導入)

1. [envの導入](#envの導入)


<br>

## Ubuntuを導入するための準備をしよう
* WindowsでLinuxSubSystemを有効化しよう
1. 検索欄に「Windows機能の有効化または無効化」を入力
1. Linux 用 Windows サブシステム,Windows ハイパーバイザー プラットフォーム,仮想マシン プラットフォームにチェック

* 開発者モードの有効化をしよう
1. スタートボタンから設定をクリック
1. 設定ページでプライバシーとセキュリティを選択
1. 開発者モードをクリックして有効化する

* Windows Terminalを導入しよう(Windows11にはデフォルトで導入されているらしいので確認してみてなかったら入れてね！)<br>
[Windows Terminalのインストールはここから！](https://apps.microsoft.com/store/detail/windows-terminal/9N0DX20HK701?hl=ja-jp&gl=JP)

## Ubuntuの導入とアップデート

1. コマンドプロンプトまたはPowerShellを管理者権限で起動
1. 以下のコマンドでUbuntu,仮想マシンプラットフォーム,WSL,WSL用Linuxカーネル,GUIアプリサポート,Linuxディストリビューションをインストール
```
wsl --install -d Ubuntu
```

### 手動でUbuntuのインストールとWSLのアップデートをする方法(上の方法で上手くインストールできなかった場合)

* [Ubuntuのインストールはここから](https://apps.microsoft.com/store/detail/ubuntu-on-windows/9NBLGGH4MSV6?hl=ja-jp&gl=JP)

* WSLをアップデートしよう<br>
[Linux カーネル更新プログラム パッケージをダウンロード](https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_x64.msi)


* Ubuntuの初期設定
  * ユーザー名入力（小文字と数字のみ使えます）
  * パスワード入力（見えないのは仕様なので注意）

* ワークスペースディレクトリの作成
  * ワークスペースの作成
  ```
  mkdir workspace
  cd workspace
  ```

* Ubuntuのバージョンを最新にする
    ```
    sudo apt update && sudo apt upgrade -y
    ```
## Ubuntuに各種ライブラリの導入
```
sudo apt install make
sudo apt install gcc
sudo apt install -y libssl-dev libreadline-dev zlib1g-dev
```

## Node.jsの導入
* npmのインストール
  ```
  sudo apt install npm
  ```
* npmのバージョン確認
  ```
  npm -v
  ```


## rbenvの導入&Rubyの導入&Railsの導入

* rbenvのインストール
  ```
  git clone https://github.com/sstephenson/rbenv.git ~/.rbenv
  ```

* rbenvのPATHを通す
  * export PATH="$HOME/.rbenv/bin:$PATH"を~/.bashrcに追記する
    ```
    echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> ~/.bashrc
    ```
  * (.bashrcファイルが無かった場合)
    ```
    touch ~/.bashrc
    ```
  * rbenvの設定を行う
    ```
    echo 'eval "$(rbenv init -)"' >> ~/.bashrc
    ```
  * 確認方法
    ```
    使用したいエディタ名(code,vim,catなど) ~/.bashrc
    ```
  * 変更の読み込み
    ```
    source ~/.bashrc
    ```

* ruby-buildのインストール
  ```
  git clone https://github.com/sstephenson/ruby-build.git ~/.rbenv/plugins/ruby-build
  ```

* RubyのインストールとRailsの導入
  * 安定バージョンの確認
    ```
    rbenv install --list
    ```
  * 2系と3系の安定バージョンをインストール(2022年6月では2.7.6と3.1.2)
    ```
    rbenv install 2.7.6
    rbenv install 3.1.2
    rbenv rehash
    ```
  * Ruby2系用ディレクトリとRuby3系用ディレクトリを作成(2022年6月では2.7.6と3.1.2)
    ```
    mkdir ruby-2.7.6
    mkdir ruby-3.1.2
    ```
  * Ruby2系＆Rails5系とRuby3系＆Rails7系の環境を反映(2022年6月ではRuby2.7.6にRails5.2.8,Ruby3.1.2にRails7.0.3)
    ```
    cd ruby-2.7.6
    rbenv local 2.7.6
    ruby -v （確認）
    gem install rails -v 5.2.8
    cd ..
    cd ruby-3.1.2
    rbenv local 3.1.2
    ruby -v （確認）
    gem install rails -v 7.0.3
    cd ..
    ```

## MySQLの導入
* MySQLとそれに関連するパッケージのインストール
  ```
  sudo apt install mysql-server mysql-client libmysqlclient-dev ruby-dev
  ```
* MySQLの起動
  ```
  sudo service mysql start
  ```
* MySQLのユーザー作成
  ```
  sudo mysql -u root
  ```
  以下MySQLを操作(mysql>)
  ```
  SHOW GLOBAL VARIABLES LIKE 'validate%';
  CREATE USER '設定するユーザー名'@'localhost' IDENTIFIED BY '設定するパスワード'; 
  GRANT ALL ON *.* TO '設定したユーザー名'@'localhost';
  quit;
  ```

* テストアプリを作成
  ```
  cd ruby-2.7.6
  rails new test_app -d mysql
  cd test_app
  ```

* database.ymlファイルにDBのユーザーとパスワードを書き込む（実際の開発では.envrcファイルに書き込む）<br>
  usernameに作成したユーザー名<br>passwordに設定したパスワード
  ```
  code config/database.yml
  ```
  ⇩database.ymlファイルの中身(一部)
  ```
  default: &default
    adapter: mysql2
    encoding: utf8mb4
    pool: <%= ENV.fetch("RAILS_MAX_THREADS") { 5 } %>
    username: MySQLで作成したユーザー名を入力
    password: MySQLで作成したパスワードを入力
  ```

* MySQLでデータベース作成とマイグレーション
  ```
  rails db:create
  rails db:migrate
  ```
  (もしエラーが出たら、Ubuntuの再起動をしてみてください)

* Railsサーバーを起動
  ```
  rails s
  ```

(余裕のある方は、同様の手順でruby-3.1.2のディレクトリでもテストアプリを作ってみよう！)

## envの導入
実際の開発でMySQLのユーザー名やパスワードを直書きしているとセキュリティ面に脆弱性ができてしまうので、別の公開しないファイルに書き込んで、変数を使って呼び出せるようにする。

* アプリのディレクトリに飛ぶ
  ```
  cd workspace/ruby-2.7.6/test_app
  ```

* dotenv-railsのインストール
  * gemファイルを開く
    ```
    code Gemfile
    ```
  * Gemfileの一番下の行を改行して、以下のコマンドを書き込む
    ```
    gem 'dotenv-rails'
    ```
  * Gemに反映させる
    ```
    bundle install
    ```

* .envファイルにMySQLのユーザー名とパスワードを書く<br>
  * .envファイルを作る
    ```
    touch .env
    ```
  * .envファイルをVScodeで開く
    ```
    code  .env
    ```
  * .envファイルに以下のことを書き込む
    ```
    DATABASE_USER=MySQLで作成したユーザー名入力
    DATABASE_PASS=MySQLで作成したパスワドを入力
    ```
  * .gitignoreファイルに.envを追加する
    ```
    code .gitignore
    ```
    gitignoreファイルが開かれたら1番下の行を改行して
    ```
    .env
    ````
    と書き込む

* アプリのdatabase.ymlファイルの情報を変更
  ```
  code config/database.yml
  ```
  ⇩database.ymlファイルの中身(一部)
  ```
  default: &default
    adapter: mysql2
    encoding: utf8mb4
    pool: <%= ENV.fetch("RAILS_MAX_THREADS") { 5 } %>
    username: <%= ENV['DATABASE_USER'] %> #←これに書き換える
    password: <%= ENV['DATABASE_PASS'] %> #←これに書き換える
  ```

* test_appを起動して確認
  ```
  rails s
  ```

errorが出なければOK！
