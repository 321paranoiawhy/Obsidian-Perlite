#grep
- [GNU Grep](https://www.gnu.org/software/grep/grep.html)
- [Grep Manual](https://www.gnu.org/software/grep/manual/)
- [Grep Download](https://gnuwin32.sourceforge.net/packages/grep.htm)
- [windows 下 grep 的安装与使用](https://www.cnblogs.com/shenxiaolin/p/16662793.html)

添加环境变量 `D:\GnuWin32\bin` 到 系统变量的 `Path` 中。

验证是否安装成功:

```bash
grep
```

> [!info] grep
> Usage: D:\GnuWin32\bin\grep.exe [OPTION]... PATTERN [FILE]...
> Try `D:\GnuWin32\bin\grep.exe --help' for more information.


```bash
kubectl describe node |grep -E '((Name|Roles):\s{6,})|(\s+(memory|cpu)\s+[0-9]+\w{0,2}.+%\))'
```