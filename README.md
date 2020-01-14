# dotfiles
Dotfiles meant to be used in Z shell with oh-my-zsh and powerlevel9k theme.
```
brew install zsh
brew install tmux
brew cask install iterm2
```

Create new ssh in github settings
```
cat ~/.ssh/id_rsa.pub
```

Go to your github gist via profile and create there dotfiles-install.sh
```
git clone --bare git@github.com:matusr/dotfiles.git $HOME/.dotfiles
function dotcfg {
   /usr/bin/git --git-dir=$HOME/.dotfiles/ --work-tree=$HOME $@
}
mkdir -p $HOME/.config-backup
dotcfg checkout
if [ $? = 0 ]; then
  echo "Checked out config.";
  else
    echo "Backing up pre-existing dot files.";
    dotcfg checkout 2>&1 | egrep "\s+\." | awk {'print $1'} | xargs -I{} mv {} $HOME/.config-backup/{}
fi;
dotcfg checkout
dotcfg config status.showUntrackedFiles no
# For oh-my-zsh and powerlevel9k
dotcfg submodule init
dotcfg submodule update
chsh -s $(which zsh)
```

Commit changes to dotfiles using gist (if any in the future)
```
dotcfg status
dotcfg add .zshrc
dotcfg commit
i
commit message
esc :wq
dotcfg push --set-upstream origin master
source .zshrc
```

As a font for your terminal emulator I advise to install, set and use patched 'Hack Regular Nerd Font Complete.ttf'
from https://github.com/ryanoasis/nerd-fonts/tree/master/patched-fonts/Hack/Regular/complete. Just download and install from the file.

For the installation of your dotfiles you can use the following in your home directory so that when you want to pull or push the latest changes (it will export to .zshrc). Put off proxy.
```
curl https://gist.githubusercontent.com/matusr/dc2a704b0595eb92a9c7b855108fb69e/raw/87271cc2d338084ae0aa6666014912a74bc28cb7/dotfiles-install.sh | /bin/bash
```
iTerm2
```
Preferences- Profiles - + - nerd
	- general - reuse previous session's directory 
	- text - font - hack nerd font
	- make nerd default profile
```

tmux
```
#enter tmux
crtl + s 
alt + copy text
#split screen
shift + \  
shift + -
#switch screen
ctrl + arrow or mouse
#end split screen
crtl + d
esc 
```
Machine specific settings put into .oh-my-zsh-custom!!!

This repository was created by following a great article https://www.atlassian.com/git/tutorials/dotfiles,
for interaction with the local repository you must use, instead of 'git', alias called 'dotcfg' (take 
a look into .zshrc).
