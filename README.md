# laptop_setup

Documenting setup steps for my new laptop (so when I change it, reinstall it, etc.) it will be easy to set up. I'm using an Ubuntu LTS version (18 as of writing this).

## 1. Set up office connection

Obviously not describing this, but set up office vpn + ssh keys to servers.

## 2. Install miniconda

Get the latest version and install it from: https://docs.conda.io/en/latest/miniconda.html

## 3. Install git & set up ssh keys

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

## 4. Customize shell

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

## 5. Install custom functions

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
```

Then `source .bashrc`.

## 6. Create conda environment 

I create an `all` conda environment that contains a dump of python libraries I use. I don't filter it, so I have everything for experimenting. Then, for a particular project, I create a new environmnet with only the dependencies I need.

```
conda create -n all
conda install pip
pip install nbdev
```
etc.

## 7. To be continued when I add new stuff
