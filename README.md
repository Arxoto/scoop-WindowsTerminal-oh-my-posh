# Scoop的安装 和 WindowsTerminal美化



## 安装Scoop

### 注意
用户名不含中文字符  
Windows 7 SP1+ / Windows Server 2008+  
PowerShell 3+  
.NET Framework 4.5+

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

如报错可尝试运行
>Set-ExecutionPolicy RemoteSigned -scope CurrentUser

### 配置scoop
运行 scoop help 查看是否安装成功  
运行 scoop install sudo git curl，会自动安装7z  
运行 scoop install aria2 ，并配置
>scoop config aria2-max-connection-per-server 16  
>scoop config aria2-split 16  
>scoop config aria2-min-split-size 1M

### 添加仓库
scoop bucket add extras  
突然发现里面有许多好用的软件比如geekuninstaller、potplayer等等。。  
但是不推荐用scoop安装steam - -







## 安装和美化 Windows Terminal

### 链接
Github地址 https://github.com/microsoft/terminal  
Microsoft Store 搜索 Windows Teminal

### 安装字体
字体自选下载 https://www.nerdfonts.com/  
我使用的是 JetBrainsMono NF

### 安装oh-my-posh
使用scoop安装主题
>scoop install https://github.com/JanDeDobbeleer/oh-my-posh3/releases/latest/download/oh-my-posh.json

### 设置
打开设置，修改默认模式，如
>"defaultProfile": "{574e775e-4f2a-5b96-ac1e-a2962a402336}"

参考设置  
（这里的管理员模式需要安装gsudo）
>PowerShell -Command "Set-ExecutionPolicy RemoteSigned -scope Process; iwr -useb https://raw.githubusercontent.com/gerardog/gsudo/master/installgsudo.ps1 | iex"

这里的背景和图标都放在 C:\Users\user\AppData\Local\Packages\Microsoft.WindowsTerminal_8wekyb3d8bbwe\RoamingState 文件夹下  
图片链接 https://wallpaperhub.app/wallpapers/6277  
图标链接 https://www.iconfont.cn/search/index?searchType=icon&q=powershell
>{  
    // 默认模式的值就是guid  
    "guid": "{41dd7a51-f0e1-4420-a2ec-1a7130b7e950}",  
    "name": "PowerShell Elevated",  
    "hidden": false,  
    // 管理员模式打开power shell 7  
    "commandline": "sudo.exe pwsh",  
    // 启动路径  
    "startingDirectory": "D:/",  
    // 图标  
    "icon" : "ms-appdata:///roaming/powershell.png",  
    // 字体和大小  
    "fontFace": "JetBrainsMono NF",  
    "fontSize": 11,  
    // 背景颜色和亚克力效果  
    "background": "#013456",  
    "useAcrylic": true,  
    "acrylicOpacity": 0.5,  
    // 背景图片 伸缩模式为按比例放大 背景图片透明度  
    "backgroundImage": "ms-appdata:///roaming/goose.png",  
    "backgroundImageStretchMode": "uniformToFill",  
    "backgroundImageOpacity": 0.6  
}

编辑$PROFILE，此文件中的命令会在每次打开power shell 7 的时候运行
>if (!(Test-Path -Path \$PROFILE )) { New-Item -Type File -Path $PROFILE -Force }

以上命令可能需要，使用vsCode编辑
>code $PROFILE

没有vsCode也可以用
>notepad $PROFILE

写入（手动）
>Invoke-Expression (oh-my-posh --init --shell pwsh --config "$(scoop prefix oh-my-posh)/themes/jandedobbeleer.omp.json")

主题路径 Scoop\apps\oh-my-posh\current\themes  
jandedobbeleer.omp.json可更换为其他主题  
自写的一个主题
>{  
  "$schema": "https://raw.githubusercontent.com/JanDeDobbeleer/oh-my-posh3/main/themes/schema.json",  
  "blocks": [  
    {  
      "type": "prompt",  
      "alignment": "right",  
      "vertical_offset": -1,  
      "segments": [  
        {  
          "type": "time",  
          "style": "plain",  
          "foreground": "#007ACC",  
          "properties": {  
            "time_format": "15:04:05"  
          }  
        }  
      ]  
    },  
    {  
      "type": "newline"  
    },  
    {  
      "type": "prompt",  
      "alignment": "left",  
      "segments": [  
        {  
          "type": "session",  
          "style": "diamond",  
          "leading_diamond": "\uE0B6",  
          "trailing_diamond": "\uE0B0",  
          "foreground": "#100e23",  
          "background": "#ffffff"  
        },  
        {  
          "type": "path",  
          "style": "powerline",  
          "powerline_symbol": "\uE0B0",  
          "foreground": "#100e23",  
          "background": "#91ddff",  
          "properties" : {  
              "home_icon": "\uF7DB",  
              "folder_icon": "\uF115",  
              "folder_separator_icon": " \uE0B1 ",  
              "style": "agnoster"  
          }  
        },  
        {  
          "type": "git",  
          "style": "powerline",  
          "powerline_symbol": "\uE0B0",  
          "foreground": "#193549",  
          "background": "#95ffa4"  
        },  
        {  
          "type": "exit",  
          "style": "powerline",  
          "powerline_symbol": "\uE0B0",  
          "foreground": "#ffffff",  
          "background": "#ff8080"  
        }  
      ]  
    }  
  ],  
  "final_space": true  
}  




