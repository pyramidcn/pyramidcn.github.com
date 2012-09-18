---
layout: post
title: Pyramid 介绍
---

## Pyramid 介绍

**框架 VS 库**

一个 *框架* 和一个 *库* 最大的区别在于：库里面的代码被你写的代码 *调用* ，而框架则是 *调用* 你写的代码。
使用一系列的库来创建应用程序通常在刚开始的时候要比使用矿建简单，因为你可以有选择性地放弃一些控制权给不是你写的库代码。
但是当你使用一个框架的时候，你必须放弃绝大部分的控制权交给那些不是你写的代码：整个框架。你不是必须使用一个框架来创建
一个 WEB 应用程序在使用 Python 的情况下。一大批丰富的库都被已经被开发出来。然而在实际应用中，使用框架去创建应用要比
使用一系列的库更加实用，如果这个框架提供的一些列功能都符合你的项目要求。
    
Pyramid 是一个通用、开源的 Python 网络应用程序开发框架。它主要的目的是让 Python 开发者更简单的创建网络应用程序。

Pyramid 倾向以下设计哲学和理念：

**Simplicity** （简单易用）

Pyramid 采用 *“pay only for what you eat”* 这样一个设计理念。即使在你对 Pyramid 有限的了解下，你也可以得到结果。
它不强制你使用任何一个特殊的技术去开发一个应用，我们也一直努力把你需要了解的核心理念保持在一个最小范围内。

**Minimalism** （简明扼要）

Pyramid 努力去解决在网络应用开发过程中最根本的几个问题：URL 到程序代码的映射、模板、安全和静态资源服务。
我们认为这些核心功能几乎是所有网络应用程序中最常见的。

**Documentation** （规范文档）

Pyramid 的简明意味着我们更容易去更新维护一份详尽的文档。我们的目标是任何一个 Pyramid 相关方面都有参考文档。

**Speed** （速度效率）

Pyramid 致力于明显的快速执行常见任务，比如模板渲染和生成一个简单的响应。尽管 *“hardware is cheap”* ，当看到他或者
她自己负责管理许多机器的时候就会发现这种方法（增加硬件）带来的一些限制会很痛苦。

**Reliability** （性能可靠）

Pyramid 一直在谨慎的开发和细致的测试。对于任何和 Pyramid 有关的源代码，我们的座右铭是：*“If it ain’t tested, it’s broke”*

**Openness** （开源的开放）

