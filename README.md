# Bash Cookbook

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

### Help Documentation

```bash
<cmd> --help
man|info [section] <cmd>
which [-a] <cmd>
```

### Key Bindings

- `Tab` - Completion
- `Ctrl+D` - `exit` or EOF
- `Crrl+C` - SIGTERM
- `Ctrl+A` / `Ctrl+E` - Go to Beginning / End of Command Line
- `Ctrl+U` / `Ctrl+K` - Cut from Current Position to Beginning / End of Command Line
- `Ctrl+Y` - Paste
- `Ctrl+L` - `clear`
- `Ctrl+R` - History Search, `Ctrl+C` to Quit
- `Ctrl+Z` - SIGSTP

### tar & gzip & bz2

```bash
tar xzvf tar.gz|tgz
tar xjvf tar.bz2

tar czvf tar.gz|tgz <file ...>|<dir>
tar czvf tar.bz2 <file ...>|<dir>
```

### find - Search File

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

### grep - Search File Contents

```bash
grep [opt] <pattern> <file>
  -i, --ignore-case
  -w, --word-regexp
  -x, --line=regexp
  -n, --line-number
  -v, --invert-match
  -f, --file=<pattern-file>
```

### Date & Time

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

### Join Files

*Say we have a large file that has been split into multiple parts, and we want
to join them back together. If the files were named: movie.mp4.001, movie.mp4.002 ... movie.mp4.099*

```bash
cat movie.mp4.0* > movie.mp4
```
