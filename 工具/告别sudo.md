# 告别sudo
主要原理是在终端利用sudo的root权限给当前用户赋予用户文件夹下的所有目录权限，从而不用再写sudo

命令如下：
```bash
sudo chown -R username /Users/username
```
或者

```bash
sudo chown -R $(whoami) /Users/(用户文件夹)
```