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
  - `decorate` show all the reference
  - `graph` display ascii graph for branch structure
  - `p` patch, show the change of every commit
  - `stat` show the number of change of files
- can send option
  - number to show the last-number, 2 for last 2 commit
  - `after` or `since` for after certain time, after="yesterday", 30 minute ago, last tuesday, last week, 2 week ago, 3-15-16, 3/15/16
  - `before` or `until` for commit before certain time, before="yesterday"
  - `author` author name, author="mohsen" all commit with author and email contain mohsen
  - `grep` search in commit message
  - `S` search for string when add or remove in code, S"mat", better use with p arguman to see where used
  - `G` search with regex for change in code dont need comma,-GMath\|Random -> search for Math or Random
  - `i` ignore case sensitive
  - `no-merges` see without merge commit
  - `..` commit with range of references [ref1]..[ref2]
  - `[file name]` the commit involve that files

```sh
git log --oneline --graph

git log -p -i -S"mat"

git log -3 -i --author="mohsen" README.md

git log -S"Math" --after="2 months ago" --online --stat
```

### diff

- use without argument or name show un-commit change

```sh
git diff
```

- `cashed` show difference between working directory and stashed

```sh
git diff --cashed
```

- can send branch name to see diff

```sh
git diff [branch name]
```

- can send file name

```sh
git diff origin/master README.md
```

### blame

- who modify the file and when

```sh
git blame [file name]
```

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

- its equal to

```sh
git fetch && git merge
```

- send change to remote

```
git push
```

## Branch

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

- delete branch

```sh
git checkout -d [branch name]
```

### rebase

```sh
git rebase [branch name]
```

- use `i` for interactive mode

```sh
git rebase -i [branch name]
```

- combine all commit to one commit -> hold first to pick and change other to squash or only s, after save and exit you can add one commit message for all of that
- after this change must push with `f` or force flag

```sh
git push -f
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

### binary search

- for start

```sh
git bisect
```

- mark this commit as bad commit

```sh
git bisect bad
```

- mark the good commit

```sh
git bisect good [commit id]
```

- git start searching for bad commit, answering them:

```sh
git bisect good
git bisect bad
```

- exit from bisect search

```sh
git bisect reset
```

### tag

- add tag

```sh
git tag v1.0.0
```

- see all tag

```sh
git tag
```

- push tag to remote

```sh
git push --tags
```

- annotate comment for tag with `a`, if not use `m` it open in default editor

```sh
git tag -a v2.0.0 -m "tag message"
```

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

- go to github -> profile -> edit profile -> ssh keys -> add ssh key -> title: like the name of the computer or machine, past the key
- verify the key

```sh
ssh -T git@github.com
```

### git hook

- in `.git/hooks` folder, there is some sample files, for run you must make file with out sample
- for example in file `.git/hooks/pre-commit`, run test and lint before test

```sh
#!/bin/bash
npm test && npm run lint
```

- after that make file executable

```sh
chmod +x .git/hooks/pre-commit
```

- if one of them failed, we can not commit
- this setting just use locally and cant send to remote repository

### Global Setting

- save in `.gitconfig` file in home directory

```sh
git config --global user.name 'mohsen shabanian'
```

- config default editor

```sh
git config --global core.editor vim
```

- add alias

```sh
git config --global alias.graph 'log --graph --oneline'
```

-- see all config list

```sh
git config list
```

### ignore file

- make `.gitignore` file and file name like `.DS_Store` for mac or `Thumbs.db` for windows
- for remove tracked file that ignore but added before:

```sh
git rm --cached
```

- we can make `.gitignore_global` in home directory for ignore file in all the place and define it in `.gitconfig`

```sh
git config --global core.excludesfile ~/.gitignore_global
```

## Reference

- Egghead: practical-git-for-everyday-professional-use
