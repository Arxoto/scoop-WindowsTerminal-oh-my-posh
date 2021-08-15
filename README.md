# Scoop的安装 和 WindowsTerminal oh-my-posh美化



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
>or  
>iwr -useb get.scoop.sh | iex

如报错可尝试先运行
>Set-ExecutionPolicy RemoteSigned -scope CurrentUser

### 配置scoop
运行 scoop help 查看是否安装成功  
运行 scoop install sudo git curl，会自动安装7z  
运行 scoop install aria2（用aria2代替下载，可跳过），并配置
>scoop config aria2-max-connection-per-server 16  
>scoop config aria2-split 16  
>scoop config aria2-min-split-size 1M  

运行 scoop checkup 检测当前潜在问题，并根据提示进行修正

### 添加仓库
scoop bucket add extras  
推荐仓库有 extras nerd-fonts java versions nirsoft dorado ...  
不推荐用scoop安装steam（软件自动更新问题）  
  
推荐部分软件  
dismplusplus（系统优化垃圾清理） driverstoreexplorer（驱动清理） freemove（mklink移动文件） spacesniffer or wiztree（查看盘符文件占用） memreduct（内存清理）  
geekuninstaller（卸载工具） hasher（计算hash） notepadplusplus（记事本） potplayer（播放器）  
trafficmonitor（网速温度占用） ditto（剪切板 系统自带win+v） switchhosts（host切换）  
qbittorrent-enhanced（bt下载） motrix or neatdownloadmanager（下载器）  
screentogif（录屏gif） sumatrapdf（pdf阅读）  
everything or listary or wox（搜索启动）  
JetBrainsMono-NF SarasaGothic-SC   
ffmpeg youtube-dl youtube-dl-gui    







## 安装和美化 Windows Terminal and oh-my-posh

### Windows Terminal
Github地址 https://github.com/microsoft/terminal  
Microsoft Store 搜索 Windows Teminal

### 设置 WindowsTerminal
打开设置，修改setting.json
>"defaultProfile": "{574e775e-4f2a-5b96-ac1e-a2962a402336}"

自行修改，具体参考我上传的json  
（管理员模式需要安装gsudo提权）
>PowerShell -Command "Set-ExecutionPolicy RemoteSigned -scope Process; iwr -useb https://raw.githubusercontent.com/gerardog/gsudo/master/installgsudo.ps1 | iex"  
>or    
>scoop install gsudo  

我的背景和图标都放在 C:\Users\user\AppData\Local\Packages\Microsoft.WindowsTerminal_8wekyb3d8bbwe\RoamingState 文件夹下  
使用时路径为 ms-appdata:///roaming/goose.png  
图片链接 https://wallpaperhub.app/wallpapers/6277  
图标链接 https://www.iconfont.cn/search/index?searchType=icon&q=powershell

### 字体
oh-my-posh的部分图标需要字体支持 不然会出现口口  
字体自选下载 https://www.nerdfonts.com/  
我使用的是 JetBrainsMono NF  
也可以scoop中的直接搜索，在nerd-fonts里

### 安装oh-my-posh
使用scoop安装主题  
https://github.com/JanDeDobbeleer/oh-my-posh  
https://ohmyposh.dev/docs/windows  
>scoop install oh-my-posh3

### 设置 oh-my-posh 主题
编辑$PROFILE  
此文件中的命令会在每次打开power shell 7 的时候运行，同理在该文件中删去oh-my-posh初始化命令则不启用oh-my-posh
>if (!(Test-Path -Path \$PROFILE )) { New-Item -Type File -Path $PROFILE -Force }  
>notepad $PROFILE

写入（手动）
>Invoke-Expression (oh-my-posh --init --shell pwsh --config "$(scoop prefix oh-my-posh)/themes/jandedobbeleer.omp.json")

主题路径 Scoop\apps\oh-my-posh\current\themes  
jandedobbeleer.omp.json可更换为其他主题  
也可以自写主题然后手动指定主题路径

