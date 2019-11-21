# apacheメモ #
## .htaccess ##
***
### Satisry 認証論理 ###
---
IP制限やBasic認証を一緒にかけた場合の認証通過方法
```
Satisfy Any・・・いずれかの条件を満たせば通過
Satisfy All・・・全ての条件を満たせば通過
※どこに定義しても良い
```
### order IP制限 ###
---
***リバプロ、ロードバランサを中継する場合は、IP制限は使えないのでFWでガードする。***

order Deny,Allow（ホワイトリスト）
```
1. Deny ディレクティブが Allow ディレクティブの前に評価する
2. Deny ディレクティブが未定義の場合、デフォルトは全許可する
3. Deny ディレクティブに合わないか、Allow ディレクティブに合うクライアントはアクセスを許可する
```
order Allow,Deny（ブラックリスト）
```
1.Allow ディレクティブが Deny ディレクティブの前に評価する
2.Allow ディレクティブが未定義の場合、デフォルトは全拒否する
3.Allow ディレクティブに合わないか、Deny ディレクティブに合うクライアントはアクセスを拒否する
```
### BASIC認証のキャッシュ削除 ###
---

* Chrome
    1. キャッシュの削除  
    chrome://settings/clearBrowserData
    1. 再起動  
    chrome://restart

## .htpasswd
***
* パスワード9文字以上はMD5エンコードする
* エンコードツール  
https://www.softel.co.jp/labs/tools/basic-auth/

### 特定URLのBASIC認証 ###
---

#### フレームワーク系

ブートストラップ(index.php)を必ず踏むフレームワークの場合はブートストラップを別名コピーして、認証させるurlを別名ブートストラップにリダイレクトしてベーシック認証をかける
```
<IfModule mod_rewrite.c>
    RewriteEngine On
    # 通常ブートストラップの前に認証用のブートストラップリダイレクトを入れる
    # ここから
    RewriteCond %{REQUEST_FILENAME} !-d
    RewriteCond %{REQUEST_FILENAME} !-f
    RewriteCond %{REQUEST_URI} ^.*hoge.*$
    RewriteRule ^(.*)$ index.auth.php?_url=/$1 [QSA,L]
    # ここまで
    RewriteCond %{REQUEST_FILENAME} !-d
    RewriteCond %{REQUEST_FILENAME} !-f
    RewriteRule ^(.*)$ index.php?_url=/$1 [QSA,L]
</IfModule>

<Files index.auth.php>
  AuthType Basic
  AuthName "Input your ID and Password." 
  AuthUserFile /var/www/.htpasswd.hoge
  require valid-user
</Files>
```

### 定義済変数などシンタックスのメモ ###
---

```
<IfModule mod_rewrite.c>
    RewriteEngine On # 必須
    /**
     * RewriteCond 直後のRewriteRule実行の判定条件 RewriteCondの連続指定はデフォルトでAND結合、[OR]は指定可能
     *
     * 定義済変数
     * %{HTTP_HOST}            リクエストのホスト部のみ httpd:// { www.hoge.com } /index
     * %{REQUEST_URI}         リクエストのホスト部以降 ( ルートのスラッシュ含む ）http://hoge.com { /path/to/action?param=fuga&... }
     */
    RewriteCond %{REQUEST_URI} ^.*hoge.*$
    RewriteRule ^(.*)$ index.auth.php?_url=/$1 [QSA,L]
</IfModule>
```