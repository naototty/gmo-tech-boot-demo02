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
PS C:\> Set-ExecutionPolicy Unrestricted

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
~~~ bash
  choco /?
~~~

## 5) test install; google chrome
~~~ bash
  choco list chrome
  choco install -y GoogleChrome
~~~

## 6) install VirtualBox
~~~ bash
  choco list VirtualBox
  choco install -y VirtualBox VirtualBox.ExtensionPack vagrant Wget
~~~
仮想化のソフトなので、管理者権限が必要

## 7) install git command
~~~ bash
  choco list git
  choco install -y git git.commandline git.install hosts.editor
~~~

## 8) install putty, ssh
~~~ bash
  choco list ssh
  choco install -y putty.install
~~~
and close power shell window.


## 9) install openssh (ssh command client for power shell)
execute Windows PowerShell with Administrator roles

open new Administrator powershell : "管理者として実行する"
~~~ bash
Windows PowerShell
Copyright (C) 2013 Microsoft Corporation. All rights reserved.

PS C:\Windows\system32> $path = [Environment]::GetEnvironmentVariable('PATH', 'Machine')
PS C:\Windows\system32> $path += ';' + 'C:\git\bin'
PS C:\Windows\system32> [Environment]::SetEnvironmentVariable('PATH', $path, 'Machine')
PS C:\Windows\system32>
~~~
and close AlL power shell window.
  
open new power shell

powershellのwindowを開き直すことで、sshのpathが通っている状態の端末となる


## 9.a) install python2





以上、ここまでがセットアップになります。
