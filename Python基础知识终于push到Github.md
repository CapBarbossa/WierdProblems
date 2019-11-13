工作目录 `Python基础知识` 经过好多次总不能够push到Github, 原因在于这个目录内, 存在好多子 `git` 目录, 导致在最外面执行 `git push`的时候, 有一些文件不能正确上传. 一直困扰了我好久.

Solution:
  ```shell
  # 找到所有的 .git目录
  find . -type d -name .git -print
  # 删除
  rm -rf .git
  # 重新建立git目录
  git init
  git add .
  git ci -m "哈哈,好了"
  git remote add origin https://github.com/123.git
  git push -u origin master
  
  



