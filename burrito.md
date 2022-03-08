# Burrito Setup

## Installed Ubuntu 20.04

I added the option to install new updates, but not 3rd party drivers.

## Configure Firefox

1. Sign in to `start.me`. Add start.me addon.
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

## Install CUDA

Install gcc:    

```
sudo apt install gcc
``` 

Follow the steps on the [Nvidia](https://developer.nvidia.com/cuda-downloads?target_os=Linux&target_arch=x86_64&=Ubuntu&target_version=20.04&target_type=deb_network) website.

Also install CUDA toolkit (for `nvcc`):
```
sudo apt install nvidia-cuda-toolkit
```

Next, you have to restart your computer.

Check `nvidia-smi` and `nvcc --version` to see if everything is installed.

Note: you might need to update your PATH variable if things don't work.

```
export PATH=/usr/local/cuda-11.3/bin${PATH:+:${PATH}}
```

## Download Editors

1. Download [VSCode](https://code.visualstudio.com/) from their website and install it.
1. Download [Atom](https://atom.io/download/deb) and install it.
1. Download [Obsidian](https://obsidian.md/) App image and put it in `$HOME/bin`
    - Rename the file to `obsidian` and add execute permissions


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

## Install miniconda

[Get the latest version](https://docs.conda.io/en/latest/miniconda.html) and install it.

Then, create `all` environment:

```
conda create -n all
conda activate all
conda install pip
conda install -c conda-forge notebook   
```
## Install docker

Follow steps on [docker website](https://docs.docker.com/engine/install/ubuntu/).

Don't forget the post-install setup (so that docker can be run without sudo):

```
sudo groupadd docker
sudo usermod -aG docker $USER
```

Log out and back in, and test
```
docker run hello-world
```

Also, install `docker-compose` from [the docker website](https://docs.docker.com/compose/install/).

Check with

```
docker-compose --version
```

## Install Useful Tools

```
sudo apt install curl
sudo apt install tmux
sudo apt install python3-virtualenv
```

Install postgres: https://www.postgresql.org/download/linux/ubuntu/

Install pgadmin4: https://www.pgadmin.org/download/pgadmin-4-apt/

(note: I needed to create a symlink with `ln -s /usr/pgadmin4/bin/pgadmin4 ~/bin/pgadmin4`)

Install slack: https://slack.com/intl/en-gb/downloads/instructions/ubuntu

Add CLI-get from the [firefox extensions](https://addons.mozilla.org/en-GB/firefox/addon/cliget/)

## Set up Noki repos

This is needed for `pip install psycopg2`:
```
sudo apt install libpq-dev python3-dev
```

Install node: https://github.com/nodesource/distributions/blob/master/README.md#tests

```
git clone git@gitlab.com:nokiapp/zoombot.git
git clone git@gitlab.com:nokiapp/noki.git
```

## Install custom functions

I like these shortcuts for visualizing git log in a nice way & deleting trailing white space.
```
cat >> .bashrc <<- EOM
gv() {
    git log -n \${1:-20} --all --oneline --graph --decorate
}
export gv
ws_del() {
    sed -i'' -e "s/[[:blank:]]*$//" ${1}
}
export ws_del
EOM
source .bashrc
```

