# scoop
scoop help #查看帮助
scoop help <某个命令> # 具体查看某个命令的帮助

## 安装 app
    scoop install <app>
    scoop install <app>@<version>
    scoop install <bucketName>/<app>
## 卸载 app
    scoop uinstall <app>

## 列出已安装的 app
    scoop list
## 搜索 app
    scoop search
## 检查哪些软件有更新
    scoop status

## 更新 scoop 自身; app; all
    scoop update 
    scoop update <appName1> <appName2>
    scoop update *
## 锁定 app 版本; 解锁
    scoop hold <app>
    scoop unhold <app>
## 切换 app 的版本
    scoop reset <app>@<version>
## 删除 app 旧版本
    scoop cleanup <app>

## 列出已知所有 bucket
    scoop bucket known
## 加某个 bucket
    scoop bucket add <bucketName>

## 查看所有以下载的缓存信息
    scoop cache show
## 清除 app 的下载缓存
    scoop cache rm <app>

##  别名
    scoop alias
