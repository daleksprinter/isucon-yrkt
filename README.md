# ISUCONやること

## Gitセットアップ
1. webappをgit initする
2. nginx.conf, my.cnfをwebappに移動、symlinkを貼る
```
mv /etc/nginx/sites-avaliable/${nginx_conf_file} ${app_dir}
ln -sfv ${app_dir} /etc/nginx/sites-available/${nginx_conf_file}

mv /etc/nginx/nginx.conf ${app_dir}
ln -sfv ${app_dir} /etc/nginx/nginx.conf

mv /etc/mysql/mysql.conf ${app_dir}
ln -sfv ${app_dir} /etc/mysql/mysql.conf
```
3. commit & pushしておく

## 各種スクリプト作成
アプリケーションのディレクトリにMakefile作る
1. ベンチマーク
2. ログローテート
```
cp /var/log/nginx/access.log access.log.$(date "+%Y%m%d%H%M%S").bak
```

## kataribeをインストール
##### Repo `https://github.com/matsuu/kataribe`
1. `go get -u github.com/matsuu/kataribe`
2. `kataribe -generate`
3. nginx.confの編集
```
log_format with_time '$remote_addr - $remote_user [$time_local] '
                     '"$request" $status $body_bytes_sent '
                     '"$http_referer" "$http_user_agent" $request_time';
access_log /var/log/nginx/access.log with_time;
```
