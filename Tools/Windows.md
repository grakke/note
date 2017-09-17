# Windows

## 工具

- launchy Wox Rolan
- markdown编辑器: 作业部落 MarkdownPad(需要浏览器渲染插件awesome) MarkPad
- 资源管理器: Clover Total Commander
- 快捷键：AutoHotKey
- 本地搜索：Listary Everything
- 编辑器：Atom SublimeText3
- 工具：ShareX
- 同步工具：goodsync
- 词典：GoldenDict
- vagrant
- VistaSwitcher：程序切换工具
- StrokeIt:让鼠标手势无处不在
- Rolan 轻量级桌面启动器
- Listary :Windows 文件浏览增强工具
- f.lux 随时间改变屏幕色温
- RSS:深蓝阅读 theoldreader
- Foxit Reader
- editor：Visual Studio Code
- 命令行：xshell
- CCleaner, Defraggler, Recuva & Speccy.
- [Chocolatey](https://chocolatey.org/):The package manager for Windows Software Management Automation

  ```
  // 以管理员运行cmd
  @"%SystemRoot%\System32\WindowsPowerShell\v1.0\powershell.exe" -NoProfile -InputFormat None -ExecutionPolicy Bypass -Command "iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))" && SET "PATH=%PATH%;%ALLUSERSPROFILE%\chocolatey\bin"
  ```

## 配置

添加自启动：启动文件放在C:\Users\henryli\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Startup

- Evernote
- Foxmail
- RTX
- TIM
- Youdao
- Sticky Notes
- 支持bash：在启用或关闭 Windows 功能，开启Windows Subsystem for linux (Beta)，通过bash切换到bash[参考](https://blog.jessfraz.com/post/windows-for-linux-nerds/)

  ```
  PowerShell as Administrator and run:
  Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux
  restart system
  cmd + r input:bash download ubuntu
  ```

## 快捷键

- alt+tab：长按为显示任务列表，短切为与上次任务切换
- WIN+D：窗口最小化，显示桌面，再按一次还原桌面；
- WIN+R：打开运行，输入命令可以执行相应操作，输入路径可以打开对应路径，输入程序名称可以打开对应程序（前提是你打开的是windows下面的程序）;输入cmd打- 开DOS窗口，输入notepad打开记事本，输入calc打开计算器等。
- WIN+E：打开我的电脑；
- CTRL+ALT+Delete Ctrl + Shift + Esc ：程序不响应时用这一招结束不响应的程序，xp下用得比较多；
- WIN+L：锁屏；
- WIN+Tab/ALT+SHIFT+TAB：切换程序；
- CTRL+W：关闭程序标签页；
- CTRL+Home：跳转到文件最开头，直接按Home跳转到行头；
- CTRL+End：跳转到文件尾部，直接按End跳转到行尾；
- ALT+双击：查看文件属性；
- WIN+数字键：启动任务栏上的程序；
- ctrl + z/y:
- 在桌面或者任何文件夹下，SHIFT+鼠标右键，可以在当前路径下打开DOS命令窗口；
- 在桌面或者任何文件夹下，CTRL+鼠标左键，拖动文件、文件夹都可以立马生成文件对应的副本；
- 新建只有扩展名的文件的方法：".suffix."，·比如创建.gitignore，正常情况下windows是不允许创建的，但在扩展名后面加点，即.gitignore.就可以正常创建了；
- CTRL+SHIFT+ESC/Ctrl+Alt+Del：打开进程管理器；
- WIN+左箭头：当前窗口缩放为屏幕的一半，靠屏幕左侧显示；
- WIN+右箭头：当前窗口缩放为屏幕的一半，靠屏幕右侧显示；
- WIN+上箭头：最大化当前窗口；
- WIN+下箭头：还原和最小化当前窗口；
- Win+Shift+左箭头：移动到左边屏幕。
- Win+Shift+右箭头：移动到右边屏幕。
- 在桌面上，右键任何一个程序，鼠标定位到快捷键一栏，为该应用设置启动快捷键，然后你就可以通过这个这个快捷键来启动该程序啦；
- alt + f4:关闭程序
- shift + del：彻底删除文件
- alt + d：定位到地址栏
- f11：窗口最大化的来回切换
- alt + ←/→：切换上下级文件
- ctrl+shift+n：新建文件夹
- WIN+Home：最小化所有窗口，除了当前激活窗口；
- WIN+M：最小化所有窗口；
- WIN+SHIFT+M：还原最小化窗口到桌面上；
- WIN+P：选择一个演示文稿显示模式；
- WIN+Pause：显示系统属性对话框；
- WIN+F：打开windows帮助中心；
- WIN+T/alt+ESC：切换任务栏上的程序；
- WIN+ALT+数字：让位于任务栏指定位置（按下的数字作为序号）的程序，显示跳转清单；
- Win + Home：最小化所有窗口，除了当前激活窗口
- win + p:投影
- 命令行：WIN+R

  - 输入"msconfig"，弹出系统设置界面，可设置禁止、允许进程开机自启动；
  - 输入"psr"后回车：打开步骤记录器；
  - 输入"mip"，启动数学公式手写板；
  - cmd进入命令行

```
ipconfig /flushdns：刷新域名
```

快捷方式可以设置快捷键

- Shift+Tab（返回上一个选项或上一栏）
- Ctrl+Shift+Tab（切换至上一个标签）
- CTRL+鼠标左键，拖动文件、文件夹都可以立马生成文件对应的副本
- Win+T to cycle through the taskbar icons
- Win + d：删除文件

## 软件安装

```
choco search python php birtualbox jdk8 cclear
choco uninstall python

choco install mysql.workbench
```