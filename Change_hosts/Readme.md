# 改hosts的bat

- 其中p站加host前面没有加入开启管理员模式的代码，所以请右键以管理员方式运行
- 开启管理员模式的代码可能有些电脑不支持？？ **存在这种问题**

- 开启管理员模式的打码如下
```
@echo off
rem 开启管理员模式, 如果出现闪退情况
rem 例如在win10中貌似不需要开启管理员模式即可运行下方命令
rem 则将下面:Admin以上到本行的代码注释掉即可
cacls.exe "%SystemDrive%\System Volume Information" >nul 2>nul
if %errorlevel%==0 goto Admin
if exist "%temp%\getadmin.vbs" del /f /q "%temp%\getadmin.vbs"
echo Set RequestUAC = CreateObject^("Shell.Application"^)>"%temp%\getadmin.vbs"
echo RequestUAC.ShellExecute "%~s0","","","runas",1 >>"%temp%\getadmin.vbs"
echo WScript.Quit >>"%temp%\getadmin.vbs"
"%temp%\getadmin.vbs" /f
if exist "%temp%\getadmin.vbs" del /f /q "%temp%\getadmin.vbs"
exit

:Admin
```

## 主要代码

- 先进入hosts所在的目录
```
@echo off
c:
cd %SystemRoot%\system32\drivers\etc\
```

- 然后所以加入的内容输入到hosts里

    - 以加入p站hosts为例
    - echo. >> hosts 这句是加入一个换行到host里
    - 需要管理员运行这个bat
```
echo. >> hosts
echo 210.129.120.41 pixiv.net >> hosts
echo 210.129.120.44 accounts.pixiv.net >> hosts
echo 210.140.131.145 source.pixiv.net >> hosts
echo 210.140.131.160 d.pixiv.org >> hosts
echo 210.140.131.144 imgaz.pixiv.net >> hosts
echo 210.129.120.41 www.pixiv.net >> hosts
```
