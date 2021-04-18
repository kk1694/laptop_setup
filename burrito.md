# Burrito Setup

## Installed Ubuntu 20.04

I added the option to install new updates, but not 3rd party drivers.

## Configure Firefox

1. Sign in to `start.me`
1. Under Settings/General tick `Restore previous session`
1. Under Settings/Home, put `start.me` as the home page for new windows, and black screen for new tabs.

## Create $HOME/bin

I'll put most user-installed binaries in `$HOME/bin`. Sourcing `.profile` automatically adds these to `$PATH` (see [here](https://askubuntu.com/questions/402353/how-to-add-home-username-bin-to-path)).

```
cd ~
mkdir bin
source .profile
```


## Install git & set up ssh keys

```
sudo apt isntall git
git config --global user.email "krisztiankovacs@fastmail.com"
git config --global user.name "krisztian"
```

Then generate keys and copy to accepted keys in github & gitlab:

```
ssh-keygen
cat .ssh/id_rsa.pub
```

## Customize shell

I'm using the bash-it github repo.

```
git clone --depth=1 https://github.com/Bash-it/bash-it.git ~/.bash_it
~/.bash_it/install.sh
```
Then, modify the .bashrc theme to
```
export BASH_IT_THEME="powerline-plain"
```
(Note: not all themes print out the anaconda environment)

Then `source .bashrc`.

## Download Editors

1. Download [VSCode](https://code.visualstudio.com/) from their website and install it.
1. Download [Atom](https://atom.io/download/deb) and install it.
1. Download [Obsidian](https://obsidian.md/) App image and put it in `$HOME/bin`

## Install custom functions

I like these shortcuts for visualizing git log in a nice way & deleting trailing white space.
```
cat >> .bashrc <<- EOM
git_visualize() {
    git log -n \${1:-20} --all --oneline --graph --decorate
}
export git_visualize
ws_del() {
    sed -i'' -e "s/[[:blank:]]*$//" ${1}
}
export ws_del
EOM
source .bashrc
```

## Install miniconda

[Get the latest version](https://docs.conda.io/en/latest/miniconda.html) and install it.

Then, create `all` environment:

```
conda create -n all
conda activate all
conda install pip
conda install -c conda-forge notebook
echo 'conda activate all' >> .bashrc
```

## Install Useful Tools

```
sudo apt install curl
sudo apt install tmux
```

Add CLI-get from the [firefox extensions](https://addons.mozilla.org/en-GB/firefox/addon/cliget/)