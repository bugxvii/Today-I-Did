tags: #git

This command will revert you commit back to one BUT also deletes all newly made content.
```bash
$ git reset --hard HEAD~1
```

To retain your changes but just cancel the local commit, you can use 
```bash
$ git reset HEAD~1
```
