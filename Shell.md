# Shell

## Prompt
+ csh/tcsh
```Shell
set prompt="%Y%W%D %P %n@%m:%/\n> "
```
+ bash
```Shell
export PS1='\[\033[1;31m\]$(date +%Y.%m.%d) \t\[\033[00m\] | \[\033[32;40m\]\u@\h:$(pwd)\[\033[00m\]\n$ '
```

## Navigating the File System
Your home directory (~) is your initial location when you log in.
+ cd
```Shell
> cd ~                                 # move to your home directory
> cd                                   # move to your home directory
> cd ..                                # move to parent of current directory
> cd ~name                             # move to the home directory of user name
> cd -                                 # return to the previous directory
```
+ pushd/popd
```Shell
> pushd /
/ ~
> pushd /usr
/usr / ~
> pushd /usr/bin
/usr/bin /usr / ~
> pushd +3
~ /usr/bin /usr /

```
