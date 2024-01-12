# LF will be replaced by CRLF the next time Git touches it

在 `windows` 系统上, 提交时会进行 `CRLF->LF` 的转换, 检出时会进行 `LF->CRLF` 的转换, 可使用如下命令更改这一行为:

```bash
# 在 windows 系统上默认为 true
git config --global core.autocrlf false
```

`safecrlf` 检查:

```bash
git config --global core.safecrlf true

git config --global core.safecrlf false

git config --global core.safecrlf warn
```