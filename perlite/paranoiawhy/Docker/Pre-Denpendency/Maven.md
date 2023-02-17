# 什么是 `Maven`

`Maven` 是 `JAVA` 项目的依赖管理工具。

# 下载 `3.6.3` 版本

- [Maven Previous Release](https://maven.apache.org/download.cgi#previous-releases)
- [Index of /dist/maven/maven-3/3.6.3/binaries](https://archive.apache.org/dist/maven/maven-3/3.6.3/binaries/)
- [Windows 环境下 maven 安装与环境变量配置](https://www.cnblogs.com/liuhongfeng/p/5057827.html)
- [How do I fix maven error The JAVA_HOME environment variable is not defined correctly?](https://stackoverflow.com/questions/44680125/how-do-i-fix-maven-error-the-java-home-environment-variable-is-not-defined-corre)

查看 `maven` 是否安装成功:

```bash
mvn --version
```

或者使用如下命令:

```bash
echo %MAVEN_HOME%
```

> [!danger]
> The JAVA_HOME environment variable is not defined correctly
> This environment variable is needed to run this program
> NB: JAVA_HOME should point to a JDK not a JRE

修改 `JAVA_HOME` 的值为 `D:\Java\jdk1.8.0_361`, 注意路径末尾不需要 `\bin` 。

> [!info] mvn --version
> Apache Maven 3.6.3 (cecedd343002696d0abb50b32b541b8a6ba2883f)
> Maven home: D:\Software\apache-maven-3.6.3\bin\..
> Java version: 1.8.0_361, vendor: Oracle Corporation, runtime: D:\Java\jdk1.8.0_361\jre
> Default locale: zh_CN, platform encoding: GBK
> OS name: "windows 10", version: "10.0", arch: "amd64", family: "windows"

> [!info] echo %MAVEN_HOME%
> D:\Software\apache-maven-3.6.3

# 安装项目依赖

```bash
mvn 
```