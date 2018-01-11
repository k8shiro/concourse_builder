# concourse_builder

docker-composeを実行することでConcourse CIの本体(web, db. worker)とCLIツール(fly)のコンテナを立ち上げます。
パスワードなどは埋め込まれている検証用です。

## 各種パスワード

パスワードはすべて`p@ssw0rd`として埋め込んでいます。

## 起動まで

以下のコマンドを実行してください

```
git clone https://github.com/ko-he-/concourse_builder
cd concourse_builder
./gen_key.sh
docker-compose up -d --build
```
この時点で http://[Docker host ip]:8080 からWebUIを見ることができます。


## CLIツールからログイン

起動しているコンテナ名を確認します。ここでは

- concoursebuilder_fly_1 : CLIツール用コンテナ
- concoursebuilder_concourse-web_1 : APIの宛先用コンテナ

になります。

```
# docker ps --format "{{.Names}}"
concoursebuilder_fly_1
concoursebuilder_concourse-worker_1
concoursebuilder_concourse-web_1
concoursebuilder_concourse-db_1
```


CLIツールがインストールされているflyコンテナにはSSHで入れます(Dockerのホストマシンの2222番ポートに割り当てています)。
パスワードは'p@ssw0rd'です。

```
# Dockerホスト内部から
ssh localhost -p 2222

# Dockerホスト外部から
ssh [Docker host ip] -p 2222
```

ログイン後、flyコンテナからAPIを実行する場合、以下のようにURLにwebコンテナのnameの「concoursebuilder_concourse-web_1」を使用してConcourse CIにログインできます。

- user: `concourse`
- pass: `p@ssw0rd`

```
# Concourse CIにログイン 
fly -t concourseci login -c http://concoursebuilder_web_1:8080
```



