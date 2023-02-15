
# Install

Neuron APIのURL、APIキーを設定してください

```.env
NEURON_API_URL=xxxxxx
NEURON_API_KEY=xxxxxx
```

```bash
docker-compose up -d
```

# 起動・停止



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
"<https://xxxxxx.com/xxx|タイトル[Neuron:https://xxxxxx.com/xxx]>",
"<https://xxxxxx.com/xxx|タイトル[Neuron:https://xxxxxx.com/xxx]>"
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
