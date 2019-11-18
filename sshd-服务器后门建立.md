公钥文件 `id_rsa.pub` 的***打开方式***很重要
---
使用 `more` 在终端中打开,然后复制到使用 `vim` 打开的终端中, 结果一直提示需要密码, 差点让所有的工作功亏一篑.
正确的做法是---
  1. 使用 `vim` 打开 `id_rsa.pub` 文件, 然后复制到剪切板, 然后使用 `vim` 打开目标计算机的 `/root/.ssh/authorized_keys` 文件, 粘贴公钥.

修改目标计算机的 `sshd` 配置文件 `/etc/ssh/sshd_config`, 将 `PermitRootLogin ProhibitLogin` 项目注销掉, *手动*添加上一条: `PermitRootLogin yes`.

重新启动 `sshd` 服务: `service sshd restart`. Note: 重启的是 `sshd`, 而不是 `ssh`.










