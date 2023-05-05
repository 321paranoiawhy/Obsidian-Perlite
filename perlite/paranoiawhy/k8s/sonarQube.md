# 教程

- [sonarQube下载配置及使用](https://blog.51cto.com/u_14082075/5465953)
- [SonarQube下载、安装、使用](https://www.jianshu.com/p/4d9d2534c0d3)
- [sonarqube7.7的下载与安装](https://blog.csdn.net/donggga/article/details/112938902)

# 下载

## sonarqube 7.1

[sonarqube 7.1 版本下载](https://binaries.sonarsource.com/Distribution/sonarqube/sonarqube-7.1.zip)

> [!warning]
> `sonarqube 7.9` 版本之后不再支持 `MySQL` [See here](https://github.com/SonarSource/docker-sonarqube/issues/563#issuecomment-1205710633)

下载 `7.1` 版本后解压, 双击 `bin\windows-x86-64\StartSonar.bat` 即可。

![[../Attachments/sonarQube 安装成功.png]]

安装成功后浏览器打开 `localhost:9000` 即可进入管理页面。

在 `conf\sonar.properties` 中加入以下内容:

```txt
sonar.jdbc.url=jdbc:mysql://127.0.0.1:3306/text?useUnicode=true&characterEncoding=utf8&rewriteBatchedStatements=true&useConfigs=maxPerformance&useSSL=false
sonar.jdbc.username=root  
sonar.jdbc.password=123456
sonar.sorceEncoding=UTF-8
sonar.login=admin
sonar.password=admin
```

其中:

- `sonar.jdbc.username` 和 `sonar.jdbc.password` 为 `mysql` 登录用户名和密码
- `sonar.login` 和 `sonar.password` 为 `localhost:9000` 登录用户名和密码

## 退出 sonarqube

> [!danger]
> 不能直接关闭 `cmd` 窗口, 否则下一次运行 `StartSonar.bat` 文件会报错。
> 应在 `sonarqube` 当前运行的 `cmd` 窗口快捷键 `CTRL + C` 然后输入 `Y` 退出, 下一次即可重启。

## Sonar-Scanner 2.5

[Sonar-Scanner 2.5 版本下载](https://binaries.sonarsource.com/Distribution/sonar-scanner-cli/)

![[../Attachments/Sonar-Scanner.png]]

配置环境变量:

设置环境变量 `SONAR_SCANNER_HOME` 的值为 `Sonar-Scanner` `bin` 文件夹路径, 并在 `Path` 中追加 `%SONAR_SCANNER_HOME%`。

```bash
sonar-scanner -h
sonar-scanner -v
```

![[../Attachments/Sonar-Scanner-h-v.png]]

切至项目根目录创建 `sonar-project.properties` 文件, 并在命令行下执行:

```bash
sonar-scanner
```

> [!warning]
> 文件名必须是 [sonar-project.properties](https://community.sonarsource.com/t/you-must-define-the-following-mandatory-properties-for-unknown-sonar-projectkey/41793/6), 否则会报错:
> 
> You must define the following mandatory properties for 'Unknown': sonar.projectKey, sonar.sources

> [!tip] sonar-project.properties
> 
> ```property
> # must be unique in a given SonarQube instance
> 
> # sonar.projectKey=integration-hub
> sonar.projectKey=integration-hub
> # this is the name and version displayed in the SonarQube UI. Was mandatory prior to SonarQube 6.1.
> sonar.projectName=integration-hub
> sonar.projectVersion=1.0 
> # Path is relative to the sonar-project.properties file. Replace "\" by "/" on Windows.
> # This property is optional if sonar.modules is set. 
> sonar.sources=.
> # Encoding of the source code. Default is default system encoding
> sonar.sourceEncoding=UTF-8
> ```

# mysql

登录:

```bash
mysql -u root -p
```


# 在 Docker 中运行 sonarqube

```bash
docker run -d --name sonarqube -e SONAR_ES_BOOTSTRAP_CHECKS_DISABLE=true -p 9999:9999 sonarqube:latest
```

运行完毕后打开 `localhost:9000`, 用户名和密码均为 `admin` 。

# 在 k8s 中运行 sonarqube

- [在Kubernetes上运行SonarQube](https://blog.frognew.com/2017/01/sonarqube-mysql-on-kubernetes.html)
- [Integrate SonarQube with Jenkins Pipeline | Sonarqube Integration with Jenkins Pipeline Script](https://www.youtube.com/watch?v=g3g3T6_abUU)

> [!error]
> Can not connect to database. Please check connectivity and settings (see the properties prefixed by 'sonar.jdbc.')

> [!tip]
> 配置环境变量 `SONARQUBE_JDBC_URL` 时, 端口后面的字符串表示 `MySQL` 的一个数据库(`Database`), 须手动创建该数据库。

## Jenkins 配置

- [SonarQube Scanner for Jenkins](https://plugins.jenkins.io/sonar/)
- [Installation](https://docs.sonarqube.org/latest/analyzing-source-code/scanners/jenkins-extension-sonarqube/#installation)

![[../Attachments/SonarQube Scanner Jenkins Plugin Installation.png]]

在 `Jenkins` 中创建 `SonarQube` 账户 [token](https://docs.sonarqube.org/latest/user-guide/user-account/generating-and-using-tokens/#generating-a-token):

`User` > `My Account` > `Security`.

![[../Attachments/Generating a token in SonarQube.png]]

将 `token` 保存到全局凭证中:

