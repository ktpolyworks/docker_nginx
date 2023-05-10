# docker_cakephp4_base
docker / cakephp4 / php7.4 / mysql5.7

docker baseをclone
```
git clone https://github.com/ktpolyworks/docker_cakephp4_base.git
clone後フォルダ名を変更 testblog等
```

dockeriイメージ作成
```
$ docker-compose build
```

dockerコンテナ起動
```
$ docker-compose up -d
```

コンテナが作成されているか確認
```
$ docker ps -a
```

sshログイン
```
$ docker exec -it testblog_phpfpm_1 /bin/sh
```

composerインストール
```
# curl -s https://getcomposer.org/installer | php
```

cakephpインストール
```
# php composer.phar create-project --prefer-dist cakephp/app app
```

docker-compose.ymlのPRJを変更
```
#変更前
PRJ:"tmp"
#変更後
PRJ:"testblog"
```

コンテナ設定をアップデート
```
$ docker-compose up -d
```

webサーバーのroot変更
```
default.conf
#変更前
root /var/www/html;
#変更後
root /var/www/html/app/webroot;
```

nginx再起動
```
$ docker restart testblog_nginx_1
```

DB設定
/config/app.phpのDatasources
```
'host' => 'mysql',
'username' => 'root',
'password' => 'password',
```

完了！

http://localhost
