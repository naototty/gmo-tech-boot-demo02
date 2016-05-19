# install_setup_win_chocolatey.md
===============

HandsOnでは、Mac OS XとWindowsで共に開発に必要な環境をセットアップして利用します。Macでは"HomeBrew", Windowsでは"Chocolatey"です。

下記では、WindowsでのLocal環境構築をまず記載します
(Windows 7以上, 検証Windows 7 Pro)

## Chocolatey

Windowsで開発環境などを整えるツールです。
HandsOnでの初期セットアップです。

**
すでに、Vagrant, dockerの環境を手元のPCに構築している人は、講師の人々又はアシスタント担当者に聞いて進めてください。
**

> 公式サイト
https://chocolatey.org/


### PowerShell policy (win8, win10)

powershellのpolicyを変更する必要があるかもしれませんので、下記を実行して確認します。

powershellを開きます

```powershell
PS C:\> Get-ExecutionPolicy
Restricted
```

Restrictedの場合には、下記のコマンドでpolicyを変更します。

```powershell
PS C:\> Set-ExecutionPolicy -ExecutionPolicy Unrestricted

```
または

(Windows 7)
```powershell
PS C:\> Set-ExecutionPolicy RemoteSigned

```

  - RemoteSigned : 信頼した署名が入ったものは実行できる
  - Unrestricted : 制限なし

(Windows 8.1)で現在のユーザだけ変更するには下記のようにするようです
```powershell
PS C:\> Set-ExecutionPolicy -Scope CurrentUser RemoteSigned

```


制限のPolicy変更の内容については下記のURLを確認してください。

https://technet.microsoft.com/ja-jp/library/ee176961.aspx

セキュリティ的に気になる方は、最初にGet-ExecutionPolicyで取得した値をメモしておき、ハンズオンが終わったら、その値に戻します。


### chocolatey のインストール

powershellで、下記のコマンドを入力します。
powershellは管理者権限のものを使ってください

```powershell
iex ((new-object net.webclient).DownloadString('https://chocolatey.org/install.ps1'))
```

powershell v3+(v3以上)の環境では、下記のようにしても実行できます

```powershell
iwr https://chocolatey.org/install.ps1 | iex
```                                                                                                               
  
## 4) open power shell
``` powershell
  choco /?
```                                                                                                               

## 5) test install; google chrome
``` powershell
  choco list chrome
  choco install -y GoogleChrome
```                                                                                                               

## 6) install VirtualBox
``` powershell
  choco list VirtualBox
  choco install -y VirtualBox VirtualBox.ExtensionPack vagrant wget
```

wget はWindows 8以上などのpowershellが新しい環境では、コマンドレット"wget"と実行バイナリ"wget.exe"で
結果が異なることになります。


## 7) install git command, hosts.editor, Editor
インストールで、エクスプローラを開いている場合には、すべて閉じておいてください

``` powershell
  choco list git
  choco install -y hosts.editor
  choco install -y git.commandline
  choco install -y git.install
```

すごくダウンロードが遅い場合(github.comからの制限)
処理をキャンセルしてから、Homeディレクトリでファイルを取得して、インストールします


``` powershell
　PS C:\> cd ~
  PS C:\Users\hoge\> choco uninstall -y git.install
  PS C:\Users\hoge\> wget.exe https://conoha.macpoi.me/demo02/Git-2.8.2-64-bit.exe
  PS C:\Users\hoge\> .\Git-2.8.2-64-bit.exe /silent
```

and close AlL powershell window.

### 7-A) install Visual Studio Code insiders
趣味の問題(GUI editor)

``` powershell
  choco install -y visualstudiocode-insiders
```

Visual Studio Code insidersをインストールする場合、一度起動してupdateをかけると、最新版が利用できます。

入れるEditorはなんでも良いですが、改行コード(LF, CRLF)、文字コード(utf8)などが扱えるものにしてください。


### 7-B) install vim-x64
趣味の問題(CUI/CLI editor)

``` powershell
  choco install -y vim-x64
```


## 8) install putty, openssh
``` powershell
  choco list openssh
  choco install -y win32-openssh
  choco install -y putty.install
```
and close power shell window.


## 9) install openssh (ssh command client for power shell)
execute Windows PowerShell with Administrator roles

open new Administrator powershell : "管理者として実行する"
(pathを通すSetメソッドは、powershell管理者権限が必要)

``` powershell
Windows PowerShell
Copyright (C) 2013 Microsoft Corporation. All rights reserved.

PS C:\> $path = [Environment]::GetEnvironmentVariable('PATH', 'Machine')
PS C:\> $path += ';' + 'C:\git\bin'
PS C:\> [Environment]::SetEnvironmentVariable('PATH', $path, 'Machine')
PS C:\>
```
and close AlL powershell window.
  
open new power shell

powershellのwindowを開き直すことで、sshのpathが通っている状態の端末となる


## 10) install python2

OpenStack clientの環境をWindowsに作ります。
~~~ bash
  choco search python2
  choco install -y python2
~~~

実は、殆どの場合、うまく行きません。
ここで、もし失敗した場合、python2を手動でインストールします。

https://www.python.org/downloads/windows/

直近(2016/05/19)、2.7.11が最新のようなので、それを選択します

https://www.python.org/downloads/release/python-2711/

wgetがインストール済みなので、wgetで取得します

``` powershell
　PS C:\> cd ~
  PS C:\Users\hoge\> choco uninstall -y python2
  PS C:\Users\hoge\> wget.exe https://conoha.macpoi.me/demo02/python-2.7.11.amd64.msi
  PS C:\Users\hoge\> .\python-2.7.11.amd64.msi /passive
```

インストールできると、"(すべての)プログラム" メニューに "Python 2.7" が追加されます。

powershellで使うには、powershellを一回閉じます。

powershellをもう一度開いて、python が使えない場合、pathを通します。
(Setメソッドは、powershell管理者権限が必要)

``` powershell
PS C:\> $path = [Environment]::GetEnvironmentVariable('PATH', 'Machine')
PS C:\> $path += ';' + 'C:\tools\python2'
PS C:\> $path += ';' + 'C:\tools\python2\Scripts'
PS C:\> [Environment]::SetEnvironmentVariable('PATH', $path, 'Machine')
```


## 11) install virtualenv, virtualenvwrapper

windows版のpython2.7.11では、pipが最初に入っていますが、upgradeが必要です。

``` powershell
PS N:\> easy_install-2.7.exe --upgrade pip

PS N:\> pip --version
pip 8.1.2 from C:\tools\python2\lib\site-packages (python 2.7)
```

作業の為のvirtualenvのツールをいれます。
(場合によっては、"--upgrade" オプションを入れる必要があるかも)

``` powershell
PS N:\> pip install virtualenv
PS N:\> pip install virtualenvwrapper
PS N:\> pip install virtualenvwrapper-win
```

以上、ここまでが環境セットアップになります。
