# gmo-tech-boot-demo02
gmo tech boot camp demo02 (PC Virtulization and Cloud)

まずは、Local PCでの仮想化

## 1) 1setup gmo tech bootcamp handson env.

まずは、以下のOSごとの環境セットアップを実行して、環境を構築してください。

localのPCに vagrant などの環境を構築します。


### 1-A) Mac OS X setup
  * mac setup : https://github.com/naototty/gmo-tech-boot-demo02/blob/demo02_01/install_setup_mac_homebrew.md


### 1-B) Windows 7(8, 10) setup
  * win setup : https://github.com/naototty/gmo-tech-boot-demo02/blob/demo02_01/install_setup_win_chocolatey.md


## 2) make Hands on "demo02" work dir

``` bash
  cd ~
  mkdir devel
  cd devel

  mkdir demo02_01
  cd demo02_01
  pwd
```


## 3) git clone "demo02" hands on environment

``` bash
  git clone https://github.com/naototty/gmo-tech-boot-demo02.git

  ls 

  cd gmo-tech-boot-demo02
 
  git checkout demo02_01
```

got cloneして、branchを demo02_01に変更します

git branchの確認

``` bash
  git branch

* demo02_01
  master
```



## 4) vagrant up "demo02" server

~~~ bash

  vagrant up
~~~


## 5) view http://192.168.33.11/ on web browser

  うまく起動まで行けば、つぎのURLでwebが立ち上がり、phpのphpinfo()の実行を確認できる 
 
  http://192.168.33.11/


## 6) ssh web server

~~~ bash

  vagrant ssh node1
  sudo su -
~~~

or 

~~~ bash

  ssh -l vagrant 192.168.33.11
  sudo su -
~~~


