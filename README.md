<p align="center">
  <img src="./assets/logo.svg" alt="Logo">
</p>

# wechat-article-exporter

![GitHub stars]
![GitHub forks]
![GitHub License]


在线批量导出微信公众号文章，支持阅读量、评论数据的导出，支持内嵌的音视频导出，无需搭建任何环境，可100%还原文章样式，支持私有部署。

交流群(QQ): `991482155`

## 注意

由于公共代理资源有限，因此推荐 **搭建私有代理节点** 服用，私有代理可部署在以下平台：

- [Deno Deploy][Deno Deploy]
- [Cloudflare Workers][Cloudflare Workers]

查看 [搭建私有代理节点](docs/private-proxy.md) 教程。


## :dart: 特性

- [x] 搜索公众号，支持关键字和biz搜索
- [x] 搜索公众号内文章(根据文章标题搜索)
- [x] 导出 html 格式(打包了图片和样式文件，能够保证100%还原文章样式)
- [x] 批量导出 html 格式(zip打包)
- [x] 缓存文章列表数据，减少接口请求次数 (关键字搜索的文章不会进入缓存)
- [x] 支持文章过滤，包括作者、标题、发布时间、原创标识、所属合集等
- [x] 支持合集下载
- [x] 支持内嵌的音视频下载
- [x] 支持图片分享消息
- [x] 支持视频分享消息
- [x] 支持导出评论、阅读量等数据 (需要抓包获取 credentials 信息，[查看操作步骤](docs/credentials.md))
- [ ] 支持订阅机制，根据指定规则自动下载文章


## :hammer: 如何使用

1. 注册一个微信公众号 (已有账号的话跳过)

前往 [微信公众平台] 注册，服务号和订阅号皆可。

2. 二维码扫码登录

进入 [登录页面]，用微信扫描页面上的二维码，然后选择自己的 **公众号** 进行登录。

> 注意，必须选择公众号登录，用小程序登录无法使用。

3. 配置私有代理(推荐)

在设置页面配置私有代理地址，如下所示：

![配置私有代理](assets/config-private-proxy.png)

4. 搜索目标公众号，开始下载文章

通过左上角的公众号切换按钮，搜索自己感兴趣的公众号，如下图所示：

![切换账号]


## :earth_americas: 关于代理节点

数据的下载采用代理池的思路，以便解决跨域、防盗链、加速等一系列问题。

目前公共代理有以下节点:
```
https://wproxy-01.deno.dev
https://wproxy-02.deno.dev
https://wproxy-03.deno.dev
https://wproxy-04.deno.dev
https://wproxy-05.deno.dev
https://wproxy-06.deno.dev
https://wproxy-07.deno.dev
https://wproxy-08.deno.dev
https://wproxy-09.deno.dev
https://wproxy-10.deno.dev
```

> 这些节点全部部署在 Deno Deploy 的免费账户中，每个月有100G的免费额度，超过额度之后需要等到下个周期刷新。
>
> **这些节点仅供测试使用，正式使用请搭建自己的私有节点。**


## 关于导出其他格式
本项目暂不支持导出除`html`格式之外的其他格式，很大一部分原因是样式很难保真。如果需要其他格式，可以自行寻找其他格式转换工具。

> PDF格式可参考: https://github.com/colin4k/wechat-article-dl


## 常见问题
请参考 [faq](docs/faq.md) 文档，如果遇到其他使用问题，欢迎在 Issue 中说明。

## :heart: 感谢

- 感谢 [Deno Deploy]、[Cloudflare Workers] 提供免费托管服务
- 感谢 [WeChat_Article] 项目提供原理思路


## :coffee: 支持

如果你觉得本项目帮助到了你，请给作者一个免费的 Star，感谢你的支持！



## :rocket: 私有部署 (网站)

