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

- Edit latest commit's message
``` 
git commit --amend -m "new commit message"
```

- Remove staged files (for untrack files added later to .gitignore)
```
git rm -r --cached <files>
```