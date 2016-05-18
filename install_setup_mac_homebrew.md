# install_setup_mac_homebrew.md
===============

HandsOnでは、Mac OS XとWindowsで共に開発に必要な環境をセットアップして利用します。Macでは"HomeBrew", Windowsでは"Chocolatey"です。

下記では、MacでのLocal環境構築をまず記載します

## HomeBrew

Mac OS X(Yosemite:10.10.x, El Capitan:10.11.x)でのHandsOnでの初期セットアップです。

**
すでに、Vagrant, dockerの環境を手元のPCに構築している人は、講師の人々又はアシスタント担当者に聞いて進めてください。
**

> 公式サイト(ja:日本語)
http://brew.sh/index_ja.html


### "Xcode"と"Command Line Tools for Xcode"のインストール
Mac OS Xにはrubyが入っていますので、それを利用します。
また、インストールでコンパイルが必要な物は、XcodeのCLI Toolsが必要なので、それをまずインストールします。

"xcode-select" というコマンドが、標準で入っています。

```bash:CLI
$ xcode-select --install
xcode-select: note: install requested for command line developer tools
```

コマンドを叩いて、xcodeが入っていない場合、Dialogが開いて、インストールされるように誘導されます。

Xcode自体が入っていない場合には、ここで開いたDialogの「Xcodeを入手」のボタンをおして、まずインストールします。

入っていない場合には、Mac App StoreからXcodeを検索して、Xcodeをインストールします。


xcodeが入っている場合には下記のようなメッセージになるようです。

```bash:CLI
$ xcode-select --install
xcode-select: error: command line tools are already installed, use "Software Update" to install updates
```


Xcodeの入手では、以下のURLからMac App Storeに移動できます
https://developer.apple.com/xcode/download/jp/


