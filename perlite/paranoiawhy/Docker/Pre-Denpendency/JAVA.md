#Java
# `JDK 8`

[JDK 8 windows](https://www.oracle.com/java/technologies/downloads/#java8-windows)
[超详细！JDK 8 下载、安装和环境配置（macOS 和 Windows 版本）](https://cloud.tencent.com/developer/article/1803374)

> [!attention]
> 验证 `JDK` 是否下载成功:
> 
> ```bash
> java -version
> ```
> 只能用 `java -version` , 以下形式均不合法:
> - `java -v`
> - `java -V`
> - `java -Version`
> - `java --version`
> - `java --Version`

> [!info]
> java version "1.8.0_361"
> Java(TM) SE Runtime Environment (build 1.8.0_361-b09)
> Java HotSpot(TM) 64-Bit Server VM (build 25.361-b09, mixed mode)

# `VS Code` 报错

> [!danger]
> Please download and install a JDK to compile your project. You can configure your projects with different JDKs by the setting 'java.configuration.runtimes'

> [!tip] 解决报错
> 在 `VS Code` 中设置如下:
> 
> ```json
> // settings.json
> "java.configuration.runtimes": [
> 	{
> 		"name": "JavaSE-1.8",
> 		"path": "D:/Java/jdk1.8.0_361",
> 	},
> ]
> ```
> [参考](https://github.com/redhat-developer/vscode-java/wiki/JDK-Requirements#project-jdks)
> 
> 或者设置环境变量 `JAVA_HOME` 的值为 `D:/Java/jdk1.8.0_361`

> [!tip] `JDK` path
> JDK home path. Should be the JDK installation directory, not the Java bin path.
> 
> On Windows, backslashes must be escaped, i.e.
> 
> "path":"C:\\Program Files\\Java\\jdk1.8.0_161".

## `JAVA` 相关环境变量设置

- `JAVA_HOME` : `D:\Java\jdk1.8.0_361`
- `%JAVA_HOME%\bin` 加入 `Path` 环境变量中

### 查看 `java` 版本

```bash
java -version
```

### 查看 `javac` 版本

```bash
javac -version
```

### `Hello World`

```java
public class HelloWorld {

    public static void main(String []args) {
        System.out.println("Hello World");
    }
}
```

```bash
javac HelloWorld.java
java HelloWorld
```

# 环境变量

## `cmd`

查看所有环境变量的值:

```bash
set
```

查看某个环境变量的值:

```bash
set ENV_NAME
```

设置/修改某个环境变量的值:

```bash
set ENV_NAME=ENV_VALUE
```

> [!caution]
> 设置/修改/删除环境变量的值仅在当前窗口有效。

删除某个环境变量:

```bash
set ENV_NAME
```

## `powershell`

查看所有环境变量的值:

```bash
Get-ChildItem env:
ls env:
```

查看某个环境变量的值:

```bash
$env:ENV_NAME
```

设置/修改某个环境变量的值:

```bash
$env:ENV_NAME=ENV_VALUE
```

如设置环境变量 `JAVA_HOME` 的值:

```bash
$env:JAVA_HOME='D:\Java\jdk1.8.0_361\bin'
```

在当前窗口查看环境变量 `JAVA_HOME` 的值:

```bash
$env:JAVA_HOME
```

删除某个环境变量:

```bash
del env:ENV_EXAMPLE
```

> [!caution]
> 设置/修改/删除环境变量的值仅在当前窗口有效。