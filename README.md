# Bash Cookbook

<section align="center">
  <img src="https://lucas-six.github.io/bash-cookbook/imgs/Bash-noalpha.png"
    alt="Bash Logo" width="384" height="161" style="text-align:center;" title="Bash Logo">
  <br><br>
  <p>
    <a href="https://github.com/lucas-six/bash-cookbook/actions/workflows/lint.yml">
      <img src="https://github.com/lucas-six/bash-cookbook/actions/workflows/lint.yml/badge.svg"
      alt="GitHub Actions - lint" style="max-width:100%;">
    </a>
  </p>
  <p>Recipes for <code>Bash</code> (Bourne Again shell).</p>
  <p>Hands-on Bash examples and guides for daily work.</p>
  <p><a href="https://lucas-six.github.io/bash-cookbook/">https://lucas-six.github.io/bash-cookbook/</a></p>
</section>

<!-- markdownlint-disable line-length -->

## Installation and Update

### Linux

Bash is the default shell for *Linux*.

#### Ubuntu, Debian

```bash
apt install bash bash-completion
```

#### Red Hat (RHEL, CentOS, Fedora)

```bash
dnf install -y bash bash-completion
```

or

```bash
yum install -y bash bash-completion
```

### macOS

#### Homebrew

```bash
brew install bash bash-completion@2
chsh -s /usr/local/bin/bash
```

## Builitin

### Basic

```bash
cd [~|-|..|<dir>]
pwd  # $PWD
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

### `type`

```bash
$ type type
type is a shell builtin

$ type cp
cp is /usr/bin/cp

$ type ls
ls is aliased to 'ls --color=auto'
```

## Help

```bash
help <builtin-cmd>

<cmd> --help
man|info [section] <cmd>
which [-a] <cmd>
```

## Key Bindings

- `Tab` - Command Completion
- `Ctrl+D` - `exit` or **EOF**
- `Ctrl+C` - **SIGTERM**
- `Ctrl+A` / `Ctrl+E` - Go to Beginning / End of Command Line
- `Ctrl+U` / `Ctrl+K` - Cut from Current Position to Beginning / End of Command Line
- `Ctrl+Left` / `Ctrl+Right` - Go to Previous / Next Word
- `Ctrl+Y` - Paste
- `Ctrl+L` - `clear`
- `Ctrl+R` - History Search, `Ctrl+C` to Quit
- `Ctrl+Z` - **SIGSTP**
- `Ctrl+-` - Undo

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

## Input / Output

### Input

#### From stdin

```bash
DEFAULT="default"
read -t 5 -p "Prompt [$DEFAULT]: " VAR
if [[ $? != 0 ]]; then
    echo "xxx"
fi
VAR=${VAR:-$DEFAULT}
```

#### From File

```bash
cat > /etc/pip.conf <<EOF
[global]
index-url = https://pypi.douban.com/simple

[list]
format = columns
EOF
```

### Output Redirection

#### Redirect stderr

```bash
ls -l /bin/usr 2> ls-error.log
```

#### Redirect stdout and stderr

```bash
ls -l /bin/usr &> ls.log  # Bash 4.0+
ls -l /bin/usr > ls.log 2>&1
```

### Redirect stdout and stderr

```bash
ls -l /bin/usr &> ls.log  # Bash 4.0+
ls -l /bin/usr > ls.log 2>&1
```

#### Sometimes "silence is golden"

```bash
ls -l /bin/usr > /dev/null 2>ls.log
```

## Expansion

- **pathname expansion**: `*.txt`
- **tilde expansion**: `~`
- **brace expansion**: `{a,b}`, `{A..C}`
- **command substitution**: `$(echo a)`
- **arithmetic expansion**: `$((1+1))`
- **parameter expansion**: `$USER`

```bash
$ echo text ~/*.txt {a,b} {A..C} $(echo a) $((1+1)) $USER
text /home/ly/a.txt a b A B C a 2 ly

$ echo "text ~/*.txt {a,b} {A..C} $(echo a) $((1+1)) $USER"
text ~/*.txt {a,b} {A..C} a 2 ly

$ echo 'text ~/*.txt {a,b} {A..C} $(echo a) $((1+1)) $USER'
text ~/*.txt {a,b} {A..C} $(echo a) $((1+1)) $USER
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

## Startup Files

### Login Shell Sessions

- **`~/.bash_profile`**
- *`~/.bash_login`*
- *`~/.profile`*
- **`/etc/profile`**
- *`/etc/profile.d/*.sh`*

### Non-Login Shell Sessions

- **`~/.bashrc`**
- *`/etc/bash.bashrc`*

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

## Loop Over Array

```bash
a=(1 2)
for i in ${a[*]}; do
    echo $i
done
```

## References

- [The Bash Reference Manual](https://www.gnu.org/savannah-checkouts/gnu/bash/manual/bash.html)