> [!WARNING]
> ~~由于项目目前还没有进入稳定状态，所以如果进行了私有部署，请随时关注该项目的最新更新，特别是代理部分的变化，后续将会修改使用策略。~~
>
> ~~或者你可以修改`config/index.ts`中的`AVAILABLE_PROXY_LIST`变量，完全使用自己搭建的节点。~~
>
> ~~另外，目前只有部署到 Deno Deploy 的文档，如果需要部署到其他平台，请在 Issue 中说明。~~
>
> 2024.11.14 更新
>
> 推荐使用 **[公共网站](https://wechat-article-exporter.deno.dev/)** + **私有代理节点** 的形式使用。
> 
> 如果你确实需要部署私有网站，可查看下面的部署教程。
> 
> 注意：公众网站(也就是 https://wechat-article-exporter.deno.dev/ )的功能是最全的，后续某些 Pro 版功能只会出现在公共网站中，私有部署不支持。

<details>
<summary><span style="font-size: 16px;font-weight: 500;">部署到 Deno Deploy</span></summary>

1. Fork 该项目

![create a fork][create-a-fork]

2. 点击 [New Project][new-deno-deploy-project] 在 Deno Deploy 上面创建一个项目，选择你刚fork的仓库，如下图所示:

![create deno deploy project][create-deno-deploy-project]

创建之后如下所示:

![deno deploy project result][deno-deploy-project-create-result]

3. 修改github仓库发布配置

启用仓库的 workflows (默认fork的仓库是禁用的):

![enable github workflows][enable-github-workflows]

修改`.github/workflows/deno_deploy.yml`:

![update workflows project][update-workflows-project]

提交:

![commit changes][commit-changes]

4. 等待发布结果

![deploy success][deploy-success]

![finally website][finally-website]
</details>


## 关于后续更新计划

后续会区分出 **免费版** 和 **Pro版**，区别如下:

### 免费版
- 所有现有功能
- 所有现有的代理节点
- 现有功能的bug修复

### Pro版
- 订阅自动下载服务
- 更多专用代理节点

> 目前只是有这个计划，并没有开始实施。对于之前有赞赏行为的用户，可提供优惠政策。


## :bulb: 原理

在公众号后台写文章时支持搜索其他公众号的文章功能，以此来实现抓取指定公众号所有文章的目的。


## :memo: 许可

MIT


## :star: Star 历史

[![Star History Chart]][Star History Chart Link]



<!-- Definitions -->

[deploy-badge]: https://img.shields.io/github/actions/workflow/status/jooooock/wechat-article-exporter/.github%2Fworkflows%2Fdeno_deploy.yml?label=Deploy

[deploy]: https://github.com/jooooock/wechat-article-exporter/actions

[Github stars]: https://img.shields.io/github/stars/jooooock/wechat-article-exporter?style=social&label=Star&style=plastic

[Github forks]: https://img.shields.io/github/forks/jooooock/wechat-article-exporter?style=social&label=Fork&style=plastic

[Github License]: https://img.shields.io/github/license/jooooock/wechat-article-exporter?label=License

[微信公众平台]: https://mp.weixin.qq.com/cgi-bin/registermidpage?action=index&lang=zh_CN

[登录页面]: https://wechat-article-exporter.deno.dev/login

[切换账号]: assets/switch-account.png

[create-a-fork]: assets/deploy/create-fork.png

[new-deno-deploy-project]: https://dash.deno.com/new_project

[create-deno-deploy-project]: assets/deploy/create-deno-deploy-project.png

[deno-deploy-project-create-result]: assets/deploy/deno-deploy-project-result.png

[enable-github-workflows]: assets/deploy/enable-github-workflows.png

[update-workflows-project]: assets/deploy/update-workflows-project.png

[commit-changes]: assets/deploy/commit-changes.png

[deploy-success]: assets/deploy/deploy-success.png

[finally-website]: assets/deploy/finally-website.png

[Deno Deploy]: https://deno.com/deploy

[Cloudflare Workers]: https://workers.cloudflare.com

[Wechat_Article]: https://github.com/1061700625/WeChat_Article

[Star History Chart]: https://api.star-history.com/svg?repos=jooooock/wechat-article-exporter&type=Timeline

[Star History Chart Link]: https://star-history.com/#jooooock/wechat-article-exporter&Timeline
