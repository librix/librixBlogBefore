---
tags:
  - Chocolatey
---

发现很多软件的安装都需要 brew ，但是出于原因必须使用 Windows。所以找了一些资料，发现 Windows 下依然有类似的工具，出于一个显然的原因：Next，Next，Next 后，你不知道还需要去安装其它的东西才可以使用当前的软件……这是包的依赖关系。

正确的做法自然是使用包管理工具（Package Manager）去管理这些软件。Windows 用户可以使用 Chocolatey 这个包管理工具，Mac 用户可以使用 Homebrew 。

## 安装 Chocolatey

1.**以管理员身份打开命令行工具**

2.输入命令

3.测试

在 命令提示符 上安装 Chocolatey

```
@powershell -NoProfile -ExecutionPolicy unrestricted -Command "iex ((new-object net.webclient).DownloadString('https://chocolatey.org/install.ps1'))" && SET PATH=%PATH%;%ALLUSERSPROFILE%\chocolatey\bin
```

在 Powershell 上安装 Chocolatey

```
iex ((new-object net.webclient).DownloadString('https://chocolatey.org/install.ps1'))
```

> 提示：如果是在 Powershell 下面安装 Chocolatey 之前，先修改一下 Powershell 的执行策略，不然会出现 “此系统中禁止执行脚本” 这样的错误，解决的方法是执行下面的命令，意思就是把执行的策略设置成不限制：
> ```
> Set-ExecutionPolicy unrestricted
> ```

在命令行工具的下面进行测试，输入：

```
choco help
```

## 使用 Chocolatey

在 Chocolatey 的官方网站上（[https://chocolatey.org/packages](https://chocolatey.org/packages)）可以查看所有可以使用 Chocolatey 安装的东西。或者也可以在命令行工具的下面去搜索想要安装的东西：

```
choco search <keyword>
```

跟 `search` 命令功能类似的还有 `list`命令：

```
choco list <keyword>
```

比如搜索一下 nodeJS 相关的包，可以这样：

```
choco search nodeJS
```

上面的命令会在返回所以跟 nodeJS 相关的包，想要查看这些包所**有的可用的版本**，可以在命令的后面加上一个 -all 参数：

```
choco search nodeJS -all
```

[1]: https://ninghao.net/blog/2071	"路径（二）：更好的安装软件的方法"

安装包，用的是 `choco install` 命令

比如我们想去安装一个 cURL 工具，安装之前可以先用 search 命令搜索一下，搜索的时候加上 -all 参数，会显示出包的所有可用的版本，在安装的时候，你可以在 -version 参数的后面，指定一个具体要安装的版本，不使用 -version 参数，直接安装会安装包的最新发布的版本。

```
choco search curl -all
```

下面我们故意去安装一个旧版本的 curl ， 一会儿再去升级一下它。比如我要安装的是 7.22.0 版本的 curl ：

```
choco install curl -version 7.22.0
```

安装以后，可以用 choco list 命令，加上一个 -localonly 或 -lo（简写形式） 参数，查看在本地安装的包的列表。

```
choco list -localonly
```

升级安装在本地电脑上的包，用的是 choco upgrade 命令，后面加上要升级的包的名字：

```
choco  upgrade <package>
```

在升级包之前，可以先先去查看一下有没有可用的升级。如果你想查看 Chocolatey 本身有没有可用的升级，执行命令：

```
choco version
```

想要删除掉用 Chocolatey 安装的包，用的是 choco uninstall ，后面加上要卸载或者删除掉的包的名字。

```
choco uninstall <package>
```

在删除包之前，可以查看一下所有安装在本地的包的列表：

```
choco list -localonly
```

成功以后，再查看一下安装在本地的包的列表，已经看不到 cURL 了。