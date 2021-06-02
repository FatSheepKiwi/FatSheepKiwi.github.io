# Jekyll

当我萌生搞个个人博客的时候，其实我对一些生成静态网站的框架就已经有所了解。Hexo，Hugo，Wordpress 等都是现成的选择，都有着很不错的社区和主题支持，常见问题也可以很快的找到资料解决。最后选择了 Jekyll，是看中了它是与 Github Page 功能结合的最好的，有免费稳定的托管平台，何乐而不为呢？随之而来的就是新的问题了，我对 Jekyll 不熟啊（虽然其他的框架也是白纸一张），它的工作原理是怎样的呢？选择个人博客很重要的一点就是可以自己定制功能，玩不转的话就没意义了。So time to learn Sth new。

## Liquid

Jekyll 使用了 [Liquid](https://liquid.bootcss.com/) 模板语言来生成网站，它提供了简单的语法来进行逻辑控制，并且内置了丰富的 filter 函数，帮助简化了编码过程。

## 分页功能

当文章越来越多的时候，就会有分页显示文章列表的需求。Jekyll 已经自建分页功能。

在Jekyll 3中，需要在`gems`中安装`jekyll-paginate`插件，并添加到你的`Gemfile`和`_config.yml`中。在 Jekyll 2 中，分页是标准功能。
