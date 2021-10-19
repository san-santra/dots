# Backup of dot files

## GRUB theme
https://github.com/lfelipe1501/Atomic-GRUB2-Theme

## Restoring 
```
git clone --bare https://github.com/san-santra/dots.git $HOME/.cfg
function config {
   /usr/bin/git --git-dir=$HOME/.cfg/ --work-tree=$HOME $@
}
mkdir -p .config-backup
config checkout
if [ $? = 0 ]; then
  echo "Checked out config.";
  else
    echo "Backing up pre-existing dot files.";
    config checkout 2>&1 | egrep "\s+\." | awk {'print $1'} | xargs -I{} mv {} .config-backup/{}
fi;
config checkout
config config status.showUntrackedFiles no
```
Or using the alias
```
alias config='/usr/bin/git --git-dir=$HOME/.cfg/ --work-tree=$HOME'
```

## Reference
1. https://www.atlassian.com/git/tutorials/dotfiles
