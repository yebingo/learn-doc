# 如何优雅的在git中回滚？
> master已经提交到远程，需要回滚到某次commit，直接reset后推不上去，又没有 push -f 的权限怎么办？来来，看这里

```bash
git reset xxx --hard

git reset origin/master --soft

git commit -am '回滚'

git push
```
会将回滚的变动作为一次commit提交，比其push -f git的主线看起来会很好看。