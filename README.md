# tips
## 1、误传服务器密码，彻底清除文件的历史
[转载](https://blog.csdn.net/ysy950803/article/details/53383582)
```
git filter-branch --force --index-filter 'git rm --cached --ignore-unmatch FILE_PATH' --prune-empty --tag-name-filter cat -- --all

git push origin master --force

rm -rf .git/refs/original/

git reflog expire --expire=now --all

git gc --prune=now

git gc --aggressive --prune=now
```
*  注意上面的FILE_PATH要是**路径**而不只是文件名字，例如src/main/java/com/ysy/demo/filename.java）

---
