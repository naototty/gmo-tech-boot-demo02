# gmo-tech-boot-demo02
gmo tech boot camp demo02_03 (PC Virtulization and Cloud)

This repo is gmo boot camp demo01.
https://github.com/naototty/gmo-tech-boot-demo02

まずは、Local PCでの仮想化
webのLB, Reverse Proxy(Layer 7)

## 1) destroy demo02_02 vm, IF you did not destroy vm

``` bash
  vagrant destroy
```


## 2) make Hands on "demo02_03" work dir

``` bash
  cd ..

  mkdir demo02_03
  cd demo02_03
  pwd
```


## 3) git clone "demo02_03" hands on environment

gitで branch demo02_03 を取ってきます

``` bash
  git clone https://github.com/naototty/gmo-tech-boot-demo02.git

  ls 

  cd gmo-tech-boot-demo02
 
  git checkout demo02_03
```

git cloneして、branchを demo02_03 に変更します

git branchの確認

``` bash
  git branch

* demo02_03 <<< これが出る
  master
```



## 4) vagrant up "demo02" server

``` bash

  vagrant up
```


## 5) view http://192.168.33.11/ on web browser

  うまく起動まで行けば、つぎのURLでwebが立ち上がり、phpのphpinfo()の実行を確認できる 
 
  http://192.168.33.11/


### 5-A) hostsの設定

今はテストなので、hosts に ホスト名を設定します。

  * Mac OS Xの場合
    * 初期のインストールのところで入れた Hostsというツールで設定
      - コントロールパネルに "Hosts" という設定ツールが増えている
    * または、手動で書き換え(Editor)

  * Windowsの場合
    * 初期のインストールのところで入れた Hosts File editorというツールで設定
      - アプリケーションメニューに "Hosts File Editor" が増えている
    * または、手動で書き換え(Editor)


## 6) ssh web server

``` bash

  vagrant ssh node1
  sudo su -
```

or 

``` bash

  ssh -l vagrant 192.168.33.11
  sudo su -
```


