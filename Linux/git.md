# Git

## local command

### Add

- add file

```sh
git add [file name]
```

- add all

```sh
git add -A
```

- or add all file in this folder

```sh
git add .
```

### Commit

- save addlist to history

```sh
git commit -m"[descriptive message]"
```

### Log

- see the history of commits

```sh
git log
```

- its less command in linux
  - `q` ->quite
  - `/[search]` and enter, n to next, N to Previous

### Status

- current status

```sh
git status
```

- can send argument, can send two or more
  - `oneline` for see every commit in one line
  - `decorate` show all the refrence
  - `graph` display aski graph for branch structure
  - `p` patch, show the change of every commit
  - `stat` show the number of change of files
- can send option
  - number to show the lastnumber, 2 for last 2 commit
  - `after` or `since` for after certain time, after="yesterday", 30 minute ago, last tuesday, last week, 2 week ago, 3-15-16, 3/15/16
  - `before` or `until` for commit before certain time, before="yesterday"
  - `author` author name, author="mohsen" all commit with author and email contain mohsen
  - `grep` search in commit message
  - `S` search for string when add or remove in code, S"mat", better use with p arguman to see where used
  - `G` serch with regex for change in code dont need comma,-GMath\|Random -> search for Math or Random
  - `i` ignore case sensitive
  - `no-merges` see whitout merge commit
  - `..` commit with range of refrenses [ref1]..[ref2]
  - `[file name]` the commit involve that files

```sh
git log --oneline --graph

git log -p -i -S"mat"

git log -3 -i --author="mohsen" README.md

git log -S"Math" --after="2 months ago" --oneline --stat
```

### diff

### reset current change

```sh
git reset --hard [name]
```

### stash

- save temporary the change added to history and clean the status

```sh
git stash
```

- unstash or come back the stash change

```sh
git stash apply
```

## remote access

### clone

```sh
git clone http://github.com/mohsen12999/mycheat
```

### add remote

```sh
git remote add origin git@github.com:fhfh/fgfg.git
```

### see remotes

```sh
git remote -v
```

### pull, push

- get the history from remote

```sh
git pull
```

- its equel to

```sh
git fetch && git merge
```

- send change to remote

```
git push
```

## Branche

- add branch

```
git branch [new branch name]
```

- see all branch

```
git branch
```

- go to branch

```sh
git checkout [branch name]
```

- make and go to new branch

```sh
git checkout -b [new branch name]
```

- go to Previous branch

```sh
git checkout -
```

- merge branch to this branch [add feature of other branch to this branch]

```sh
git merge [branch name]
```

- delete banch

```sh
git checkout -d [branch name]
```

### conflict

```
< < < HEAD
our change
= = =
change come from server
> > >
```

## other

### save password

```sh
git config credential.helper store
```

### config ssh

- generate key

```sh
ssh-keygen -t rsa -b 4096 -C sample@mail.com
```

- add to ssh program

```sh
ssh-agent -s
```

- add rsa to ssh

```sh
ssh-add ~/.ssh/id_rsa
```

- copy rsa key to clip board

```sh
clip <~/.ssh/id_rsa
```

- go to github -> profile -> edit profile -> ssh keys -> add ssh key -> title: like the name of the computer or machin, past the key
- verify the key

```sh
ssh -T git@github.com
```