!["xcode app store"](https://raw.github.com/wiki/naototty/gmo-tech-boot-demo02/images/xcode_app_store.png "xcode app store")



### HomeBrewのインストール

xcodeインストール後、terminalを開いて、HomeBrewをインストールします


公式 HomeBrew インストールコマンド
```bash
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

以下の流れです
  * "RETURN" keyを押す
  * ログイン時のパスワード(sudoでadmin権限で実行するため)
  * 'Installation successful!'と表示された

インストールできた場合、次のコマンドが実行できます。

```bash
$ brew help

2nd-ConoHa-MacBook-Pro:~ chroum$ brew help
Example usage:
  brew search [TEXT|/REGEX/]
  brew (info|home|options) [FORMULA...]
  brew install FORMULA...
  brew update
  brew upgrade [FORMULA...]
  brew uninstall FORMULA...
  brew list [FORMULA...]

Troubleshooting:
  brew config
  brew doctor
  brew install -vd FORMULA

Brewing:
  brew create [URL [--no-fetch]]
  brew edit [FORMULA...]
  https://github.com/Homebrew/brew/blob/master/share/doc/homebrew/Formula-Cookbook.md

Further help:
  man brew
  brew help [COMMAND]
  brew home
```

さあ、helpは表示できましたか?

'brew doctor'で環境を確認できます。

```bash:file.sh
2nd-ConoHa-MacBook-Pro:~ chroum$ brew doctor
Please note that these warnings are just used to help the Homebrew maintainers
with debugging if you file an issue. If everything you use Homebrew for is
working fine: please don\'t worry and just ignore them. Thanks!

Warning: Your XQuartz (2.7.7) is outdated
Please install XQuartz 2.7.8:
  https://xquartz.macosforge.org

Warning: You have unlinked kegs in your Cellar
Leaving kegs unlinked can lead to build-trouble and cause brews that depend on
those kegs to fail to run properly once built. Run \`brew link\` on these:
    ghostscript

Warning: Broken symlinks were found. Remove them with \`brew prune\`:
    /usr/local/share/man/man1/brew-cask.1

Warning: Some installed formula are missing dependencies.
You should \`brew install\` the missing dependencies:
  brew install jpeg libtiff little-cms2

Run \`brew missing\` for more details.
```

"Warning:"で表示されているところは、 なにかあったら、振り返って治す必要があるかもしれないところです。なにかでインストール失敗などした時に、"brew docker" コマンドで確認します。


## install HandsOn Tools

ハンズオンで使用するツールをインストールしていきます。


### Castroom

brewのpluginのリポジトリのようなものです。

手動でインストールするようなアプリケーションを、コマンドラインでインストールすることができます。

公式サイトは以下です: HomeBrew Cast
https://caskroom.github.io/

セットアップします。

```bash
brew tap caskroom/cask
```


### git
gitはCVS(コンテンツ・バージョン管理・システム)です。githubを活用しますので、インストールします。

```bash
$ brew install git
```

### virtualbox, virtualbox-extension-pack
先ほど入れたHomeBrew Castを活用します

"virtualbox" で brewコマンドでsearchすると、以下のものが検索されます。

```bash
2nd-ConoHa-MacBook-Pro:~ chroum$ brew search virtualbox
Caskroom/cask/virtualbox-extension-pack        Caskroom/cask/virtualbox                       Caskroom/versions/virtualbox-beta
```

virtualbox本体とextension-packが必要なので、インストールします。

```bash
$ brew install Caskroom/cask/virtualbox
$ brew install Caskroom/cask/virtualbox-extension-pack
```

実行すると以下の結果になります

```bash
2nd-ConoHa-MacBook-Pro:~ chroum$ brew install Caskroom/cask/virtualbox
==> Tapping caskroom/cask
Cloning into '/usr/local/Library/Taps/caskroom/homebrew-cask'...
remote: Counting objects: 3645, done.
remote: Compressing objects: 100% (3588/3588), done.
remote: Total 3645 (delta 57), reused 809 (delta 35), pack-reused 0
Receiving objects: 100% (3645/3645), 5.95 MiB | 376.00 KiB/s, done.
Resolving deltas: 100% (57/57), done.
Checking connectivity... done.
Tapped 1 formula (3,613 files, 13.7M)
==> brew cask install Caskroom/cask/virtualbox
==> Downloading http://download.virtualbox.org/virtualbox/5.0.20/VirtualBox-5.0.20-106931-OSX.dmg
######################################################################## 100.0%
==> Verifying checksum for Cask virtualbox
==> Running installer for virtualbox; your password may be necessary.
==> Package installers may write to any location; options such as --appdir are ignored.
Password:
==> installer: Package name is Oracle VM VirtualBox
==> installer: Upgrading at base path /
==> installer: The upgrade was successful.
🍺  virtualbox staged at '/opt/homebrew-cask/Caskroom/virtualbox/5.0.20-106931' (4 files, 86M)
```

こんな感じで、インストールされます。

"virtualbox-extension-pack"もインストールします。

(sudoでadmin権限が必要[timeoutしていないとき]なときには、パスワードが聞かれますので、注意してください)

```bash
2nd-ConoHa-MacBook-Pro:~ chroum$ brew install Caskroom/cask/virtualbox-extension-pack
==> brew cask install Caskroom/cask/virtualbox-extension-pack
==> Satisfying dependencies
==> Installing Cask dependencies: virtualbox
virtualbox ...
already installed
complete
==> Downloading http://download.virtualbox.org/virtualbox/5.0.20/Oracle_VM_VirtualBox_Extension_Pack-5.0.20-106931.vbox-extpack
######################################################################## 100.0%
==> Verifying checksum for Cask virtualbox-extension-pack
Password:
0%...10%...20%...30%...40%...50%...60%...70%...80%...90%...100%
Successfully installed "Oracle VM VirtualBox Extension Pack".
🍺  virtualbox-extension-pack staged at '/opt/homebrew-cask/Caskroom/virtualbox-extension-pack/5.0.20-106931' (16M)
```

### Editor: vim

Terminalでの編集用(入れるかどうかは、おまかせです)に入れます

```bash
$ brew install vim
```

### Editor: code, visual-studio-code-insiders

GUIでの編集用(おまかせ)に入れます

```bash
$ brew install Caskroom/versions/visual-studio-code-insiders
```

CLIでインストール後、"Applications"に入っているので、選択して起動します


!["visual_studio_code_insiders.png"](https://raw.github.com/wiki/naototty/gmo-tech-boot-demo02/images/visual_studio_code_insiders.png "visual_studio_code_insiders.png")


起動後、MacのTerminalから"code"コマンドで呼び出せるように設定を入れます。
メニュー"表示(V)" >> コマンドパレット(C)... 
を選択

!["vsc_menu_command_pallet.png"](https://raw.github.com/wiki/naototty/gmo-tech-boot-demo02/images/vsc_menu_command_pallet.png "vsc_menu_command_pallet.png")



「コマンド窓」にshellと入れると、補完されて２つのコマンドが表示されます。

「シェルコマンド:PATH内に'code'コマンドをインストールします」 \
"Shell Command: Install 'code' command in PATH"

vsc_shell_input.png
!["vsc_shell_input.png"](https://raw.github.com/wiki/naototty/gmo-tech-boot-demo02/images/vsc_shell_input.png "vsc_shell_input.png")

これを選択してインストール後、"Visual Studio code insiders"は一旦終了しておきます

vsc_shell_input_done.png
!["vsc_shell_input_done.png"](https://raw.github.com/wiki/naototty/gmo-tech-boot-demo02/images/vsc_shell_input_done.png "vsc_shell_input_done.png")


### wget

```bash
$ brew install wget
```

### bash-completion

```bash
$ brew install bash-completion
```

インストール後に、自分の .bashrcに設定を追加します
(以下をコピペして実行してください)

```bash
cat >> ~/.bash_profile << __EOF
  if [ -f \$(brew --prefix)/etc/bash_completion ]; then
    . \$(brew --prefix)/etc/bash_completion
  fi

__EOF

```


##  python環境セットアップ

OpenStackのCLIなどのツールはpythonで書かれています。

ConoHaはOpenStackなので、pythonをPCに入れます。


### pip, virtualenv, virtualenvwrapper

python 2.7は標準で入っていますが、pipが入ってないかもしれませんので、インストールします。

```bash
$ sudo /usr/bin/easy_install-2.7 pip
```

pipを使って、virtualenv, virtualenvwrapper をいれます。

```bash
$ sudo pip install virtualenv virtualenvwrapper
```

virtualenvwrapperの設定をbashにいれます。

```bash
$ echo ". /usr/local/bin/virtualenvwrapper.sh" >> ~/.bash_profile
```

初回は手動で読み込みます。つづけて、"openstack"という名称でvirtualenvをつくります。
```bash
$ . /usr/local/bin/virtualenvwrapper.sh
$ mkvirtualenv openstack
```

実行例、実行されると、プロンプトの先頭に"(openstack)"とvirtualenvの名称が付きます

```bash
$ mkvirtualenv openstack
New python executable in /Users/chroum/.virtualenvs/openstack/bin/python
Installing setuptools, pip, wheel...done.
virtualenvwrapper.user_scripts creating /Users/chroum/.virtualenvs/openstack/bin/predeactivate
virtualenvwrapper.user_scripts creating /Users/chroum/.virtualenvs/openstack/bin/postdeactivate
virtualenvwrapper.user_scripts creating /Users/chroum/.virtualenvs/openstack/bin/preactivate
virtualenvwrapper.user_scripts creating /Users/chroum/.virtualenvs/openstack/bin/postactivate
virtualenvwrapper.user_scripts creating /Users/chroum/.virtualenvs/openstack/bin/get_env_details

(openstack) $
```

環境を作った後に、以前作った"(openstack)"というVirtualenvに切り替えるには、下記のように実行します

```bash
$ . /usr/local/bin/virtualenvwrapper.sh

$ workon openstack

(openstack) $
```

以上、ここまでがセットアップになります。


## README.md に戻る

README.md にもどってください


