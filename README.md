# Scoop的安装 和 WindowsTerminal美化



## 安装Scoop

### 注意和推荐
- 用户名不含中文字符
- Windows 10
- PowerShell 7
- .NET Framework 4.5+

### 准备
win10自带PowerShell 5.X  
推荐PowerShell-7-win-x64.msi  https://github.com/powershell/powershell

### 安装Scoop
默认的Scoop应用会安装在 C:\Users<user>\scoop  
全局安装的程序（–global）位于C:\ProgramData\scoop  
可以通过环境变量更改设置（可能需要管理员）  
将Scoop安装到自定义目录
>\$env:SCOOP='D:\develop\Scoop'  
>[Environment]::SetEnvironmentVariable('SCOOP', $env:SCOOP, 'User')

将Scoop配置为将全局程序安装到自定义目录 SCOOP_GLOBAL
>\$env:SCOOP_GLOBAL='D:\develop\Scoop\GlobalScoopApps'  
>[Environment]::SetEnvironmentVariable('SCOOP_GLOBAL', $env:SCOOP_GLOBAL, 'Machine')


PowerShell运行命令
>Invoke-Expression (New-Object System.Net.WebClient).DownloadString('https://get.scoop.sh')

或
>iwr -useb get.scoop.sh | iex

如报错可尝试先运行
>Set-ExecutionPolicy RemoteSigned -scope CurrentUser

### 配置scoop
运行 scoop help 查看是否安装成功  
运行 scoop install sudo git curl，会自动安装7z  
运行 scoop install aria2 ，并配置
>scoop config aria2-max-connection-per-server 16  
>scoop config aria2-split 16  
>scoop config aria2-min-split-size 1M  

运行 scoop checkup 检测当前潜在问题，并根据提示进行修正

### 添加仓库
scoop bucket add extras  
推荐仓库有 extras nerd-fonts java versions nirsoft ...  
突然发现里面有许多好用的软件比如geekuninstaller、potplayer等等。。  
但是不推荐用scoop安装steam（软件自动更新问题）







## 安装和美化 Windows Terminal

### 链接
Github地址 https://github.com/microsoft/terminal  
Microsoft Store 搜索 Windows Teminal

### 安装字体
字体自选下载 https://www.nerdfonts.com/  
我使用的是 JetBrainsMono NF  
也可以scoop中的直接搜索，在nerd-fonts里

### 安装oh-my-posh
使用scoop安装主题
>scoop install https://github.com/JanDeDobbeleer/oh-my-posh3/releases/latest/download/oh-my-posh.json
>scoop install https://github.com/JanDeDobbeleer/oh-my-posh/releases/latest/download/oh-my-posh.json

### 设置 WindowsTerminal
打开设置，修改默认模式，如
>"defaultProfile": "{574e775e-4f2a-5b96-ac1e-a2962a402336}"

参考设置  
（这里的管理员模式需要安装gsudo）
>PowerShell -Command "Set-ExecutionPolicy RemoteSigned -scope Process; iwr -useb https://raw.githubusercontent.com/gerardog/gsudo/master/installgsudo.ps1 | iex"

这里的背景和图标都放在 C:\Users\user\AppData\Local\Packages\Microsoft.WindowsTerminal_8wekyb3d8bbwe\RoamingState 文件夹下  
图片链接 https://wallpaperhub.app/wallpapers/6277  
图标链接 https://www.iconfont.cn/search/index?searchType=icon&q=powershell

### 设置 oh-my-posh 主题
编辑$PROFILE，此文件中的命令会在每次打开power shell 7 的时候运行
>if (!(Test-Path -Path \$PROFILE )) { New-Item -Type File -Path $PROFILE -Force }
>notepad $PROFILE

写入（手动）
>Invoke-Expression (oh-my-posh --init --shell pwsh --config "$(scoop prefix oh-my-posh)/themes/jandedobbeleer.omp.json")

主题路径 Scoop\apps\oh-my-posh\current\themes  
jandedobbeleer.omp.json可更换为其他主题  
也可以自写主题然后手动指定主题路径
