# docker-rubocop-vscode<!-- omit in toc -->

- 古いバージョンのRuboCopでVSCode拡張を動作させるために作成したもの

## TOC<!-- omit in toc -->

- [Required](#required)
- [Setup](#setup)
- [ENV Config](#env-config)

## Required

- VSCode Extension:
  - [misogi.ruby-rubocop](https://marketplace.visualstudio.com/items?itemName=misogi.ruby-rubocop)

## Setup

- `env`ファイルを作成して値を入力（[ENV Config](#env-config)）

  ```bash
  $ cp env.example env
  ```

- Docker Composeでイメージビルド、Dockerコンテナを起動

  ```bash
  $ docker compose build
  $ docker compose run app bundle install
  $ docker compose up -d
  ```

- VSCodeに[misogi.ruby-rubocop](https://marketplace.visualstudio.com/items?itemName=misogi.ruby-rubocop)をインストール

- RuboCopをVSCodeで実行したいプロジェクトで`.vscode/settings.json`に以下の内容を追記

  ```json
  {
    // 本プロジェクトにあるrubocopファイルまでのフルパス
    // example: /Users/<username>/docker-rubocop/bin/
    "ruby.rubocop.executePath": "/path/to/docker-rubocop/bin/",
    "[ruby]": {
      "editor.defaultFormatter": "misogi.ruby-rubocop"
    }
  }
  ```

## ENV Config

- `env`に入力する値

  | 項目 | 内容 | 例 |
  | -- | -- | -- |
  | RUBY_VERSION | コンテナで実行するRubyバージョン | 2.7.2 |
  | RUBOCOP_VERSION | コンテナで実行するRuboCopバージョン | 0.34.2 |
  | RUBOCOP_YML_PATH | .rubocop.ymlのフルパス | /Users/\<username\>/rails/.rubocop.yml |
  | SOURCE_PATH | RuboCopを実行するソースコードのフルパス | /Users/\<username\>/rails |
