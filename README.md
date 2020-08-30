#### kataribeをインストール
1. `go get -u github.com/matsuu/kataribe`
2. `kataribe -generate`
3. nginx.confの編集
```
log_format with_time '$remote_addr - $remote_user [$time_local] '
                     '"$request" $status $body_bytes_sent '
                     '"$http_referer" "$http_user_agent" $request_time';
access_log /var/log/nginx/access.log with_time;
```

