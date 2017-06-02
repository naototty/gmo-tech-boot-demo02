# gmo-tech-boot-demo02 demo02_02

gmo tech boot camp demo02_02 (Cloud)

次に、ConoHa cloud での仮想化

## 1) setup gmo tech bootcamp handson env.

まずは、以下のOSごとの環境セットアップを実行して、環境を構築してください。

ConoHa cloud に vagrant up して、desktop PC(Note PC)と同じプロビジョニングをしてみます

作業ディレクトリは、最初にgit clone して、Vagrantfile がある場所です


## 2) git checkout "demo02_02" branch hands on environment

さきほど、以下の操作をして、local PC 環境で vagrantでweb(php)を動かしました
``` bash
  mkdir demo02_01
  cd demo02_01
  pwd
  git clone https://github.com/naototty/gmo-tech-boot-demo02.git
  cd gmo-tech-boot-demo02
  git checkout demo02_01
  vagrant up
```

一つ上のディレクトリ "devel" に戻って、次の "demo02_02" を作ります

demo02_02 の git branch をcheckout します

``` bash
  cd ..
  mkdir demo02_02
  pwd

  git clone https://github.com/naototty/gmo-tech-boot-demo02.git
  cd gmo-tech-boot-demo02
  git checkout demo02_02
```

### 2-a) virtualenv環境の構築


作業用の端末はCentOS 7.xであること (ConoHa上)
kimさんのハンズオンで使ったVMでOK


rootでインストール作業

python の virtualenv,  virtualenvwrapperを入れる


``` bash
# yum -y groupinstall "Development Tools"
# yum -y install readline-devel zlib-devel bzip2-devel sqlite-devel openssl-devel

# yum -y install python-virtualenv python-virtualenvwrapper
```

### 2-b) virtualenv環境の設定 (github使う)

#### github上
先に作ったgithubアカウントで、bashrcを管理するプロジェクトを作ります。


たとえば、"mybashrcenv" とかいう名前の場合

https://github.com/naototty/mybashrcenv

というようになります。


#### 作業用CentOS 7.x

作業端末のConoHa VM で git add / git commit / git push します

``` bash
git clone https://github.com/naototty/mybashrcenv.git

cd mybashrcenv/

cp ~/.bashrc ./mybashrc

git add mybashrc
git commit -a -m'add my bashrc'
git push
```

#### NotePC上

``` bash
git clone https://github.com/naototty/mybashrcenv.git

```

できた "mybashrcenv" フォルダを Visual Studio Code で
 Open >> "mybashrcenv" を選択

します。

mybashrc ファイルを左で選択します。
>> エディタで表示されます。


以下の内容をVisual Studio Codeで追記します。

``` shell
### Virtualenvwrapper for GTB2017
if [ -f /usr/bin/virtualenvwrapper.sh ]; then
    export WORKON_HOME=$HOME/devel/gtb2017/.virtualenvs
    source /usr/bin/virtualenvwrapper.sh
fi

```

Visual Studio Codeでコミットします。
git pushします


### 2-c) virtualenv環境の設定 (github使わない)

virtualenvのdirを作成

``` shell
mkdir -p $HOME/devel/gtb2017
```

shellで以下を実行、

``` shell
cat >> .bashrc << __EOF_

### Virtualenvwrapper for GTB2017
if [ -f /usr/bin/virtualenvwrapper.sh ]; then
    export WORKON_HOME=$HOME/devel/gtb2017/.virtualenvs
    source /usr/bin/virtualenvwrapper.sh
fi

__EOF_

```

"openstack" という作業用virtualenvを作る

初回は手動で読み込みます。つづけて、"openstack"という名称でvirtualenvをつくります。
```bash
$ . /usr/bin/virtualenvwrapper.sh
$ mkvirtualenv openstack
```

実行例、実行されると、プロンプトの先頭に"(openstack)"とvirtualenvの名称が付きます

```bash
$ mkvirtualenv openstack
New python executable in /root/devel/gtb2017/.virtualenvs/openstack/bin/python
Installing setuptools, pip, wheel...done.
virtualenvwrapper.user_scripts creating /root/devel/gtb2017/.virtualenvs/openstack/bin/predeactivate
virtualenvwrapper.user_scripts creating /root/devel/gtb2017/.virtualenvs/openstack/bin/postdeactivate
virtualenvwrapper.user_scripts creating /root/devel/gtb2017/.virtualenvs/openstack/bin/preactivate
virtualenvwrapper.user_scripts creating /root/devel/gtb2017/.virtualenvs/openstack/bin/postactivate
virtualenvwrapper.user_scripts creating /root/devel/gtb2017/.virtualenvs/openstack/bin/get_env_details

(openstack) $
```

## 3) openstack client(OSC) installation on python virtualenv

branch "demo02_02" をcheckoutすると、ファイルが変化します。


OpenStack Clientをlocal PC にインストールします

先ほど作成した python の virtualenv を "openstack" に切り替えます

``` bash
$ workon openstack
(openstack)$ pip install -r pip-freeze-centos7-py27.txt

```

### 3-A) OSC(OpenStack client)について、GoogleでConoHaでの操作について
検索してみよう

keyword:
  "OpenStack client OSC ConoHa"

### OSCの設定ファイルを作って読み込む

sjc1 リージョンの環境で、設定を作ります

Linux, Mac OS X, (Windows 10 bash)の場合
``` bash
$  cat osrc_personal_conoha_sjc1

ID_EMAIL='naoto-gohko@plastic-machine.red'

## IF your login conoha control panel
## See. API page : https://manage.conoha.jp/API/

export OS_TENANT_NAME='gnct5********'
export OS_TENANT_ID='aefde******************'

export OS_PASSWORD='hoge*****'
export OS_USERNAME='gncu5*******'

## bellow :: no change
## We use sjc1 region (US, San Jose)
export OS_AUTH_URL='https://identity.sjc1.conoha.io/v2.0/'
export OS_REGION_NAME=sjc1

export OS_VOLUME_API_VERSION=2
export OS_IMAGE_API_VERSION=2
export OS_COMPUTE_API_VERSION=2
export PS1='[\u@\h \W(keystone_nwe_conoha_$OS_USERNAME.$OS_REGION_NAME)]\$ '

```

上記のファイルを編集して、設定します

ex) Windowsの環境変数ってどうやるのかな?


windows powershell の場合
``` powershell
$  cat osrc_personal_conoha_sjc1.ps1

$env:ID_EMAIL='naoto-gohko@plastic-machine.red';

## IF your login conoha control panel
## See. API page : https://manage.conoha.jp/API/

$env:OS_TENANT_NAME='gnct5********';
$env:OS_TENANT_ID='aefde******************';

$env:OS_PASSWORD='hoge*****';
$env:OS_USERNAME='gncu5*******';

## bellow :: no change
## We use sjc1 region (US, San Jose)
$env:OS_AUTH_URL='https://identity.sjc1.conoha.io/v2.0/';
$env:OS_REGION_NAME="sjc1";

$env:OS_VOLUME_API_VERSION=2;
$env:OS_IMAGE_API_VERSION=2;
$env:OS_COMPUTE_API_VERSION=2;

```


## 4) vagrant up "demo02_02" server




``` bash

  vagrant up
```


## 5) view http://(vmのIP)/ on web browser

  うまく起動まで行けば、つぎのURLでwebが立ち上がり、phpのphpinfo()の実行を確認できる 
 
  http://(vmのIP)/


## 6) ssh web server

``` bash

  vagrant ssh node1
  sudo su -
```

or 

``` bash

  ssh -l vagrant (vmのIP)
  sudo su -
```


