title: 用 Alfred Workflow 实现聊天内容快速引用回复
date: 2019-11-17 20:22:01
categories: technology #induction life poetry
tags: [Alfred,Workflow,引用消息,引用回复]  # <!--more-->
reward: true

---

### 1、前言
在微信 Mac/PC 端消息有个「引用消息」的功能，用于针对某个特定消息回复，而其它 App 没有该功能，或者有，比如 QQ / Telegram 都有实现回复（reply）功能，但是都是针对一条消息回复，如果需要对多条消息统一做回复，自带的功能也许真不够自定义的好。当然，最主要是我司现在用的 `企业QQ for macOS` 版本不支持这个功能，于是就想到自己做一个 workflow 可以读取当前复制的内容，然后生成一个带引用格式的文本，并完成后粘贴到 App，从而实现引用回复~

传送门下载：[Reply Message v1.0.alfredworkflow](https://github.com/iHTCboy/macOSConfig/raw/master/Alfred/Workflows/Reply%20Message%20v1.0.alfredworkflow)

<!--more-->

### 2、已实现的效果
目前已经实现了几个功能：

![Alfred-Reply-Message-alfredworkflow.png](https://github.com/iHTCboy/iGallery/raw/master/BlogImages/2019/11/Alfred-Reply-Message-alfredworkflow.png)

1. `自动模板`：复制内容，打开 Alfred 输入 `R` 键后回车，就会自动粘贴到聊天软件中
![Alfred-Copy-Template.png](https://github.com/iHTCboy/iGallery/raw/master/BlogImages/2019/11/Alfred-Copy-Template.png)

2. `回复内容`：复制内容，打开 Alfred 输入 `R` 键，空格后输入要回复的内容，完成后回车就会自动粘贴到聊天软件中
![Alfred-Copy-Template-Reply.png](https://github.com/iHTCboy/iGallery/raw/master/BlogImages/2019/11/Alfred-Copy-Template-Reply.png)

3. `快捷符模板`：复制内容后，在聊天软件中输入 `\\rp`，会自动粘贴回复的模板到聊天框
![Alfred-Shortcuts-Key.gif](https://github.com/iHTCboy/iGallery/raw/master/BlogImages/2019/11/Alfred-Shortcuts-Key.gif)

4. `自定义快捷键`：如果觉得还不够快？可以自定义一个自己喜欢的快捷键，快速生成回复模板
这个就不演示了，自己配置快捷键就可以啊

注意说明：
1、以上说的快捷键，大家都可以自己定义，不是固定的啊。
2、快捷符模板需要开启 Alfred 监听键盘权限：
![Alfred-Automatically-expand-snippets.png](https://github.com/iHTCboy/iGallery/raw/master/BlogImages/2019/11/Alfred-Automatically-expand-snippets.png)
3、本次使用到 Alfred 相关的功能试用版不支持，需要付费的正版才支持，或者使用xx版本。当然对于有条件的朋友建议购买正版，这也是一个提高效率的方式~


下载地址：[Reply Message v1.0.alfredworkflow](https://github.com/iHTCboy/macOSConfig/raw/master/Alfred/Workflows/Reply%20Message%20v1.0.alfredworkflow)

### 3、背后的简单原理

其实，原理非常的简单，就是二行代码的事：

```
clipboardtext=`pbpaste`

echo -e -n "「 ${clipboardtext} 」\n- - - - - - - - - - - - - - -\n\n：{query}"
```

就是用 shell 的 macOS 命令 `pbpaste` 获取剪切版的内容，然后拼接生成需要的格式，最后内容通过 `{query}` 传递给 Alfred。至于前期的快捷键、键盘监听，后续的推送通知、粘贴内容到输入框，全部是 Alfred 软件全自动封装好的完成，不需要我们用户关心！！！

上面的二行代码很短，但是有很多知识，大家明白了吗？

到这里，是不是感受到 Alfred 功能的强大啦！！！

备注：（`-e` 表示echo命令内容`\n`不转义， `-n`表示 echo 命令后不自动添加换行。）

### 4、总结
2018年写的《程序员的macOS系列》文章，还有一篇《高效Alfred进阶》没有写！！！

- [程序员的macOS系列：精选Mac App](https://ihtcboy.com/2018/07/15/2018-07-15_程序员的macOS系列：精选MacApp/)
- [程序员的macOS系列：Mac开发环境配置](https://ihtcboy.com/2018/09/30/2018-09-30_程序员的macOS系列：Mac开发环境配置/)
- [程序员的macOS系列：高效Alfred进阶](https://ihtcboy.com/2020/02/09/2020-02-09_程序员的macOS系列：高效Alfred进阶/)

2020年，《程序员的macOS系列》三篇已经完成 ✅，后续有想法在更新吧~

所以，相信大家能感受到 Alfred 很强大，用的好，效率是成倍成倍的提高，希望我今年还有时间的话，补一下这个文章吧，当然，最好大家自行也可以搜索一些资料自己学习，制作自己需要的 workflow 提高效率是最棒的！知识的价值是无价，经验更加是无价（当然，我会尽量的全面简单而深入浅出，我认为文章能简单或深入的点到为止，这才是写文章的乐趣，让大多数人都能学习到~），Alfred版本也从3.x升到了4.x，同时最新的 macOS 10.15 也有很多调整，真不幸，现在写总结，生命有效时间也越来越短了，知识保质期短，文章还没有写已经过期了，太难了。好吧，这次先到这里，下回聊，加油~


### 5、参考
- [Alfred神器使用手册 | louis blog](http://louiszhai.github.io/2018/05/31/alfred/)
- [从 0 到 1 写一个 Alfred Workflow - 少数派](https://sspai.com/post/47710)
- [程序员的macOS系列：高效Alfred进阶](https://ihtcboy.com/2020/02/09/2020-02-09_程序员的macOS系列：高效Alfred进阶/)


<br>

- 如有疑问，欢迎在评论区一起讨论！
- 如有不正确的地方，欢迎指导！

<br>
> 注：本文首发于 [iHTCboy's blog](https://iHTCboy.com)，如若转载，请注来源
<br>


