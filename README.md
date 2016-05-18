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


## 2) make Hands on "demo01" work dir

~~~ bash
  mkdir devel
  cd devel
  mkdir demo01
  cd demo01
  pwd
~~~


## 3) git clone "demo01" hands on environment

~~~ bash
  git clone https://github.com/naototty/gmo-tech-boot-demo02.git

  ls 

  cd gmo-tech-boot-demo02
~~~

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


