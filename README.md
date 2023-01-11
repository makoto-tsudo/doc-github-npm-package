# githubでNPMリポジトリ作成

## 概要
プライベート共通モジュールをNPMを利用してインストールするため、
共通モジュールをnpm.pkg.github.comへPublishする。  
PublishはgithubのActionsを利用して自動化する。  
共通モジュールを利用する場合は、npm.pkg.github.comをリポジトリとして登録して利用する。  

## 利点と欠点

### 利点
- 開発環境標準のパッケージマネージャを利用できる。
### 欠点
- リポジトリの認証としてトークンを利用するが、有効期限が切れると再作成する必要がある。

## 共通モジュールの準備

- [package.json](samples/package.json)へ下記項目を記載
  - *name*  
  [scope]/[モジュール名]  
  *scope* は @ + `githubユーザ名` or `organization`  
  例：@cfmlabo
  - *version*
  - *publishConfig*  
  [scope]:registry: "https://npm.pkg.github.com"
- Actionsを利用して自動的にPublishする  
  [workflows/publish-to-private.yaml](samples/publish-to-private.yaml)  

## 共通モジュールの利用

- 認証トークンの作成  
  Settings -> Developer Settings -> Personal Access Tokens -> Tokens(classic) -> Generate New Token  
  read: packagesにチェックを入れて作成する。

- 認証トークンの再作成  
  有効期限が切れている場合はRegenerateで再作成する。

- リポジトリの設定とトークンの指定  
  [.npmrc](samples/.npmrc)をプロジェクトトップディレクトリへ配置する。

- インストール  
```sh
npm install [scope]/[モジュール名]
```
