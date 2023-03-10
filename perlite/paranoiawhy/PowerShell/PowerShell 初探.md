# 生成 `GUID`

```powershell
[guid]:NewGuid()
```

> [!info]
> 924e3c1d-8a6e-4975-b035-233af011e4fe

# `Base64`

- [原来浏览器原生支持 JS Base64 编码解码](https://www.zhangxinxu.com/wordpress/2018/08/js-base64-atob-btoa-encode-decode/)
- [PowerShell 技能连载 - 用 Base64 编解码文本](https://blog.vichamp.com/2016/01/01/encode-and-decode-text-as-base64/)
- [Windows PowerShell 中的 Base64 编码](https://www.delftstack.com/zh/howto/powershell/base64-encoding-in-windows-powershell/)

## 编码

`PowerShell` `Base64` 编码:

```bash
[Convert]::ToBase64String([Text.Encoding]::ASCII.GetBytes('test'))
```

> [!info] `PowerShell` 下 `Base64` 编码 'test'
> dGVzdA==

`js` 字符串转 `Base64` :

```js
const toBase64 = (str) => btoa(encodeURI(str));
toBase64('test'); // 'dGVzdA=='
```

## 解码

`PowerShell` `Base64` 解码:

```bash
[Text.Encoding]::ASCII.GetString([Convert]::FromBase64String('dGVzdA=='))
```

> [!info] `PowerShell` 下 `Base64` 解码 ‘dGVzdA=='
> test

`js` `Base64` 转字符串:

```js
const fromBase64 = (str) => decodeURI(atob(str));
fromBase64('dGVzdA=='); // 'test'
```

# 查看 `PowerShell` 版本信息

```bash
$PSVersionTable
```

> [!info]
> Name                           Value
> ----                           -----
> PSVersion                      5.1.19041.2364
> PSEdition                      Desktop
> PSCompatibleVersions           {1.0, 2.0, 3.0, 4.0...}
> BuildVersion                   10.0.19041.2364
> CLRVersion                     4.0.30319.42000
> WSManStackVersion              3.0
> PSRemotingProtocolVersion      2.3
> SerializationVersion           1.1.0.1

# 别名

- [PowerShell 别名](https://learn.microsoft.com/zh-cn/powershell/scripting/learn/ps101/05-formatting-aliases-providers-comparison?view=powershell-7.3#aliases)

## 获取指定别名信息

```bash
Get-Alias -Name dir
```

- `-Name` 位置参数可省略: `Get-Alias dir`
- `dir` 为 `Get-ChildItem` 的别名。
- 获取多个别名信息: `Get-Alias dir,pwd`, 其中 `pwd` 为 `Get-Location` 的别名。

## 查看指定命令的别名

```bash
Get-Alias -Definition Get-ChildItem, Get-Location
```

- `-Definition` 不可省略, 因为它不能用作位置参数。
- `Get-ChildItem` 的别名有 `dir`、`gci`、`ls`
- `Get-Location` 的别名有 `gl`、`pwd`

## 查看当前 `session` 中所有别名

`Get-Alias` 或其别名 `gal` :

```bash
Get-Alias
gal
```

> [!tip]
> 查看 `Get-Alias` 的别名:
> 
> ```bash
> Get-Alias -Definition Get-Alias
> ```

## 创建别名

### 当前 `session`

```bash
Set-Alias -Name alias -Value definition
```

- `alias` 为别名, `definition` 为原始命令 (如这里的 `Set-Alias`)
- `-Name` 和 `-Value` 可省略: `Set-Alias alias definition`

### 永久别名

为了设置永久别名, 可将别名写入到 `PowerShell Profile` 文件中。

查看 `PowerShell Profile` 路径:

```bash
$PROFILE
$profile
```

> [!info] $PROFILE
> C:\Users\Administrator\Documents\WindowsPowerShell\Microsoft.PowerShell_profile.ps1

> [!attention]
> 如果该文件不存在, 可通过如下命令创建:
> 
> ```bash
> New-Item -Type file -Force $profile
> ```

在 `PowerShell Profile` 文件中添加一行:

```bash
Set-Alias k8s kubectl
```

此命令将 `k8s` 永久设为 `kubectk` 的别名。

## 删除别名

### 当前 `session`

删除别名 `test` :

```bash
Remove-Item alias:test
```

### 永久删除

在 `PowerShell Profile` 文件中删除该行:

```bash
Set-Alias k8s kubectl
```