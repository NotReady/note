# Shell

## 監視
---
### ログ

```
tail -F {ファイル}
```
### 定期実行
任意のコマンドを定期実行する
```
watch   [-n] {1(sec)}
        '{コマンド}'
```

## ユーザ
---
### ユーザを作成する
---
```
useradd [-m]    # ホームディレクトリ作成 
        {ユーザ名}
```

### パスワードを設定する
---
```
passwd {ユーザ名}
```

### 鍵作成
---
```
cd /path/to/userhome/.ssh

[ansible@localhost .ssh]$ ssh-keygen -t rsa
Generating public/private rsa key pair.
Enter file in which to save the key (/home/ansible/.ssh/id_rsa): 
Enter passphrase (empty for no passphrase): 
Enter same passphrase again: 
Your identification has been saved in /home/ansible/.ssh/id_rsa.
Your public key has been saved in /home/ansible/.ssh/id_rsa.pub.
The key fingerprint is:
SHA256:WP5XOwrqo9xBO8GYXdXk7/q3DTUIy2XXBBHnUfcZvUc ansible@localhost.localdomain
The key's randomart image is:
+---[RSA 2048]----+
|            .o=*B|
|           . ..+E|
|        . .. o.+=|
|       O .. = oo.|
|      + S  o ...+|
|       . +   . +.|
|        + o . + .|
|     . ..+ o . +o|
|      oo+.  . .o=|
+----[SHA256]-----+

[ansible@localhost .ssh]$ ls -lav
-rw-------. 1 ansible ansible 1675 Dec 12 16:40 id_rsa
-rw-r--r--. 1 ansible ansible  411 Dec 12 16:40 id_rsa.pub

```

## ネットワーク
***
### DNS
***

```
dig {dns名}
```

```
nslookup {dns名|ipアドレス}
```
### パフォーマンス
***
> http://www.math.kobe-u.ac.jp/HOME/kodama/tips-free-memory.html


プロセスとリソースのトレース
```
top    [-M] # 消費メモリ順
```

使用メモリのトレース
```
free

              total        used        free      shared  buff/cache   available
Mem:        1014972      506384       80460        7064      428128      323132
Swap:       2097148         264     2096884

Linuxは余剰メモリをバッファ(buffer)とキャッシュ(cache)に利用してディスク入出力の負荷を減らしている。そのためfreeコマンド等で見える残りメモリ－(free)は 1M 程度の 瞬間的な使いまわしに対処する程度しか残っていない事が多いが、実質的な残りメモリ－はバッファとキャッシュに転用された分も考慮すると以下の通り。
> free(80460) + buffer/cache(428128) = 508,588k
```
## HTTPクライアント
***
### CURL
---
```
curl [-sS]  # s:進捗表示なし S:エラーは表示 
     [-k]   # 証明書エラー無視
     [-u] {user}:{password}  # 認証ユーザ
     [-c] {出力ファイルパス}  # cookieをファイルに保存する
     [-b] {入力ファイルパス}  # cookieをファイルから入力する
     [-o] {出力ファイルパス}  # ダウンロードしたデータをファイルに保存する
     [-O] {出力ファイルパス}  # レスポンスをそのままファイルに保存する
     [-L] リダイレクトを追跡する
     {URL}

```