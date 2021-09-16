# Shell

## Prompt
+ csh/tcsh
```Shell
set prompt="%Y%W%D %P %n@%m:%/\n> "
```
+ bash
```Shell
export PS1='\[\033[1;31m\]$(date +%Y.%m.%d) \t\[\033[00m\] | \[\033[32;40m\]\u@\h:$(pwd)\[\033[00m\]\n$ '

export PS1='\[\033[1;38;5;196;48;5;234m\]\D{%Y.%m.%d} \t\[\033[0m\] | \[\033[1;38;5;28;48;5;234m\]\u@\h:$(pwd)\[\033[0m\]\n$ '
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

## Script
+ example in /usr/share/doc/util-linux
```bash
#!/bin/bash

# A small example script for using the getopt(1) program.
# This script will only work with bash(1).
# A similar script using the tcsh(1) language can be found
# as getopt-parse.tcsh.

# Example input and output (from the bash prompt):
#
# ./getopt-parse.bash -a par1 'another arg' --c-long 'wow!*\?' -cmore -b " very long "
# Option a
# Option c, no argument
# Option c, argument 'more'
# Option b, argument ' very long '
# Remaining arguments:
# --> 'par1'
# --> 'another arg'
# --> 'wow!*\?'

# Note that we use "$@" to let each command-line parameter expand to a
# separate word. The quotes around "$@" are essential!
# We need TEMP as the 'eval set --' would nuke the return value of getopt.

USAGE=$(cat <<EOF
usage: ${0##*/} [-h|--help] [-f <file>]

    find out denied namespace on \`filter from /var/log/messages

    -f <file>
                to specify a file containg LFNs

    -h|--help
                to show this help

EOF
)

TEMP=$(getopt -o 'ahb:c::' --long 'a-long,help,b-long:,c-long::' -n 'example.bash' -- "$@")

if [ $? -ne 0 ]; then
    echo "$USAGE"
        exit 1
fi


# Note the quotes around "$TEMP": they are essential!
eval set -- "$TEMP"
unset TEMP

while true; do
        case "$1" in
        '-h'|'--help')
            echo "$USAGE"
            exit 0
        ;;
                '-a'|'--a-long')
                        echo 'Option a'
                        shift
                        continue
                ;;
                '-b'|'--b-long')
                        echo "Option b, argument '$2'"
                        shift 2
                        continue
                ;;
                '-c'|'--c-long')
                        # c has an optional argument. As we are in quoted mode,
                        # an empty parameter will be generated if its optional
                        # argument is not found.
                        case "$2" in
                                '')
                                        echo 'Option c, no argument'
                                ;;
                                *)
                                        echo "Option c, argument '$2'"
                                ;;
                        esac
                        shift 2
                        continue
                ;;
                '--')
                        shift
                        break
                ;;
                *)
                        echo 'Internal error!' >&2
                        exit 1
                ;;
        esac
done

echo 'Remaining arguments:'
for arg; do
        echo "--> '$arg'"
done
```