和 Python 一样， Pyramid 软件采用[宽松的许可协议](http://repoze.org/license.html)。

### <a id="what-makes-pyramid-unique"></a> 是什么让 Pyramid 独一无二

通常，人们不想听到那些工程规则，他们想听到能解决问题的具体事物和方法。那么试想，如今是什么使得一些人想用 Pyramid
而不是其他的一些可行性的 WEB 框架？是什么使得 Pyramid 成为独一无二的呢？

这确实很难回答，因为在众多优秀的选择方案里面你是很难做出错误决定的，特别是在 Python 网络应用开发框架的市场里面。但是
这个答案很合理：你不需要了解很多，就可以用 Pyramid 写出比较简单的应用程序。“什么？”你说，“那不是一个独一无二的特征，
好多其他 WEB 框架都可以做到！”是的，你是对的。但是不同于其他框架系统，你稍微学习更多一点关于 Pyramid 的知识就可以开发出
大型的应用程序。Pyramid 能让你快速开发，伴随你成长；它不会让你退步即使开发一个小应用程序，当应用程序扩大时也不会阻碍你。
“那好，”，你说，“许多其他的 WEB 框架都能让我去开发大应用程序。”确实如此。但是其他的 Python WEB 框架不会让你同时大、小
应用都做。他们看起来形成了两个没有重叠的分类：开发 *“small apps”* 的框架和开发 *“big apps”* 的框架。小框架通常牺牲
了大框架的特色，反之也是如此。

我们认为写小程序用小框架、写大程序用大框架不是一个普遍的观点。你不能真正的把控一个应用程序最终的大小。我们真的不想到时候
用另外一个大框架去重写之前的小应用当它变成大应用的时候。我们相信一分为二的把当前框架分为大框架和小框架是错误的；一个
设计完美的框架应该都能胜任。Pyramid 努力成为这种框架。

为了这个目的，Pyramid 提供一系列的特性，他们结合起来就是 Python WEB 框架里独一无二的。许多其他的框架也都包含其中一些特性
；Pyramid 构建的过程也从那些框架中借鉴许多。但是只有 Pyramid 把他们全部集中应用的，合适的文档记录，使用其中某个功能而
不必知道全部。这些会在下面详谈。

#### <a id="single-file-applications"></a> 单文件应用

你可以写一个 Pyramid 应用，只寄生于一个 Python 文件，而不是像 Python microframework。看懂这些应用程序很容易，因为所有
关于应用程序的信息都集中在一个地方，你可以在不用了解 Python 发行版本和包的情况下去部署它们。Pyramid 不是以一个 
microframework 推向市场的，但是它能像 microframework 那样允许你做几乎所有的事情。

   
    from wsgiref.simple_server import make_server
    from pyramid.config import Configurator
    from pyramid.response import Response

    def hello_world(request):
       return Response('Hello %(name)s!' % request.matchdict)

    if __name__ == '__main__':
       config = Configurator()
       config.add_route('hello', '/hello/{name}')
       config.add_view(hello_world, route_name='hello')
       app = config.make_wsgi_app()
       server = make_server('0.0.0.0', 8080, app)
       server.serve_forever()

参见 *[创建你的第一个 Pyramid 应用](http://docs.pylonsproject.org/projects/pyramid/en/1.3-branch/narr/firstapp.html#firstapp-chapter "创建你的第一个 Pyramid 应用")*

#### <a id="decorator-based-configuration"></a> 基于修饰符的配置

如果你不想来回切换代码文件和框架的配置文件，而是喜欢将配置语句写在对应代码的旁边，那么你可以使用 Pyramid 修饰符来本地化
配置。例如：

    from pyramid.view import view_config
    from pyramid.response import Response

    @view_config(route_name='fred')
    def fred_view(request):
        return Response('fred')

然而，不像其他系统，使用修饰符来配置 Pyramid 并不会使你的应用变得难以扩展、测试或者重用。比如，`view_config`，它实际上并
没有改变它所修饰的方法的输入输出，所以测试是一个*"所见即所得"*的操作；你不需要了解整个框架就可以测试你的代码，尽管无视
修饰符好了。你也可以申明让 Pyramid 忽略掉修饰符，或者全部使用命令语句代替修饰符来增加 views 方法。Pyramid 的修饰符是被动的
而不是主动的：你要使用 scan 来发现并且激活它们。

例如：*[使用 @view_config 修饰符来增加一个 View 配置](http://docs.pylonsproject.org/projects/pyramid/en/1.3-branch/narr/viewconfig.html#mapping-views-using-a-decorator-section "使用 @view_config 修饰符来增加一个 View 配置")*

#### <a id="url-generation"></a> URL 产生机制

Pyramid 可以为资源、路由，以及静态资源产生 URL。它的 URL 生成 API 使用简单而且灵活。如果你使用 Pyramid 多种 API 来生成 URL
，你可以随意的改变配置而不用担心会破坏页面内的链接。

例如：*[生成路由 URL](http://docs.pylonsproject.org/projects/pyramid/en/1.3-branch/narr/urldispatch.html#generating-route-urls "生成路由 URL")*

#### <a id="static-file-serving"></a> 静态文件服务

Pyramid 是非常愿意为静态文件服务的。它不会让你使用一些外部服务器来做这件事。你甚至可以在一个 Pyramid 应用程序中提供不止一组静态文件的服务（例如/static 和 /static2 ）。你也可以有选择性地把文件存放在外部的一台 WEB 服务器上，并且使用 Pyramid 帮助你生成对应文件的 URL ，这样你既可以在开发中使用 Pyramid 的内部静态文件服务，又可以在生成环境中得到一台更快的静态文件服务器而不必做任何代码的改变。

例如：*[静态资源服务](http://docs.pylonsproject.org/projects/pyramid/en/1.3-branch/narr/assets.html#static-assets-section "静态资源服务")*

#### <a id="debug-toolbar"></a> 调试工具栏

当你使用 Pyramid scaffold 构建项目的时候就会激活 Pyramid 的调试工具栏。在浏览器中，工具栏会浮动在应用程序的上面并且允许你获取一些框架的数据比如：路由配置、最后一次执行结果、当前安装包、SQLAlchemy 执行的查询、logging 数据，以及其他的实时信息。当有异常发生的时候，你可以在浏览器中查看调试器的结果来确定导致异常的原因。它是很方便的。

#### <a id="debugging-settings"></a> 调试器配置

Pyramid 允许你设置调试器来把运行时的信息输出到控制台当你觉得程序不按照你预期执行的时候。比如，你可以打开 `debug_notfound` 来输出没有匹配到视图的 URL 。你可以打开 `debug_authorization`，看到输出的信息就知道为何一个视图允许或者拒绝你执行。这些特性在 WTF 的时候都是很有用的。

也可以在一个 Pyramid 环境下执行一些命令来检测系统的配置：`proutes` 来查看所有的路由配置以及是否有应用程序和它们匹配；`pviews` 来查看所有 URL 的视图配置。某些情况下这些命令都能干掉 WTF 。

例如：*[视图授权失败调试](http://docs.pylonsproject.org/projects/pyramid/en/1.3-branch/narr/security.html#debug-authorization-section "视图授权失败调试")* 和 *[Pyramid 命令行](http://docs.pylonsproject.org/projects/pyramid/en/1.3-branch/narr/commandline.html#command-line-chapter "Pyramid 命令行")*



