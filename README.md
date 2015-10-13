# GIT
## Remove branches no longer on remote
```git gc --prune=now``` do the trick
```git fetch -p```

## Chaching GIT credential for https access
```git config --global credential.helper osxkeychain```
or for linux
```git config --global credential.helper "cache --timeout=3600"```

http://stackoverflow.com/questions/5343068/is-there-a-way-to-skip-password-typing-when-using-https-github
