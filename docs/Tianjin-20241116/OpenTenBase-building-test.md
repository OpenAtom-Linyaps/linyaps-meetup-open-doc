# OpenTenBase项目源码玲珑编译演示
从OpenTenBase开源社区分享的内容中可以得知, 目前OpenTenBase开源社区维护的 `OpenTenBase` 开源项目目前在代码托管平台GitHub上提供了项目源代码以及编译文档
除此之外, 我们从前面的环节可以了解到, 如意玲珑容器内除了提供图形化程序运行所必须要的运行库以外, 也同时提供了GNU Autotools等主流构建配置工具、Qt等主流运行库的头文件用于支持我们在玲珑容器中将应用项目源代码编译为可供容器运行的二进制执行文件.

## 构建工程准备
在开始构建`OpenTenBase` 开源项目前, 我们首先需要确保当前系统环境具备完整的玲珑运行及构建环境(ll-builder)
不同发行版的具体安装方式可参考:
[安装玲珑](https://linglong.dev/guide/start/install.html)

从当前玲珑构建工程--源码编译案例来看, 功能上玲珑构建工具支持在应用构建工程配置文件 `linglong.yaml` 中设置git仓库来源及相关commit记录即可拉取对应的源码到构建目录中并通过指定编译规则来实现 `一站源码获取==>源码编译==>二进制安装&封装`

为了方便调试&实时调整, 我这里不使用构建规则, 直接进入玲珑容器进行人工编译

### 源码获取
首先, 我们通过`OpenTenBase` 开源项目下载页面进入代码平台并获取相关源码归档包, 为了节省时间, 我这里已经提前将源码下载到一个新建的构建工程目录中
[OpenTenBase 开源项目下载页面](https://docs.opentenbase.org/download/)

### 源码类型解析
按照习惯思维来说,在解压得到源码后, 我们进入源码目录来查看大体的源码结构, 来判断我们应该采用什么样类型的源码构建工具
实际上, 咱们 `OpenTenBase` 开源项目已经很贴心为我们刚接触本项目的小伙伴提供了完整的编译指导参考, 因此我们可以直接从编译文档中得知 `OpenTenBase` 开源项目使用的是 `GNU Autotools` 构建工具

除此之外, 编译文档中同时提供了一键安装编译依赖软件包的安装示例, 确保可以使我们的环境更便捷地满足编译条件
考虑到目前玲珑容器内暂不支持直接通过apt等软件包管理器安装软件包, 因此我们需要进入容器开始编译才能确认是否完全满足编译要求

### 创建玲珑容器
为了得到一个可以用于编译的玲珑容器, 我们先简单设置一个应用构建工程配置文件 `linglong.yaml` 用于生成容器
\* 根据 `linglong.yaml` 示例, 我们填写`id`、`version`、`base`、`runtime`等基础信息, 由于本次工程人工干预, 因此无需填写完整的`build`构建规则

保存后,我们在该文件所在目录层执行下列指令可创建符合 `linglong.yaml` 描述的玲珑容器并同时进入容器
```
szbt@szbt-linyaps23:/media/szbt/Data/ll-build/WeChat$ ll-builder build --exec bash
```

### 尝试编译
在进入容器后, 默认路径即为 `linglong.yaml` 所在的构建工程目录, 我们可以在此处看到提前解压的 `OpenTenBase` 开源项目源码
为了尽可能避免代码被直接修改, 我们创建一个`build`目录, 在`build`目录中执行编译参数
我们从[OpenTenBase 开源项目编译手册](https://docs.opentenbase.org/guide/01-quickstart/#_3)中复制 `configure` 编译参数到玲珑容器中进行编译
\* 需要关注的是, `--prefix` 参数用于指定项目的 `最终安装目录`, 结合上一环节对玲珑应用构建工程基础知识的解读, 我们使用此参数指定本次编译的安装路径并开始编译

```
./configure --prefix=$PREFIX/ --enable-user-switch --with-openssl --with-ossp-uuid CFLAGS=-g
```