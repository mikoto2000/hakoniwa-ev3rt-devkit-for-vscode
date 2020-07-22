# hakoniwa-ev3rt-devkit-for-vscode

VSCode 向け [TOPPERS/箱庭 単体ロボット向け](https://toppers.github.io/hakoniwa/prototypes/single-robot/#%E5%B0%8E%E5%85%A5%E6%96%B9%E6%B3%95)プロトタイプモデルのビルド・実行環境。


## 必須環境

- docker(docker-compose ファイルバージョン 3 以上が実行可能なもの)
- Visual Studio Code Remote - Containers extension
- Unity
    - [Unityのインストール・パッケージのインポート・通信方式の切替方法](https://toppers.github.io/hakoniwa/single-robot-setup-detail/60_unity_install/) を参照


## 実行環境構成

Docker コンテナ上に構築した EV3RT とホスト上で起動した Unity が UDP で通信する構成。

Unity 側の設定は [UDP 用 Unity 設定 - 単体ロボット向けシミュレータ導入手順](https://toppers.github.io/hakoniwa/single-robot-setup-detail/61_unity_install_udp/) を参照。


```
+-----------------+       UDP(54001)      +-------+
| Docker コンテナ |---------------------->|       |
|     (EV3RT)     |                       | Unity |
|                 |<----------------------|       |
+-----------------+       UDP(54002)      +-------+
```


## 使い方

### 1. 開発環境用コンテナを VSCode で開く

1. 本リポジトリをテンプレートとして新規リポジトリを作成
    - See: [テンプレートからリポジトリを作成する - GitHub Docs](https://docs.github.com/ja/github/creating-cloning-and-archiving-repositories/creating-a-repository-from-a-template)
2. 本リポジトリのルートディレクトリに、 EV3RT のアプリケーションソースコードを格納
    - 例: [hakoniwa-scenario-samples/single-robot/line_trace](https://github.com/toppers/hakoniwa-scenario-samples/tree/master/single-robot/line_trace) 内の全ファイルをコピーする(※ 「line_trace ディレクトリを格納する」ではないことに注意)
3. 本リポジトリのルートディレクトリを VSCode で開く
4. VSCode 左下の `Open a remote window` ボタンを押下 -> `Remote-Containers: Reopen in Container` を選択

### 2. ビルド

1. ターミナルを開く
    - カレントディレクトリが `/ev3rt-athrill-v850e2m/sdk/workspace/app` になっている
2. EV3RT SDK のワークスペースディレクトリへ移動
    - `cd /ev3rt-athrill-v850e2m/sdk/workspace`
3. ビルド
    - `make img=app`
4. 実行
    - `make img=app start`

