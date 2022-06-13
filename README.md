Please move to [Dookbook](https://github.com/dookbook).

此项目已经停止更新，已并入组织 Dookbook (<https://github.com/dookbook>)

Dookbook (<https://dookbook.info/>)，是软件开发的日常菜谱，开箱即用，提供常用的代码示例。

# Bash Cookbook

`bash` **4+** is recommended.

`Linux` or `Mac OS X` is recommended.

For `Windows`, please ...

For Mac users, [install `MacPorts`](https://www.macports.org/install.php) first in `Terminal`.

Then run:

```bash
sudo port install bash bash-completion coreutils vim lbzip2 gcc make colordiff openssl curl python27

sudo port select --set python python27
sudo port select --set python2 python27
```

For Linux users, Do it yourself!

For Windows users, install a virtual machine [VirtualBox](https://www.virtualbox.org/) with `CentOS` 7.4+.
Or connect to a remote Linux host by [Putty](http://www.putty.org/) and [WinSCP](http://winscp.net/).

---

- Basic Commands
- Help Documentation
- Key Bindings
- tar & gzip & bz2
- find
- grep
- Date & Time
- Join Files
- Output
- Environment Variables
- I/O Redirection
- Expansion
- Testing Options
- Text Processing
- Regular Expression
- Input From stdin
- Input From File
- Loop Over Array

## Basic Commands

```bash
cd [~|-|..|<dir>]
pwd
ls [-l|-a|-r|-h|-R]
less <file>
ln -s[f] <src> <symlink>
cp|mv [-r|-u] <src ...> <dst>
rm [-r|-f] <file ...>|<dir>
mkdir [-p] [-m <mode>] <dir>
rmdir [-p] <empty-dir>
wc -l <file>
head|tail -n <num> <file>
tail -f <file>
cut -d -f
```

## Help Documentation

```bash
<cmd> --help
man|info [section] <cmd>
which [-a] <cmd>
```

## Key Bindings

- `Tab` - Completion
- `Ctrl+D` - `exit` or EOF
- `Ctrl+C` - SIGTERM
- `Ctrl+A` / `Ctrl+E` - Go to Beginning / End of Command Line
- `Ctrl+U` / `Ctrl+K` - Cut from Current Position to Beginning / End of Command Line
- `Ctrl+Left` / `Ctrl+Right` - Go to Previous / Next Word
- `Ctrl+Y` - Paste
- `Ctrl+L` - `clear`
- `Ctrl+R` - History Search, `Ctrl+C` to Quit
- `Ctrl+Z` - SIGSTP
- `Ctrl+-` - Undo

## tar & gzip & bzip2

```bash
tar xzvf tar.gz|tgz
tar xjvf tar.bz2

tar czvf tar.gz|tgz <file ...>|<dir>
tar cjvf tar.bz2 <file ...>|<dir>
```

## find - Search File

```bash
find <dir> <text-expr> [<logic-opertor ...>] <act>
    -name <file-pattern>
    -type f|d|l|b|c
    -size <N>c|k|M|G
    -empty
    -usr <user-name>
    -uid <uid>
    -cmin [-|+]<N-min>
    -ctime [-|+]<N-day>
    -inum <inode>

    -and
    -or
    -not
    ()

    -print
    -printf <fmt>
    -fprintf <file> <fmt>
    -delete
    -ls
    -exec <cmd> '{}' ';'|+
```

## grep - Search File Contents

```bash
grep [opt] <pattern> <file>
  -i, --ignore-case
  -w, --word-regexp
  -x, --line=regexp
  -n, --line-number
  -v, --invert-match
  -f, --file=<pattern-file>
```

## Date & Time

```bash
date <+format>
    %% - '%'
    %H - hour (00-23)
    %I - hour (01-12)
    %M - minute (00-59)
    %S - second (00-59)
    %T - %H:%M:%S
    %R - %H:%M
    %y - year (00-99)
    %Y - year (0000-9999)
    %m - month (01-12)
    %d - day of month (01-31)
    %D - %m/%d/%y
    %u - day of week (1-7, 1=Monday)
    %w - day of week (0-6, 0=Sunday)
    %n - newline ('\n')
    %t - tab ('\t')
```

## Join Files

*Say we have a large file that has been split into multiple parts, and we want
to join them back together. If the files were named: movie.mp4.001, movie.mp4.002 ... movie.mp4.099*

```bash
cat movie.mp4.0* > movie.mp4
```

## Output

```bash
echo [-n|-e] <str>
```

## Environment Variables

```bash
echo $PWD   # current directory
echo $USER  # current user name
echo $HOME  # home directory of current user
```

## I/O Redirection

### Redirect stderr

```bash
ls -l /bin/usr 2> ls-error.log
```

### Redirect stdout and stderr

```bash
ls -l /bin/usr &> ls.log  # Bash 4.0+
ls -l /bin/usr > ls.log 2>&1
```

### Sometimes "silence is golden"

```bash
ls -l /bin/usr > /dev/null 2>ls.log
```

## Expansion

```bash
$ echo text ~/*.txt {a,b} {A..C} $(echo a) $((1+1)) $USER
text /home/ly/a.txt a b A B C a 2 ly

$ echo "text ~/*.txt {a,b} {A..C} $(echo a) $((1+1)) $USER"
text ~/*.txt {a,b} {A..C} a 2 ly

$ echo 'text ~/*.txt {a,b} {A..C} $(echo a) $((1+1)) $USER'
text ~/*.txt {a,b} {A..C} $(echo a) $((1+1)) $USER
```

## Testing Options

```bash
if [[ <-opt> xxx ]]; then
    ...
fi
```

Used frequently:

```bash
-e exist
-s NOT empty
-f regular file
-d directory
-S socket
-p named pipe
-h symbolic link
-r readable
-w writable
-nt newer than
-ot older than
-ef hard link
```

## Text Processing

### Subtitute

```bash
str="a-b-c"
echo ${str/-/_}_d   # a_b-c_d
echo ${str//-/_}_d  # a_b_c_d
```

### Substring

```bash
str="abcdef"
echo ${str:1}       # a
echo ${str:2:2}     # bc
```

### Testing Operator

```bash
-z empty
-n NOT empty
```

## Regular Expression

- `*` - Any numbers of characters
- `?` - Any single character
- `[abc]` - Any character in set of `abc`
- `[!abc]` - Any character NOT in set of `abc`
- `[:alpha:]` - Any letter
- `[:lower:]` - Any lower-case letter
- `[:upper:]` - Any upper-case letter
- `[:digit:]` - Any digit
- `[:alnum:]` - `[[:alpha:][:digit:]]`
- `[:word:]` - `[[:alnum:]_]*`
- `[:blank:]` - `Space` + `Tab`
- `^abc` - Any line started with `abc`
- `abc$` - Any line ended with `abc`
- `+` - More than once
- `{n}`, `{n,m}` - From (n) to (m) times

## Input From stdin

```bash
DEFAULT="default"
read -t 5 -p "Prompt [$DEFAULT]: " VAR
if [[ $? != 0 ]]; then
    echo "xxx"
fi
VAR=${VAR:-$DEFAULT}
```

## Input From File

```bash
cat > /etc/pip.conf <<EOF
[global]
index-url = https://pypi.douban.com/simple

[list]
format = columns
EOF
```

## Loop Over Array

```bash
a=(1 2)
for i in ${a[*]}; do
    echo $i
done
```
