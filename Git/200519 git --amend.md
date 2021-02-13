tags: #git #amend #english

## `--amend`

Let say you committed a file with a wrong message
```bash
$ git add 1000.txt
$ git commit -m "1001 text added"
```

you can do `git commit --amend` to rewrite the most recent commit message
```vim
# you will see your previous commit's message and you can change it
"1000 text added"
```

## Reference
- [git --amend](https://backlog.com/ja/git-tutorial/stepup/28/)