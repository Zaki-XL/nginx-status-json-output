
# NGINX STATUS Module (json Output)
## 概要
NGINXの可動ステータスをjson形式で出力します。
オリジナルソースが正しいjson形式じゃなかったので、修正してみました。

## 使い方
### インストール
1. Nginxをインストールしたいサーバーにソースをデプロイする	
1. ```./configure --add-module=/path/to/nginx-json-status-module``` でコンパイル

### 組み込み方
nginx.confのServer部分に組み込んで下さい
```
  location /nginx_status.js {
    json_status         on;
    json_status_type    text/javascript; # Default application/json
    access_log          off;
  }
```

###  確認方法
1. コンパイルする	
1. confに組み込み
1. curl http://localhost/nginx_status.js みたいにアクセスする

## 以下オリジナルドキュメント
[ORIGINAL SOURCE](https://github.com/lindsayevans/nginx-json-status-module)

> Nginx json_status module
> A version of the Nginx HTTP stub status module that outputs in JSON format
> 
> WARNING:
> This code WILL eat your cat, crash your server and send your bank details to random Nigerian email addresses. Run at your own risk.
>
> Compiling into Nginx:
> ./configure --add-module=/path/to/nginx-json-status-module
> 
> Configuration:
> In your nginx.conf:
>
>  location /nginx_status.js {
>    json_status         on;
>    json_status_type    text/javascript; # Default application/json
>    access_log          off;
>  }
>
>
> Example output - /nginx_status.js:
> {active:1,accepts:1,handled:1,requests:5,reading:0,writing:1,waiting:0}
>
> Callback support - /nginx_status.js?callback=do_funky_stuff:
> do_funky_stuff({active:1,accepts:1,handled:1,requests:5,reading:0,writing:1,waiting:0});