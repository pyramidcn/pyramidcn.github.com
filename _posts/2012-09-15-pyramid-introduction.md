---
layout: post
title: Pyramid 介绍
---

## Pyramid 介绍

**框架 VS 库**

一个 *框架* 和一个 *库* 最大的区别在于：库里面的代码被你写的代码 *调用* ，而框架则是 *调用* 你写的代码。
使用一系列的库来创建应用程序通常在刚开始的时候要比使用框架简单，因为你可以有选择性地放弃一些控制权给不是你写的库代码。
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

#### <a id="add-ons"></a> 组件

Pyramid拥有一批和 Pyramid 自身核心组建一样高质量的扩展组件。这些组件以 package 的形式提供 Pyramid 核心没有的功能。已经有发邮件、jinja2 模板系统、XML-RPC 或者 JSON-RPC、整合 jQuery Mobile等一些扩展组件包。

例如：*[http://docs.pylonsproject.org/docs/pyramid.html#pyramid-add-on-documentation](http://docs.pylonsproject.org/docs/pyramid.html#pyramid-add-on-documentation)*

#### <a id="class-based-and-function-based-views"></a> 基于类和方法的视图模型

Pyramid 有一个统一、结构化的 **view callable** 概念。View callables 可以是函数、类的方法，或者一个实例。当你增加一个新的 view callable 的时候，你可以选择让它成为一个函数、一个类里面的方法；无论哪种方式，Pyramid 处理的方式大致相同。你可以把代码在函数和类的方法里面来回移动当你改变想法以后。一系列的 view callable 可以作为方法构成一个类，如果你高兴的话还可以让他们共享一些初始化的代码。所有的 views 都很容易理解和使用，操作也都类似。它们没有什么区别，都可以达到你的目的。

这是一个定义成为函数的 view callable：

    from pyramid.response import Response
    from pyramid.view import view_config

    @view_config(route_name='aview')
    def aview(request):
        return Response('one')

这是几个作为类里面的方法定义的 view callable：

    from pyramid.response import Response
    from pyramid.view import view_config

    class AView(object):
        def __init__(self, request):
            self.request = request

        @view_config(route_name='view_one')
        def view_one(self):
            return Response('one')

        @view_config(route_name='view_two')
        def view_two(self):
            return Response('two')

参见：*[@view_config 的位置](http://docs.pylonsproject.org/projects/pyramid/en/1.3-branch/narr/viewconfig.html#view-config-placement "@view_config 的位置")*

#### <a id="asset-specification"></a> 规范资源

规范的资源是一个包含 Python 包名和文件名或者路径的字符串，比如：`MyPackage:static/index.html`。这种规范写法在 Pyramid 中无处不在。资源规范涉及到模板、目录，或者任何一个静态的资源包。这样使得基于 Pyramid 构建的系统扩展性很强，因为你不必依赖全局设置（“静态目录”）或者查找（“给模板目录排序”）来定位你的文件。你可以移动需要的文件，包含其他的一些没有向你共享模板资源或者静态文件的包也不会有冲突。

因为规范资源在 Pyramid 中使用很多，我们也提供一种允许用户覆盖资源的方式。如果你喜欢一个别人用 Pyramid 创建的系统，那么你只需“改变一个模板”就会让它更好。不用 fork 这个应用程序，只需要用你自己的东西替换模板中的规范的资源，你可以开干了。

例如：*[理解 Asset Specification](http://docs.pylonsproject.org/projects/pyramid/en/1.3-branch/narr/assets.html#asset-specifications)* 和 *[ Overriding Assets](http://docs.pylonsproject.org/projects/pyramid/en/1.3-branch/narr/assets.html#overriding-assets-section)*

#### <a id="extensiable-templating"></a> 模板扩展

Pyramid 有一个允许扩展“renderers”的API。像Mako、GEnshi、Chameleon，以及jinja2 这样的模板系统都可以作为renderers（渲染器）。绑定在这些模板系统上的渲染器都已经被使用在 Pyramid 里了。如果你想用其他的，也未尝不可。只需拷贝一个已经存在的 renderer package 代码，然后配置在你喜欢的模板系统里面，那么就像你用 Pyramid 内建的模板系统一样来使用你这个（自己配置的）模板系统。

Pyramid 并不只让你使用单一的模板系统，甚至你可以使用多个模板系统在同一个项目里。

例如：*[马上使用模板](http://docs.pylonsproject.org/projects/pyramid/en/1.3-branch/narr/templates.html#templates-used-directly)*

#### <a id="rendered-views-can-return-dictionaries"></a> 视图渲染器可以返回字典

如果你使用一个 renderer ，你不必从一个 view 里返回“webby”这种 Response 对象，而是用一个 dictionary 代替，Pyramid 会代表你使用模板做好从 dictionary 到 Response 的转换。这会让 view 测试更简单，因为你不必解析 HTML；只需在他返回的 dictionary 中使用一个 assertion 来代替视图返回的“the right stuff”（正确的结果）。你可以写“真正”的单元测试来代替视图的功能测试了。

例如，要取代这个：

    from pyramid.renderers import render_to_response

    def myview(request):
        return render_to_response('myapp:templates/mytemplate.pt', {'a':1}, 
                                    request=request)

你这样写：

    from pyramid.view import view_config

    @view_config(renderer='myapp:templates/mytemplate.pt')
    def myview(request):
        return {'a':1}

当上面的 view 被调用的时候，`{'a': 1}`将会被 render 到 Response 里。上面 `renderer = `传递的参数是一个 asset specification ，形如`packagename:directoryname/filename.ext`。这种情况下，它指向的 mytemplate.pt 这个文件在 myapp 这个包的 templates 目录下。

例如：*[Renderers](http://docs.pylonsproject.org/projects/pyramid/en/1.3-branch/narr/renderers.html#renderers-chapter)*

#### <a id="event-system"></a> 事件系统

Pyramid 释放出 event 在它处理 request 的周期内。你可以监听任意数量的 events 。比如，你可以通过监听 NewRequest 事件来知晓一个新的 request ，监听 BeforeRender 事件而被告知一个模板将被渲染，等等。用一个事件发布系统代替硬编码消息钩子作为框架消息通知功能会使框架系统更健壮。

同样你可以使用 Pyramid 事件系统发送“你自己的”事件。比如，你想创建的系统本身就是一个框架，你想通知订阅者一个文档刚刚被加入到索引，那么你可以创建你自己的事件系统（或许就叫做DocumentIndexed）然后通过 Pyramid 发送这个事件。框架的用户就会像订阅 pyramid 自身的事件一样订阅到你的事件。

例如：*[使用事件](http://docs.pylonsproject.org/projects/pyramid/en/1.3-branch/narr/events.html#events-chapter)* 和 *[事件类型](http://docs.pylonsproject.org/projects/pyramid/en/1.3-branch/api/events.html#event-types)*

#### <a id="built-in-internationalization"></a> 内建国际化

Pyramid 核心特性搭载国际化关系特性：本地化、多元化，创建消息目录从源文件到模板。Pyramid 允许重复的消息目录通过使用 translation domains：你可以创建一个有它自己译文而不和其他语言的译文有冲突的系统。

例如：*[国际化和本地化](http://docs.pylonsproject.org/projects/pyramid/en/1.3-branch/narr/i18n.html#i18n-chapter)*

#### <a id="http-caching"></a> HTTP 缓存

Pyramid 提供一种简单的方式去关联视图和HTTP缓存。你只需加上视图配置语句 `http_cache` 来告诉 Pyramid，那么接下的就交给它来处理了，例如：

    @view_config(http_cache=3600) # 60 minutes
    def myview(request): ....

Pyramid 会增加 `Cache-Control` 和 `Expires` 来响应被调用是生成的视图。

参考 [add_view()](http://docs.pylonsproject.org/projects/pyramid/en/1.3-branch/api/config.html#pyramid.config.Configurator.add_view) 方法的 http_cache 文档介绍。

#### <a id="sessions"></a> Session 会话

Pyramid 有内建的 HTTP session ，这使得你能够把数据和匿名用户的请求关联起来，许多框架系统都会做这个。但是 Pyramid 还会允许你按照文档接口创建代码去配置你自己的 session system 。目前存在的有一个绑定包支持第三方 Beaker sessioning system，如果你有特殊的需求（或许你想要把 session 存储在 mongodb 里面），这也是可以的。你可以来回切换（session 存储的方式）而不用改变应用的代码。

参考：*[Sessions](http://docs.pylonsproject.org/projects/pyramid/en/1.3-branch/narr/sessions.html#sessions-chapter)*

#### <a id="speed"></a> 速度

Pyramid 的核心，据我们所知，至少比 python 其他 WEB framework 要快一点。它是为了速度而精心设计的，它只会尽可能地做必须的工作当你让它去干活的时候。外部函数调用和次优的算法在其核心 codepaths 中都被避免，从一个简单的 pyramid view 上每秒3500至4000次请求，在一个普通的双核笔记本电脑上并且配上一个合适的WSGI server（mod_wsgi或者gunicore）是OK的。任何情况下，没有需求和目标下的性能数据基本上都是没用的，但是如果你追求速度，Pyramid 将永远不会是你的瓶颈，至少不会超过 python 的瓶颈。

参考：*[http://blog.curiasolutions.com/the-great-web-framework-shootout/](http://blog.curiasolutions.com/the-great-web-framework-shootout/)*

#### <a id="exception-views"></a> 异常视图

异常发生，Pyramid 允许你注册一个异常视图，并不是以特别的方式把他们呈现给线上的用户。异常视图和正常视图一样的，但他们只在 Pyramid 自身有异常“抛出”的时候才被调用。例如，你可以为异常注册一个能够捕捉到所有异常的视图，然后呈现一个“well, this is embarrassing”页面；或者你只为特定类型的 application-specific 异常注册异常视图，比如一个找不到指定文件的异常或者因为用户没有权限而不能执行一个操作的异常。前一种情况下，你可以呈现一个漂亮的“Not Found”页面；后一种情况你可以显示一个登陆框。

参考：*[客户端异常视图](http://docs.pylonsproject.org/projects/pyramid/en/1.3-branch/narr/views.html#exception-views)*

#### <a id="no-singletons"></a> No singletons

Pyramid 是按照这种方式写的：它要求你的应用没有任何的“singletons”数据结构。换句话说，Pyramid 不需要你构建任何“mutable globals”，或者另一种说法，导入一个 Pyramid 应用的时候不会有任何“导入时的副作用”。如果你曾尝试处理一个 Django “settings.py”文件去做同一个应用的多次安装，或者你需要给框架做一些补丁以满足实际情况的需求，再或者你想用 asynchronous server 部署你的系统，那么这（no singletons）是一个好消息，你最终也会越来越欣赏这个特性。它不是个难题，你可以在一个python 进程中运行多个配置不相同的类似pyramid 应用程序，这是有利于主机空间共享的。（感觉这翻译的不是太好！）

#### <a id="view-predicates-and-many-views-per-route"></a> 视图谓词以及多个视图对应一个路由

不像其他系统，Pyramid 允许你一个 route 关联多个 view 。例如，你可以创建一个 `/items` 模式的 route ，当这个 route 被匹配到的时候，你可以把 request 传给一个 view 如果 request 的方式是 GET ，或者给另一个 view 如果 request 的方式是 POST ，等等。一个被称为“view predicates”的系统会允许这样做。请求方式匹配是非常重要且基本的方式，你可以以此做一个 view predicate。你也可以用其他 request 参数比如查询字符串中的元素、Accept Header等许多东西来关联匹配一个视图，无论 request 是 XHR （XML Http Request）与否。这个特性会让你的视图保持“clean”，他们不需要很多的逻辑条件，因此也很容易测试。

参考：*[视图配置参数](http://docs.pylonsproject.org/projects/pyramid/en/1.3-branch/narr/viewconfig.html#view-configuration-parameters)*

#### <a id="transaction-management"></a> 事务管理

Pyramid 的 scaffold 系统呈现的项目包含一个事务管理系统，从 Zope 借鉴而来。当你使用这个事务管理系统的时候，你就不再负责提交数据了，而由 Pyramid 来处理commit：它在 request 结束的时候 commit，或者终止于异常。为什么这是一件好事情？集中事务管理是一个好事情。如果集中管理事务，你散置 session.commit 当被应用程序逻辑本身调用的时候，然后在一个糟糕的地方结束。无论你在哪儿手动向数据库提交数据，其他一些代码很可能在提交之后运行，如果这些代码要去做其他重要的事情，一旦不小心出错就会导致程序停止之后得到的数据不一致，一些不需要入库的数据可能会被写入数据库。用集中提交就会帮你从上面的问题中解脱出来，这对于那些关心数据完整性的懒人来说简直棒极了。要么请求被成功执行并且多有改变都被提交，否则执行失败的话，所以改变都会终止提交。

同时，Pyramid 的事务管理系统允许你在多个数据库直接同步提交，也可以允许在一个事物的提交下有条件的发送邮件，但是其他都保持安静。

参考：*[SQLAlchemy + URL Dispatch Wiki Tutorial](http://docs.pylonsproject.org/projects/pyramid/en/1.3-branch/tutorials/wiki2/index.html#bfg-sql-wiki-tutorial)*（注意程序里缺少提交语句的代码）

