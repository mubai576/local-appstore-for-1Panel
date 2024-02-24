# Gitea Actions
从Gitea 1.19版本开始，Gitea Actions成为了内置的CI/CD解决方案。

## 名称
Gitea Actions与GitHub Actions相似且兼容，它的名称也受到了它的启发。 为了避免混淆，在这里我们明确了拼写方式：
* "Gitea Actions"（两个单词都大写且带有"s"）是Gitea功能的名称。
* "GitHub Actions"是GitHub功能的名称。
* "Actions"根据上下文的不同可以指代以上任意一个。在本文档中指代的是"Gitea Actions"。
* "action"或"actions"指代一些要使用的脚本/插件，比如"actions/checkout@v3"或"actions/cache@v3"。

## Runner
和其他CI/CD解决方案一样，Gitea不会自己运行Job，而是将Job委托给Runner。 Gitea Actions的Runner被称为act runner，它是一个独立的程序，也是用Go语言编写的。 它是基于nektos/act的一个分支 。

由于Runner是独立部署的，可能存在潜在的安全问题。 为了避免这些问题，请遵循两个简单的规则：
* 不要为你的仓库、组织或实例使用你不信任的Runner。
* 不要为你不信任的仓库、组织或实例提供Runner。

对于内部使用的Gitea实例，比如企业或个人使用的实例，这两个规则不是问题，它们自然而然就是如此。 然而，对于公共的Gitea实例，比如gitea.com，在添加或使用Runner时应当牢记这两个规则。

## 状态
Gitea Actions仍然在开发中，因此可能存在一些错误和缺失的功能。 并且在稳定版本（v1.20或更高版本）之前可能会进行一些重大的更改。

如果情况发生变化，我们将在此处进行更新。 因此，请在其他地方找到过时文章时参考此处的内容。

## 配置
配置文件位于安装后的 config/config.yml 中。 

`container.network` 需要修改为 gitea-runner 对应的 docker 网络，否则会导致缓存服务无法连接
`runner.capacity` 为 gitea-runner 可并发执行的任务数量，视服务器配置修改，过高的并发数可能导致服务崩溃

请参考[配置文档](https://docs.gitea.io/en-us/config-cheat-sheet/)获取更多信息。