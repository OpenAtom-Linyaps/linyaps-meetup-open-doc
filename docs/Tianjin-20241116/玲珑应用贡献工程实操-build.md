# 玲珑应用贡献工程实操
本次实操中所选用的构建辅助套件均支持一键将选定的网页封装为玲珑应用容器格式的独立程序,因此本部分暂时忽略套件的功能介绍,直接提供本次演习方案

## 环境准备
### 必选
在开始工程前,你应该先确保你的操作系统环境已经具备以下条件:
1. 已经安装`linglong-bin`和`linglong-builder`且具备桌面环境的Linux发行版(即ll-cli和ll-builder命令被使能)
[如意玲珑环境当前官方支持的多个发行版安装方式](https://linglong.dev/guide/start/install.html)
2. 确定你想用于封装所选网页的`Electron版本`,且本地目录中已经存在与该Electron版本相容的`Node.Js二进制文件`,并可以执行`npm`操作

### 可选
1. 由于deepin 23属于目前在如意玲珑社区中作为适配活跃度比较高的发行版,建议使用deepin 23作为玲珑应用构建平台以体验更多特性
2. 本次实操中所使用的便捷构建套件同时也具备生成传统deb安装的能力,若有该需求可安装相关的软件包以创建deb安装包
```
dh-make devscripts build-essential
```

## 构建工程
### 材料准备
在开始任务前,你应该先准备以下几样材料以准备参加玲珑应用便捷构建实操.
1. 在提供的应用清单-共享文档中,领取你想要进行适配的应用,在表格中,依次按照了便捷构建套件中所需的材料进行了排列
2. 下载/获取本次案例中将会使用的构建、测试套件到一个具备读写权限的目录中:
[Electron Wrapper Next](https://github.com/OpenAtom-Linyaps/sig-next-electron-wrapper)
[Linyaps Testing Toolchains](https://github.com/OpenAtom-Linyaps/sig-next-linyaps-testing-toolchains)

### 修改脚本
在得到以上文件后,你现在就可以开始编辑构建套件 `Electron Wrapper Next` 中的 `master-build.sh` 脚本以适配你的设置啦.主要修改的内容可以参考以下说明:
本构建套件当前提供的版本已经适配本次实操活动中提供的应用清单,因此仅需要修改脚本中数个变量的值即可开始构建
\* 注: 仅有 `Writeable Envs` 区域中留空变量支持修改,`Auto-generated` 区域后的变量请勿随意修改!

| 需要修改的变量值 | 说明 |
|---------|---------|
| maintainer_name | 维护者名称标识 |
| maintainer_email | 维护者邮箱联系方式 |
| NODE_PATH | Node.Js二进制文件所在目录,即此目录层级下包含bin、lib等目录 |
| ELECTRON_VERSION | 与上述变量选中Node.Js版本相匹配的Electron版本, 3位数字版本号 |
| build_num | 构建次数标识号,自拟。默认情况下与Electron版本组合形成符合玲珑应用规范的四位数字版本号 |

### 准备脚本需要导入的数据表格
便捷构建套件通过导入符合模板结构的csv数据表格为玲珑应用构建提供应用素材,模板文件 `app-info.csv` 可从 `Electron Wrapper Next` 项目中的template目录中获取
可以参考以下对每列的解释来设置数据:
| 列数 | 填入的内容 |
| 1列 | 应用包名,用于决定玲珑应用的id及Electron应用信息 |
| 2列 | 应用名,用于决定玲珑应用的Name及Electron应用名 |
| 3列 | 应用主界面对应的页面,即你期待封装为Electron应用后主界面展示的网站 |
| 4列 | 应用图标,即你期待该应用安装后在启动器中显示的图标、应用运行时任务栏显示的图标 |
| 5列 | 开发者名称,用来标记该应用的版权信息 |

\* 当前脚本使用 `_` 作为csv列分割符号,建议使用文本编辑器、vim等文本编辑器打开,在输入内容时以 `1列_2列_3列_4列_5列` 格式按行输入,填写完成后可另存为副本csv文件,使用办公软件打开来确认是否符合行列排布信息

可参考的样例:
```
❯ neovim '/home/ziggy/deepin-community/docs/data/meetup-stage-1/apps-data-release.csv' 
com.poki.apple-knight-golf_Apple Knight Golf_https://poki.com/zh/g/apple-knight-golf_"https://img.poki-cdn.com/cdn-cgi/image/quality=78,width=256,height=256,fit=cover,f=auto/18ac0a1db67de81059a244c39e3bba34.png"_Limitless
com.poki.super-fowlst-2_Super Fowlst 2_https://poki.com/zh/g/super-fowlst-2_"https://img.poki-cdn.com/cdn-cgi/image/quality=78,width=256,height=256,fit=cover,f=auto/e11252e95a1916483ac3dd76cecfa280.png"_Thomas K. Young
```

### 启动构建流程
在完成上述步骤,就可以一键开启构建步骤啦
在此之前,建议再对构建环境进行验证,以确保你的环境具备 `ll-builder` 且可以执行 `ll-builder build`
此刻,你可以开始构建了,用法为执行脚本时传入一个参数,此参数为上一环节准备的数据表格,参考:
```
░▒▓ ~/linyaps-community/auto-electron-wrapper-next-7.4.3-linyaps/template ▓▒░───────────────────────────────────────────────────────────────░▒▓ 18:26:33 ▓▒░─╮
❯ ./master-build.sh data/app-info.csv 
```

### 整理产出
在任务结束后,你就可以在 `master-build.sh` 脚本所在目录的 `build-pool` 下找到你构建的应用包名，bins目录内已存放可以安装的 `binary.layer` 文件
示例结构:
```
├── build-pool
│   └── com.silvergames.halloween-murder
│       ├── bins
│       │   ├── com.silvergames.halloween-murder.linyaps_28.3.3.1_x86_64_binary.layer
```

## 兼容性自助测试
本环节将会运用兼容性自助测试套件[Linyaps Testing Toolchains](https://github.com/OpenAtom-Linyaps/sig-next-linyaps-testing-toolchains)来对上一环节产出的玲珑应用安装文件 `binary.layer` 进行测试验证

### 环境预备
在开始使用测试套件前,你需要确保当前环境满足以下条件
1. 本次实操中所使用的自助兼容性测试套件部分功能需要使用 `Linux x11` 窗口管理工具,因此在使用前需要安装以下软件包:
```
wmctrl x11-utils
```
2. 测试套件通过x11窗口管理工具来判断应用窗口启动状态,因此需要确保你的系统是 `x11` 环境而不是 `Wayland` 环境。
3. `wmctrl` 与 `xwininfo` 组件可以正常生效,可以通过`xwininfo`查询窗口信息

### 测试启动
1. 第一步是使用 `Linyaps Testing Toolchains` 中的 `linyaps-auto-optimize.sh` 脚本对上一阶段产出的 `binary.layer` 文件进行自动整理，以满足脚本的功能
执行参数参考:
```
szbt@szbt-linyaps23:/media/szbt/Data/stage2-test$ ./linyaps-auto-optimize.sh ./ll-bins ./ll-pool

```

\* 参数顺序依次为: `binary.layer` 存放目录、 放置整理后的 `binary.layer` 目录

2. 在整理完成后将会在工作目录生成 `ll-pkg-name.csv` `ll-pkg-version.csv` 文件,分别代表指定目录中的 `玲珑应用id` 与匹配的` 版本号`,我们现在手动将两个表格合并,之后得到一个具有id、版本号双列内容的新 `ll-pkg-info.csv` 文件:
```
szbt@szbt-linyaps23:/media/szbt/Data/stage-1-fix1/linyaps-testing-toolchains-1.3.2-dev$ cat ll-pkg-info.csv
com.poki.2-player-city-racing-2.linyaps,28.3.3.3001
```

3. 到这一步就可以启动自动安装脚本 `linyaps-auto-install-release.sh` 了,用于批量安装上阶段整理后的玲珑应用,输入参数为 `玲珑应用存放目录`.
参考:
```
szbt@szbt-linyaps23:/media/szbt/Data/stage-1-fix2$ ./linyaps-auto-install-release.sh ../ll-pool
```

4. 等任务结束后就意味着可以启动应用兼容性测试了,可以看到测试套件目录中有脚本 `linyaps-auto-screenshot-general.sh`.
我们先创建一个`res`目录用于存放玲珑应用的资源,如图标等.
传入参数参考:
```
szbt@szbt-linyaps23:/media/szbt/Data/stage-1-fix2$ ./linyaps-auto-screenshot-dev.sh ../res/ ./ll-pkg-info.csv
```
其中 `ll-pkg-info.csv` 来源于上文生成

\* 由于该测试流程存在窗口判断,因此需要在图形化终端执行此脚本,并在启动脚本后最小化该终端窗口

主要有两种异常情况:
1. 超时未生成窗口的应用则会被写入`failed.csv`文件中,以判断为应用无法启动
2. 玲珑应用目录内不包含图标文件,则会被写入`icons-missing.csv`文件中,不满足如意玲珑社区中对于图形化应用的规范

### 隐藏功能
此测试套件支持在deepin 23的系统版本下自动截取应用窗口运行截图,若测试环境为deepin 23,可使用另一版本的测试套件 `linyaps-auto-screenshot-deepin23.sh`

1. 在启动测试前,需要额外安装以下软件包
```
deepin-screen-recorder imagemagick-6.q16
```

2. 确保deepin 23中系统截图保存路径为当前用户的~/Pictures/Screenshots中,且该目录为空

满足上述条件后启动测试套件,则在应用启动检测与图标检测的结果外,在指定的`res`目录中提供应用运行截图
