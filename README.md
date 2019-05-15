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
* 注意上面的FILE_PATH要是**路径**而不只是文件名字，例如src/main/java/com/ysy/demo/filename.java
---

## 2、pytorch加载模型时错误：Unexpected key(s) in state_dict
* 创建一个没有module前缀的新的有序字典，然后加载它model.load_state_dict({k.replace('module.',''):v for k,v in torch.load(checkpoint_path)['state_dict'].items()})，对我无效；
* [链接](https://discuss.pytorch.org/t/missing-keys-unexpected-keys-in-state-dict-when-loading-self-trained-model/22379/5)加了个参数strict ，model.load_state_dict(torch.load(PATH), strict=False)，解决
