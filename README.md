🌙 docker-redis
====

![GitHub issues](https://img.shields.io/github/issues/isystk/docker-redis)
![GitHub forks](https://img.shields.io/github/forks/isystk/docker-redis)
![GitHub stars](https://img.shields.io/github/stars/isystk/docker-redis)
![GitHub license](https://img.shields.io/github/license/isystk/docker-redis)

## 📗 プロジェクトの概要

Redis の学習用サンプルアプリケーションです。

## 📦 ディレクトリ構造

```
.
├── docker （各種Daemon）
│   │
│   └── redis （Redisサーバー）
│       ├── data (Redisのデータファイル)
│       └── Dockerfile
└── dc.sh （Dockerの起動用スクリプト）
```

## 🖊️ Docker 操作用シェルスクリプトの使い方

```
Usage:
  dc.sh [command] [<options>]

Options:
  stats|st                 Dockerコンテナの状態を表示します。
  init                     Dockerコンテナ・イメージ・生成ファイルの状態を初期化します。
  start                    すべてのDaemonを起動します。
  stop                     すべてのDaemonを停止します。
  --version, -v     バージョンを表示します。
  --help, -h        ヘルプを表示します。
```

## 💬 使い方

```
# Dockerを起動する
$ ./dc.sh start

# Redisサーバーにログイン
$ ./dc.sh redis login

# redis-cliを起動
# redis-cli
```

#### Strings型を保存する
最も一般的なKVSのデータ型で、画像も保存できる。
Session管理のためsession-id:値(Json)でデータを保存する。
```
127.0.0.1:6379> keys *
(empty array)
127.0.0.1:6379> set key01 value001
OK
127.0.0.1:6379> get key01
"value001"
127.0.0.1:6379> set key01 value002
OK
127.0.0.1:6379> get key01
"value002"
127.0.0.1:6379> keys *
1) "key01"
```

#### Hash型で保存する
key,field,valueを設定できる。
keyを指定すれば全て取得できて、key,fieldを指定すればvalueを取得する。
Jsonを保存するとkeyで全て、key,fieldで要素ごとに取り出したりできる。
```
127.0.0.1:6379> hset hash_key name test
(integer) 1
127.0.0.1:6379> hset hash_key mail test@test.com
(integer) 1
127.0.0.1:6379> hset hash_key tel 090-0000-0000
(integer) 1
127.0.0.1:6379> hgetall hash_key
1) "name"
2) "test"
3) "mail"
4) "test@test.com"
5) "tel"
6) "090-0000-0000"
127.0.0.1:6379> hget hash_key name
"test"
127.0.0.1:6379> hget hash_key mail
"test@test.com"
127.0.0.1:6379> hget hash_key tel
"090-0000-0000"
```

#### List型で保存する
keyに対して複数の値を設定する
```
# 先頭に追加
127.0.0.1:6379> lpush key01 value001
(integer) 1
127.0.0.1:6379> lpush key01 value002
(integer) 2
127.0.0.1:6379> lpush key01 value003
(integer) 3
# 末尾に追加
127.0.0.1:6379> rpush key01 value004
(integer) 4
127.0.0.1:6379> rpush key01 value005
(integer) 5
127.0.0.1:6379> rpush key01 value006
(integer) 6
# 全て取得
127.0.0.1:6379> lrange key01 0 -1
1) "value003"
2) "value002"
3) "value001"
4) "value004"
5) "value005"
6) "value006"
```

#### データを削除する
現在使用しているDBのデータを削除するeyに対して複数の値を設定する
```
127.0.0.1:6379> flushdb
OK
```

#### ホストからCurlでアクセスする
```
$ curl -s telnet://localhost:6379
keys *
key01
hash_key
```

## 🎨 参考

| プロジェクト| 概要|
| :---------------------------------------| :-------------------------------|
| [docker-composeでredis環境をつくる](https://qiita.com/uggds/items/5e4f8fee180d77c06ee1)| docker-composeでredis環境をつくる |
| [いまさらRedisをさわってみる](https://blog.umeso.net/entry/2020/04/19/021002)| いまさらRedisをさわってみる |


## 🎫 Licence

[MIT](https://github.com/isystk/docker-redis/blob/master/LICENSE)

## 👀 Author

[isystk](https://github.com/isystk)


