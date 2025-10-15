# Git
- Undo an un-pushed commit + unstage
```
git reset HEAD~
```

- Undo an un-pushed commit + unstage + remove all changes in the working space
```
git reset --hard HEAD~
```

- Add + commit in one line, only tracked files are done
```
git commit -am "commit message"
```