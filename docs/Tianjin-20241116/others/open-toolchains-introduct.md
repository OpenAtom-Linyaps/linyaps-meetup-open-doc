# 如意玲珑社区实用开源工具链介绍
此部分介绍如意玲珑社区中目前开放给同学们使用、学习的 `网页封装应用便捷适配套件` 、`玲珑应用自动化测试套件`

\* 套件中的部分功能基于 `deepin 23` 发行版进行适配, 其他发行版可能无法正确使能对应的功能, 建议搭建 `deepin 23` 作为构建&测试一体化平台或针对不同的发行版重新适配

## Electron Wrapper Next
Electron Wrapper Next用来包装任何一个网页到一个Electron应用。在结合本地npm缓存下,仅需数分钟即可产出任何一个网页封装之后的Electron二进制程序!
本项目是[Electron wrapper by Oyami-Srk](https://github.com/shirodeb/electron-wrapper)的正统精神传承，并承诺永久开源

### 上游版本限制条件

1. 当前源上游项目处于非活跃状态, 说明文档待完善, 对于入门贡献者存在使用门槛
2. 源上游项目大部分内容尚未完成通用化改造, 贡献者可自定义内容过少, 存在外部用户无法直接使用的风险
3. 源上游项目暂不支持批量任务
4. 源上游项目暂不支持生成与选中应用对应的玲珑应用构建工程配置文件 `linglong.yaml`


### 已实现功能
1. 支持用户通过设置可编辑变量自定义属于自己的版本
2. 支持x86_64、aarch64 CPU平台进行二进制应用构建
3. 支持导入符合模板的表格文件以开展批量任务
4. 支持将表格文件中的网页信息封装为Electron应用、deb应用安装包并生成玲珑应用构建工程配置文件 `linglong.yaml`
5. 支持自动生成通用资源 `desktop文件`、`icons目录` 等
6. 默认 `main` 分支使用 `cnpm` + `Electron` 中国大陆地区镜像站作为构建要素, 提高资源获取效率

### 支持用户自定义的变量

\* 该表以 `main` 分支最新状态为准, 其他分支无法确保以下变量的可用状态

| 变量 | 说明 |
|--------|---------|
| maintainer_name | 维护者名称标识 |
| maintainer_email | 维护者邮箱联系方式 |
| NODE_PATH | Node.Js二进制文件所在目录,即此目录层级下包含bin、lib等目录 |
| ELECTRON_VERSION | 与上述变量选中Node.Js版本相匹配的Electron版本, 3位数字版本号 |
| build_num | 构建次数标识号,自拟。默认情况下与Electron版本组合形成符合玲珑应用规范的四位数字版本号 |

## Next Linyaps Testing Toolchains
`Next Linyaps Testing Toolchains` 是一套shell脚本组成的玲珑应用测试工具链，旨在为玲珑应用测试带来更多便捷的方案
本项目是[linglong-automan](https://gitee.com/ziggy615/linglong-automan)的正统精神传承，并承诺永久开源

### 已实现功能

1. 将指定目录下零散的 `*binary.layer` 文件整理为一个具备规范化的目录结构: `xxx/id/package` 并生成存放玲珑应用id、应用版本号的两个表格

2. 指定整理完成的玲珑文件存放目录后，开启流水化安装进程

3. 指定资源存放目录和应用信息表格后，根据 `安装情况`、 `desktop文件存在状态` 、`窗口生成状态` 来模拟通过desktop文件启动应用，并对测试结果进行截图(xmind)
\* 当前代码部分功能依赖 `deepin 23` 系统组件，在其他发行版使用时需要重新适配

4. 对已安装的玲珑应用进行图标文件扫描, 判断当前应用icons目录及文件是否符合XDG规范并收集图标

5. 对已安装的玲珑应用进行批量卸载
