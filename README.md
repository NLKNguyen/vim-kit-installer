Vim Kit Installer
=============

TL;DR
> **Vim Kit Installer** is a simple package manager that simply backups and restores your *.vimrc* file and *.vim/* directory, and it can work offline.

**How?**
> To backup your .vimrc AND .vim/ directory into a package
> ```bash 
> ./install.sh --save MyAwesomeVimSettings
> ```
> To restore
> ```bash
> ./install.sh --load MyAwesomeVimSettings
> ```

**Why?**

1. When a single .vimrc won't cut it anymore and you know why

2. To keep track with multiple backups

3. You don't want to backup/restore manually every time

4. When the place to restore your settings doesn't have Internet connection thus can't simply run :PluginInstall or something like that. Yes you can do it manually, but [go back to 2]

5. To easily share your settings to even the most novice Vim users. To do that, simply fork this repository and save your package into it, then let them install from your repository.



#Installation
*System requirement*: Unix/Linux environment (eg: Solaris, Ubuntu, Mac OS X, Cygwin)

**Option 1**: use Git
```git
git clone https://github.com/NLKNguyen/vim-kit-installer.git
  ```    
**Option 2**: manually download the repository to your local and extract it
#Usage

```bash
cd vim-kit-installer
./install.sh [command] [optional argument]
```

The `[command]` can be one of the following:

**`--save <package name>`** saves/backups your *~/.vimrc*  and *~/.vim/* to a package named  `<package name>`

**`--load <package name>`** loads/restores your *~/.vimrc*  and *~/.vim/* from the package named  `<package name>`

**`--list`** lists all packages in the `pkgs/` of this program directory

**`--remove <package name>`** removes  the package named `<package name>`

**`--clean`** deletes the current *~/.vimrc* and *~/.vim/*

**`--help`** shows usage information

**`-s`** Some system requires root permission to operate some of these operations. Placing this optional flag at the end to use `sudo` on certain tasks like --load --clean --remove <br>
eg: `./install --load <package name> -s`

#Side Effect and Solution
Since the `--save` command put **~/.vim/** and **.vimrc** in a Tarball file, if you Git to store your settings, the size of the repository will go up quickly because Git cannot store multiple versions of a Tarball file as efficient as editable text files.

The solution is simple. Use BFG Repo-Cleaner tool to clean up old versions of your packages in your Git repository.

First, download the BFG jar file https://rtyley.github.io/bfg-repo-cleaner/

Then, for your convenience, in your **~/.bashrc** set an alias for `bfg` command
```Bash
alias bfg='java -jar [path to BFG .jar file]
```

In your Git repository, run this command to delete all old versions of package files. Don't worry, it will not affect the current package files in your repository.
```
bfg --delete-files *.tar.gz
```

Finally, run this command to physically remove the unwanted files
```
git reflog expire --expire=now --all && git gc --prune=now --aggressive
```

To update the remote repository, simply run `git push -f`

----------

Suggestions and contributions are welcome.

For troubleshooting, go to  [issues section]( https://github.com/NLKNguyen/vim-kit-installer/issues)


> Author: [Nguyen Nguyen](https://github.com/NLKNguyen)
