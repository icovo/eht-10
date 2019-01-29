## オープンソースのBlock Explorerを入手する

```
git clone https://github.com/etherparty/explorer
cd explorer
```

## サーバ上に必要なツールをインストールする

```
sudo apt-get install npm
```

## 設定ファイルを修正する(お好みのエディタで)

```
vim app/app.js
```

下方にある以下の行のlocalhostを、自分のサーバのGlobal IPに変更する

```
//var eth_node_url = 'http://localhost:8545'; // TODO: remote URL
var eth_node_url = 'http://xxx.xxx.xxx.xxx:8545'; // TODO: remote URL
```

```
vim  package.json
```

以下の "start" の行内のlocalhostを、サーバのホスト名に変更。
ec2-xxx-xxx-xxx-xxx.compute-1.amazonaws.com

```
  "scripts": {
    "postinstall": "bower install",
    "prestart": "npm install",
    "start": "http-server ./app -a localhost -p 8000 -c-1",
    "pretest": "npm install",
```

以下の書式でxxx部分に自分のIP
ec2-xxx-xxx-xxx-xxx.compute-1.amazonaws.com

```
  "scripts": {
    "postinstall": "bower install",
    "prestart": "npm install",
    "start": "http-server ./app -a ec2-xxx-xxx-xxx-xxx.compute-1.amazonaws.com -p 8000 -c-1",
    "pretest": "npm install",
```

## gethのRPCポートを解放する
起動しているgethのRPCポートが空いていなければ(以下のオプションをつけて起動していなければ)、
以下のオプションを追加して再起動する。
起動しているgethはkillコマンドで落として良い。

```
geth --rpc --rpccorsdomain "*"
```

## Explorerを起動
```
npm start
```
以下のログが出ていれば正常
```
Starting up http-server, serving ./app on port: 8000
```

## アクセスする
ローカルマシンのブラウザからアクセスする
http://ec2-xxx-xxx-xxx-xxx.compute-1.amazonaws.com:8000

