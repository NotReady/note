# Shell

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