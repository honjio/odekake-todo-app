# Travel-plan-application

## 概要

## 開発準備

.firebaserc の `<firebase-project-id>` の部分を自分の firebase のプロジェクト id に置き換えます。

```json
{
  "projects": {
    "default": "<firebase-project-id>"
  }
}
```

ターミナルで下記コマンドを打ちます

```bash
#① firebase コマンドを実行できない場合は firebase-tools をインストールします
  npm install -g firebase-tools

#② firebase へログインします
  firebase login

#③ 各ディレクトリに対して yarn install を実行します。
  yarn setup
```

## 開発コマンド

```bash
# vue が build され functons/ へ nuxt/ が出力される。同時に public へ assets/ コピーされる
  yarn build

# functions/ の index.ts をコンパイル後、そのファイルに基づいて firebase ローカルサーバーを立てる
  yarn serve

# functions/ の index.ts をコンパイル後、firebase へデプロイ
  firebase deploy --proejct <firebase-project-id>
```
