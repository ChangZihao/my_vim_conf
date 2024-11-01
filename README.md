# Setup NEOVIM and tmux quickly

Now I migrate to neovim for asynchronous support (although it is support in vim now) and extensibility:
- When writing Python with vim, `np.` often stucks for a few seconds, especially on a server with HDD.
- It is similar for other heavy extensions like YCM.

## old readme for VIM
[old readme here](old_README.md)

## Install neovim

Go to [latest stable release](https://github.com/neovim/neovim/releases/latest),
download `nvim.appimage` with browser, wget, or anything you like.
``` shell
# Linux:
chmod u+x nvim.appimage
mkdir ~/.local/bin
mv nvim.appimage ~/.local/bin  # assume that ~/.local/bin is in $PATH
```

Let $vimConf be where you store this repository, and git clone this repo to
$vimConf.
``` shell
git clone https://github.com/shinezyy/my_vim_conf.git $vimConf
```

Link config file to
``` shell
mkdir -p ~/.config/nvim  # create config dir for neovim
cd ~/.config/nvim
ln -s $vimConf/neovim/neovimrc ./init.vim

cd ~
mv ~/.vim ~/.vim_bak
ln -s $vimConf/vim .vim
```

Install vimPlug:
``` shell
sh -c 'curl -fLo "${XDG_DATA_HOME:-$HOME/.local/share}"/nvim/site/autoload/plug.vim --create-dirs \
       https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim'
```

Install pynvim to enable jedi and YCM:
``` shell
sudo apt install python3-pip
python3 -m pip install --user --upgrade pynvim
```


If you do not need YCM (C++ support),
Then comment out the following line in ~/.config/nvim/init.vim
```
Plug 'davidhalter/jedi-vim'
```

Open `nvim`, and input command `:PlugInstall`, it will git clone jedi and YCM for you.

If you need YCM (C++ support), you should further install YCM with clang support
``` shell
cd $vimConf/vim/bundle/YouCompleteMe
sudo apt install cmake
./install.py --clang-completer --verbose
```

# Tmux

If you use tmux and use Ctrl+A for instruction escape.

```
cd $vimConf
git submodule update --init tmux
cd ~
mv ~/.tmux.conf ~/.tmux.conf_bak
ln -s $vimConf/tmux/.tmux.conf .
```

# Zsh
Install zsh
```
sudo apt update
sudo apt install zsh
```

Install on-my-zsh
```
sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
```

Install pluging
```
cd ~/.oh-my-zsh/custom/plugins/
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git
git clone https://github.com/zsh-users/zsh-autosuggestions
```

Link config file
```
cd ~
mv .zshrc .zshrc_bak
ln -s $vimConf/zsh/zshrc ./.zshrc
```

# git
```
cd ~
mv .gitconfig .gitconfig_back
ln -s $vimConf/git/gitconfig ./.gitconfig
```

# SSH Public Keys

```
git submodule update --init ssh_pub_key
mv .ssh/authorized_keys .ssh/authorized_keys_bak
ln -s $vimConf/ssh_pub_key/authorized_keys ./.ssh/authorized_keys
```
