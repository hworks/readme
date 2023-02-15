
# Install

①Neuronの設定
scriptsディレクトリ内の.envファイルに、
Neuron APIのURL、APIキーを設定してください

```.env
NEURON_API_URL=xxxxxx
NEURON_API_KEY=xxxxxx
```

②コンテナの起動

```bash
docker-compose up -d
```
---
＜Dockerイメージを利用して構築する場合＞

・Dockerのイメージを展開する
```bash
docker load < oudan-server.tar

```
　イメージが作成されたか確認する
```bash
docker images

```

oudan-server_oudan-webapiのイメージが作成されていれば成功



# 起動・停止

コンテナ起動
```bash
docker-compose up -d
```

コンテナ停止
```bash
docker-compose down
```
or（コンテナを削除しない場合）
```bash
docker-compose stop
```


# 使い方


| 横断検索連携サーバ(WebAPI)                             ||
| ------            | -----                              |
| プロトコル        | HTTP                               |
| 文字コード        | UTF-8                              |
| content-type      | application/x-www-form-urlencoded  |
| リクエスト                                             ||
| メソッド          | GET                                |
| エンドポイントURL | http://{サーバIP}:3030/api/search/ |
| ヘッダパラメータ  | なし                               |
| ボディパラメータ                                       ||
| キー              | 説明                               |
| q                 | （必須）検索文字                   |
| rows              | （オプション）回答件数　初期値は2  |
| 例）q=＜検索文字＞                                     ||
| レスポンス                                             ||
| レスポンス形式    | JSON形式                           |

例）curlの場合

curl 'http://{サーバIP}:3030/api/search/?q=検索文字'


例）結果(JSON形式)

[
"<https://xxxxxx.com/xxx|タイトル[情報元]",
"<https://xxxxxx.com/xxx|タイトル[情報元]>"
]




## ファイル構成
- docker-compose.yml, Dockerfile 環境構築用の設定ファイル
- requirements.txt: pip install パッケージリスト
- scripts: スクリプトファイルの格納フォルダ
    - app.py: メインモジュール
    - NeuronApi.py: NeuronApi用のクラス
    - moji.py: 形態素解析用のクラス
    - logger_config.json: ロガー設定ファイル
    - .env: 設定ファイル

oudan-server-prod/
├ docker-compose.yml
├ Dockerfile
├ requirements.txt
└  scripts/
        ├ .env
        ├ app.py
        ├ moji.py
        ├ NeuronApi.py	
        └  logger_config.json


## 動作確認

docker exec -it oudan-server-prod bash
python3 -m Neuron '検索キーワード'

正常な場合
Neuron検索の結果がSlackのハイパーリンクの形式で出力される。
異常な場合
エラー内容が出力される。
タイムアウトが発生する。
.evnの横断検索のURLとAPIキーが正しいか確認する。
横断検索が動作しているか確認する。






