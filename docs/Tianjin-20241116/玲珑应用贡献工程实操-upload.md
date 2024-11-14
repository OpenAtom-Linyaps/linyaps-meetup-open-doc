# 玲珑应用贡献工程实操
本部分用于指引同学们通过不同的渠道&方式来提交在玲珑应用贡献工程实操中产出的贡献,即玲珑应用安装包 `binary.layer` 文件等
目前支持同学们提交生态贡献的途径主要有:

1. 贡献者通过在如意玲珑开源社区GitHub平台上的[公共构建平台](https://github.com/linglongdev)来提交玲珑应用构建工程配置文件 `linglong.yaml`
2. 贡献者通过[统信开发者应用分发平台](https://www.chinauos.com/partner/distribute)使用个人开发者账户上传玲珑应用安装包

## 贡献演示
### GitHub公共构建平台
若你决定通过GitHub公共构建平台进行玲珑生态的贡献, 在此之前你应当持有一个可以正常进行活动的GitHub账户以及保持网络连接顺畅.

1. 访问[公共构建平台](https://github.com/linglongdev), 在 `Repositories` 页面搜索你想要贡献的应用对应的模糊名称, 以此来降低应用维护重叠的风险
譬如, 你想要在[公共构建平台](https://github.com/linglongdev)上认领一款名为 `Converseen` 的应用, 预期使用 `io.github.Converseen` 的应用id.
那么你可以在搜索处搜索 `Converseen` `io.github.Converseen` `converseen` 等大小写交换的关键词来查看是否已有同名仓库存在

2. 确认不存在已被认领的应用后, 就可以开始申领应用的流程了, 在这里表现为在[公共构建平台](https://github.com/linglongdev)组织中申请一个仓库
参考[公共构建平台 仓库管理指导](https://github.com/linglongdev/Repository-Manager) 通过提交 `Pull requests` 来启动仓库申请流程.
流程合并后, 我们将会在[公共构建平台](https://github.com/linglongdev)的仓库列表中找到我们申请的应用专有仓库,这意味着我们从此刻起已经成为该应用的常态维护者了

3. 访问该仓库并将其fork至用户个人仓库下

4. 我们将fork后的仓库通过 `git clone` 同步到本地目录中, 提交该应用对应的玲珑应用构建工程配置文件 `linglong.yaml`

5. 保存要提交的文件后, 依次通过 `git add` `git commit` `git push`操作将文件推送至源仓库

6. 此时进入fork后的仓库可以看到存在与上游的commits差异,点击contribute即可通过 `Pull requests` 来将刚刚提及的文件推送至仓库

7. 当`Pull requests`发起后, 将会触发[公共构建平台](https://github.com/linglongdev)的构建流程
\* 仅有仓库中 `linglong.yaml` 的版本号(version)发生变化时, 才会触发构建流程

8. 构建成功后, 自动化流程cicd将会返回兼容性自动测试的程序运行截图

9. 当本次构建的应用通过兼容性测试后, 本次 `Pull requests` 将会被管理员合并. 合并后, 本次应用的构建将会被推送到应用仓库中提供下载,
\* 对于已合并的提交, 可在 `Release` 页面下载到历史提交版本的安装文件 `binary.layer`.

### 开发者平台
若你决定通过[统信开发者应用分发平台](https://www.chinauos.com/partner/distribute)进行玲珑生态的贡献, 在此之前你应当持有一个已经通过个人开发者认证的账户
若未完成个人开发者身份认证, 可以进入[开发者中心](https://identity.chinauos.com/main/index)进行认证

1. 在认证个人开发者身份后, 进入[应用分发平台](https://appstore-dev.uniontech.com/#/index), 添加活动期间产出的 `binary.layer` 安装文件
2. 进入软件包管理页面,点击 `添加新应用`
3. 选择 `玲珑包` ,点击 `上传`, 选择`binary.layer` 安装文件
\* 每次上传一款新应用时, 仅支持上传同一玲珑应用id的文件, 若需要新增提交数个应用, 则请在提交本应用后再次添加
4. 目前玲珑应用支持 `deepin 23`,包上传完成后使用 `版本管理` 设置分发的系统版本
5. 根据实际情况依次设置`应用分类`、`应用展示素材`、`截图`、`图标`、`开发者名称`等
\* 若应用选择上架至中国(含港澳台)以外的地区,请确保满足该应用的分发限制
