 uninstall HomeBrew from Mac OS X "Yosemite"

## uninstall HomeBrew

公式のHomeBrew環境の削除は以下のようになります。

```bash
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/uninstall)"
```

以下のようにして、削除できます。


```bash
2nd-ConoHa-MacBook-Pro:~ chroum$ ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/uninstall)"
Warning: This script will remove:
/Library/Caches/Homebrew/
/Users/chroum/Library/Logs/Homebrew/
/usr/local/.git/
/usr/local/.github/
/usr/local/.gitignore
/usr/local/.travis.yml
/usr/local/.yardopts
/usr/local/CODEOFCONDUCT.md
/usr/local/Cellar/
/usr/local/LICENSE.txt
/usr/local/Library/
/usr/local/README.md
/usr/local/bin/brew
/usr/local/etc/bash_completion.d/brew
/usr/local/share/doc/homebrew/
/usr/local/share/man/man1/brew.1
/usr/local/share/zsh/site-functions/_brew
Are you sure you want to uninstall Homebrew? [y/N] y
==> Removing Homebrew installation...
==> Removing empty directories...
==> Homebrew uninstalled!
The following possible Homebrew files were not deleted:
/usr/local/bin/
/usr/local/Cellar/
/usr/local/etc/
/usr/local/lib/
/usr/local/share/
/usr/local/texlive/
/usr/local/var/
You may consider to remove them by yourself.
You may want to restore /usr/local's original permissions
  sudo chmod 0755 /usr/local
  sudo chgrp wheel /usr/local
```
