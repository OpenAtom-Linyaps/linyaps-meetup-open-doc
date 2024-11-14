# 玲珑应用构建工程基础知识
在正式开始构建一个玲珑应用工程前, 我们需要对关于玲珑应用构建的基础知识有一个认知, 以此协助我们更好地决策我们在启动构建工程前决定要准备哪些材料、进行哪一类型的操作

## 玲珑应用遵循的主流规范
每一款Linux桌面软件包管理方案为了能够保障完整的功能和良好的体验, 均需要遵守软件包管理方案提出的各类规范要求以最大限度发挥软件包管理方案的功能并保障应用生态体验.
如意玲珑也并不总是特立独行, 需要满足一定的规范来保障如意玲珑生态得以持续稳步发展.

目前如意玲珑生方案遵守以下主流的规范:

1. Freedesktop XDG规范
2. 玲珑应用目录结构规范
3. 玲珑应用构建工程配置文件 `linglong.yaml` 规范 

### Freedesktop XDG规范

1. 玲珑应用解决方案遵循Freedesktop XDG规范,一款正常的图形化应用应具备图标文件、desktop文件并符合Freedesktop XDG规范
2. 玲珑应用图标文件应该根据不同尺寸归类到`$PREFIX/share/icons/hicolor/目录下
3. 玲珑应用容器中使用 `XDG_DATA_DIRS` 等变量, 支持读写宿主机中的用户目录

### 玲珑应用目录结构规范

1. 玲珑应用遵循$PREFIX路径规则,该变量自动生成, 应用所有相关文件需存放于此目录下, 该目录层级下存在 `bin` `share` 等目录

2. 玲珑应用容器中的应用将不被允许读取宿主机中系统目录中的二进制文件、运行库

3. 玲珑应用容器中运行库、头文件所在目录将根据运行环境类型而异
foundation类: 在玲珑容器中映射为普通系统路径 `/usr/bin` `/usr/include` 等, 作为基础运行系统环境存在
runtime类: 在玲珑容器中映射为runtime容器路径 `/runtime/usr/bin` `/runtime/usr/include` 等, 作为基础运行系统环境存在

\*默认情况下, 玲珑容器内部的环境变量已自动处理好路径识别问题, 如:

```
PATH=szbt@szbt-linyaps23:/project$ echo $PATH
/bin:/usr/bin:/runtime/bin:/opt/apps/com.tencent.wechat/files/bin:/usr/local/bin:/usr/bin:/bin:/usr/local/games:/usr/games:/sbin:/usr/sbin
```

通用表达为:
```
PATH=szbt@szbt-linyaps23:/project$ echo $PATH
/bin:/usr/bin:/runtime/bin:$PREFIX/bin:/usr/local/bin:/usr/bin:/bin:/usr/local/games:/usr/games:/sbin:/usr/sbin
```

### 玲珑应用构建工程配置文件规范
1. 玲珑应用遵循 `$PREFIX` 路径规则,该变量自动生成，应用所有相关文件需存放于此目录下. 构建规则中若有需要涉及安装文件的操作, 均需要安装到 `$PREFIX` 路径下
\* `$PREFIX` 变量名即为填写的实际内容, **请勿使用 `绝对路径` 或任何具有绝对值作用的内容代替 **

2 玲珑应用目前遵循 `四位数字` 的版本号命名规则,不符合规则无法启动构建工程

3. `base`、`runtime` 版本支持自动匹配最新版本 `尾号`,版本号可以仅填写版本号的`前三位数字`.如:
当base `org.deepin.foundation`同时提供 `23.0.0.28` `23.0.0.29`, 若 `linglong.yaml` 中仅填写
```
base: org.deepin.foundation/23.0.0
```
那么在启动玲珑应用构建工程时, 将会默认采用最高版本号的 `23.0.0.29`

4 玲珑应用构建工程配置文件目前不直接兼容其他包构建工具的配置文件,需要根据构建工程配置文件案例来进行适配修改:
https://linglong.dev/guide/ll-builder/manifests.html