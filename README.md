# Nginx STATUS Module (json Output)
## 概要
Nginxの可動ステータスをjson形式で出力します。  
オリジナルソースのjson形式が微妙に困ったので、修正してみました。

## 使い方
### コンパイル＆インストール
1. Nginxをインストールしたいサーバーにソースをデプロイ
1. Nginxをmakeする前にconfigureでモジュールを組み込み	
1. ```./configure --add-module=/path/to/nginx-json-status-module``` でコンパイル
1. Nginxをmake && make install

詳細は [InstallOptions - Nginx Community :](http://wiki.nginx.org/InstallOptions) を参考にしてみてください

### Nginxへの組み込み方
nginx.confのServer部分に組み込んで下さい

```
  location /nginx_status.js {
    json_status         on;
    json_status_type    text/javascript; # Default application/json
    access_log          off;
  }
```

###  確認方法
1. curl http://localhost/nginx_status.js みたいにHTTPでアクセスする
1. ``` {"active":3,"accepts":290,"handled":290,"requests":9,"reading":0,"writing":1,"waiting":2} ``` みたいに返ってくる

## ChangeLog
2014/09/16 - 初版

## 以下オリジナルドキュメント
[ORIGINAL SOURCE - nginx-json-status-module](https://github.com/lindsayevans/nginx-json-status-module)

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