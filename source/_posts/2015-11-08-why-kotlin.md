title: '[译] 为什么 Kotlin 是我下一门要使用的语言'
date: 2015-11-08 20:49:11
tags:
- Kotlin
- Android
- Java
- JVM
categories:
- 编程
----------

{% asset_img index-page-header-bg.jpg 坐落于俄罗斯岛屿 —— Kotlin 上的灯塔 %}

作者            | 原文
----------------|------------------------------------------------
[Mike Hearn][1] | [Why Kotlin is my next programming language][2]

[Kotlin](http://kotlinlang.org/) 是一门新的编程语言，它来自 [JetBrains](http://jetbrains.com/) —— 世界上最伟大 IDE 的开发商。在做了许多研究后，我决定将 Kotlin 作为我未来 5 到 10 年的主力编程开发语言。

我十分喜爱 Kotlin，它将会是一个很成功的项目。人们看到我在开源项目中使用了该语言后让我介绍一下它，所以在本文中我将说明为什么 Kotlin 是优秀的，讨论一些使用中可能会遇到的问题，

*注意：Kotlin 目前处于 beta 阶段，有望于 2015 年底发布 1.0 正式版并且提供稳定的标准库。*

<!--more-->

### 为什么说 Kotlin 是优秀的

本文不会像一般介绍语言的文章那样，一开头就罗列出语言那些酷炫的特性，我们稍后再来探讨这些内容。

首先我将介绍一些其它的信息，因为 [2013 年一项研究](http://sns.cs.princeton.edu/docs/asr-oopsla13.pdf)显示，当开发者评估一种编程语言时生态系统要比语言特性更重要。这符合我个人的经验，下面就让我开始介绍吧：

**Kotlin 被编译成 JVM 字节码或者 JavaScript 代码**。Java 开发者将会是对它最感兴趣的人，不过对于使用垃圾收集运行时语言的开发者而言它也具有一定的吸引力，比如 Scala、Go、Python、Ruby 和 JavaScript 等语言。

**Kotlin 来自业界**，而不是学术界。它解决了开发者现今面临的实际问题。例如它的类型系统可以帮助你避免空指针异常。

**切换到 Kotlin 无需成本！** 它是开源的但这不是重点，重点是它提供了一个高质量的一键从 Java 转换到 Kotlin 的工具，并且十分关注 Java 二进制文件的兼容性。你可以将现有 Java 项目的一次性转换成 Kotlin 项目，而该项目仍将可以正常编译，即使这是一个包含上百万行代码的复杂程序。

显然你可以从上文得知，**Kotlin 程序能够使用所有现存的 Java 框架和库**，甚至那些依赖注解处理的高级框架。它们之间的交互是无缝的，不需要包装或者适配层。Kotlin 可以整合 Maven，Gradle 以及其它构建系统。

它十分平易近人，语法精炼直观，仅仅是阅读语言参考文档**几个小时就能学会使用**。Kotlin 看起来十分像 Scala 但是更加简洁并且兼顾了可读性。

**它不遵循特定的编程哲学**，例如极度的函数式编程或者面向对象编程风格。

它**不会增加运行时的开销**。Kotlin 的标准库十分小巧紧凑：专注于扩展 Java 标准库，编译阶段的大量内联操作意味像 map/filter/reduce 等管道结构函数将被编译成类似于命令式语言的代码。

[Anko](https://github.com/JetBrains/anko) 与 [Kovenant](http://kovenant.komponents.nl/android/features/) 等框架的出现意味着**在 Android 开发者中 Kotlin 开始变得流行起来**。如果你正在从事 Android 相关的工作，相信你很快就会获得好的工作。你可以阅读这份 [Square 公司开发者 JakeWharton 的报告](https://docs.google.com/document/d/1ReS3ep-hjxWA8kZi0YqDbEhCqTt29hG8P44aA9W0DM8/edit?hl=en&forcehl=1)，了解用 Kotlin 进行 Android 开发的体验。

Kotlin 允许你继续使用你的工作效率提升工具。**IntelliJ 的 IDE 对 Kotlin 的支持十分完善**：你可以对代码进行重构、搜索、导航以及使用自动完成，而且 IDE 充分支持调试、单元测试、性能分析等等功能。

除了 Android，我认为 **Kotlin 还非常适用于企业中 Java 的应用场景** 。如果你的工作是整天埋头于大公司的代码库中，那么当 Kotlin 1.0 版本正式发布时你应该尽快去了解一下：
-	**由知名公司为它提供强大的商业支持**。 JetBrains 这家公司 有一个高度称职的大团队致力于该项目，有稳定的商业模式甚至在自己的部分旗舰产品中使用 Kotlin，这表明短期内 Kotlin 不会被放弃。
-	**使用 Kotlin 风险较低**：可以由一两个感兴趣的团队成员在项目中小范围的试验 Kotlin，这并不会扰乱你的项目，因为 Kotlin 的类对外提供的 Java API 看起来就与普通的 Java 代码一样。
-	因为 Kotlin 十分注重语法的可读性，**代码审查不会成为问题**，对 Kotlin 不熟悉的团队成员仍然能够完成该工作。
-	**Kotlin 基于 Java 6**，所以假如你难以在项目中升级使用新版本的 JVM，你可以使用 Kotlin。

今年早些时候我向 Swiss Re 这家瑞士再保险公司的团队（他们使用 Java 和 .NET）展示了 Kotlin。首先我定义了一个简单的 Java 类包含一些字段以及 toString、equals、hashCode 等方法，大概有 50 行代码。然后我将它转换成 Kotlin 代码（大部分是自动完成的），结果仅剩 1 行代码，接着我还演示了其它节省时间的特性。他们看过后对 Kotlin 充满了热情并且认为 Kotlin 是它们项目中 C# 语言的一个潜在竞争对手。

我认为 Kotlin 正中企业 Java 开发者的红心，所以尽管 Kotlin 是免费的，JetBrains 还是能够通过它增加商业版本 IDE 的销售来赚大钱。这将激励他们根据用户的意愿持续改进它。

与此相比，对于那些由不相关产品资助的语言开发者来说，当用户需求与之前的设计理念冲突时，他们很少会因此作出调整。

---

### 特性

Kotlin 作为一门新的编程语言能够脱颖而出，是因为它关注生态系统：JetBrains 懂得生产力的高低更多的取决于生态系统而不是便捷的语法。

尽快如此，Kotlin 还是有许多有用的特性能让你编码的过程变得愉快：

-	我们已经提过 [**null 安全**](http://kotlinlang.org/docs/reference/null-safety.html)（可选），它能够让编译器系统的标记潜在的空指针引用。与一些语言不同的是它不涉及 option 类，因此是零开销的，并且还有其它语言特性确保它不会造成不便。
-	**精炼的语法**：无处不在的类型推断、简单的函数只需要一行、简单的结构以及 JavaBeans 也只需要一行就能声明、[**真正的属性**](http://kotlinlang.org/docs/reference/properties.html)——可以在背后自动生成 getFoo/setFoo 方法用于与 Java 进行交互、函数可以独立存在于类之外。
-	**异常均为非检查型**。（译者注：感兴趣的可以阅读一下 [Java 理论与实践: 关于异常的争论](https://www.ibm.com/developerworks/cn/java/j-jtp05254/)）
-	使用 [data class](http://kotlinlang.org/docs/reference/data-classes.html) 关键字创建数据类会**自动生成通用方法**，例如 equals、hashCode、toString 以及 copy 和 componentN（[同时声明多个变量时会调用该方法](http://kotlinlang.org/docs/reference/multi-declarations.html)）。这将帮助你在不使用构建器的情况下便捷的获得不变类（immutable classes）。
-	但如果你需要构造复杂的结构体，借助[类型安全的构建器](http://kotlinlang.org/docs/reference/type-safe-builders.html)这个特性可以简洁的实现。如果你使用 Google Protocol Buffers 来存储结构化数据， 通过 [KBuilders](http://levelmoney.github.io/kbuilders/) 这个库也能很轻易做到。
-	**支持函数式编程**以及[零开销的 lambda 表达式](http://kotlinlang.org/docs/reference/lambdas.html)，能够在 Java 的集合中做 Map、Filter、Folder 等处理。Kotlin 的类型系统能够自动识别可变或者不可变的集合。
-	[**扩展函数**](http://kotlinlang.org/docs/reference/extensions.html)特性能够让你在不改动源码的情况下为类添加方法。乍眼一看以为是为了避免写出像 FooUtils 这种风格工具类的语法糖，不过随着使用的加深，你会认识到它不仅能帮你更加容易的通过自动完成使用方法，还能协助你集成现有的 Java API 以及借助其它 Kotlin 特性构建功能强大的扩展。
-	支持[**运算符重载**](http://kotlinlang.org/docs/reference/operator-overloading.html)，但是不会像 Scala 或者 Perl 那样出现难以理解的代码。运算符被映射成相应名字的方法，通过重写这些方法改变运算符的行为（包括函数调用），但是不能定义新的运算符。这使得程序能够兼顾功能与可读性。
-	Kotlin 没有宏或者其它的方式来重定义语言，但是通过这些精心设计的特性能够使第三方库自由的对它进行扩展，官方对集合类进行的扩展也只是小试牛刀而已，请看以下例子。
-	想使用 **fibers、actors 和 Go 风格的 channels**？一个名为 [Quasar](http://blog.paralleluniverse.co/2015/06/04/quasar-kotlin/) 的库已经为你实现了。
-	[**使用 Markdown 替代 HTML**](http://kotlinlang.org/docs/reference/kotlin-doc.html) 来编写 API 文档，这样编写 JavaDocs 可比以前舒适多了。（译者注：JetBrains 提供了相应的文档生成器 [Dokka]( http://github.com/kotlin/dokka)）
-	更好用的[**泛型**](http://kotlinlang.org/docs/reference/generics.html)。如果你没有完全掌握泛型参数中 super 以及 extends 的含义，别担心，这不是你的错。Java 的泛型的确令人费解，Kotlin 解决了这个问题。
-	[**委托**](http://kotlinlang.org/docs/reference/delegation.html)是一个大家都知道的设计模式，Kotlin 原生支持它。
-	[**== 运算符**](http://kotlinlang.org/docs/reference/equality.html) 的行为符合预期（译者注：简单来说 a == b 相当于 a.equals(b)；新增了 === 运算符，用来判断运算符两边是否指向同一个对象）
-	想快速便捷的进行[**异步编程**](http://kovenant.komponents.nl/)吗？当然！
-	**[字符串插值](https://kotlinlang.org/docs/reference/basic-types.html#string-templates)** "可以使用这样的写法在字符创中直接引用变量{this.example}"
-	函数中的参数可以指定默认值、使用可变长度以及通过参数名传参。
-	还有许多的调整与优化。假如 Java 中有某些让你觉得困扰的问题，我相信 Kotlin 一定已经把它处理好了。

---

### 现在就来试用一下！

跟很多现代编程语言一样，Kotlin 可以通过网页浏览器来进行体验。不过跟其他语言不一样的是，Kotlin 的实验网站提供了一个成熟的 IDE，包括响应很快的自动完成，实时的后台编译，甚至还有在线的静态分析！
#### [**在线试用一下吧**](http://try.kotlinlang.org/#)
好了，让我们继续接下来的内容

---

### 目前存在哪些问题？

生活中没有什么是完美的，包括 Kotlin。以下是我尝试这门语言时遇到的一些问题。

最大的问题是不够成熟，因为 Kotlin 目前还处于 Beta 阶段，这意味着：

-	[每更新一个版本，语法、ABI 以及标准库就变一次](http://blog.jetbrains.com/kotlin/2015/06/kotlin-evolves-how-to-keep-your-code-up/)。好消息是这些变化通常比较微小，可以借助 IntelliJ IDE 来自动升级你的代码，所以这个过程并不会太麻烦。
-	Java-to-Kotlin 的转换工具（J2K）还没有完成。它偶尔会大规模的破坏和默默地擦除 Java 8 中的 Lambdas（*修改：2015 年 10 月：M13 版本的转换工具已经可以正确地处理 Java 8 的特性了*）。由它转换而成的代码并不总是最好的写法，但是 JetBrains 为这个工具付出了大量努力，它已经是我用过的语言转换工具中最好的了。所以我并不太担心这个问题，这个转换器正在迅速的改进中，变得越来越成熟。
-	你**会**遇到编译器错误。尽管我的程序并不大，但还是会发生无法编译的情况，甚至错误的编译结果。诊断这些问题并不难，但终归还是影响了开发的体验。
-	你**会**遇到 IDE 内部错误。当这个错误发生时，IntelliJ IDE 会弹出一个悬浮窗口，附带向 JetBrains 报告的选项。大部分错误无需理会，不过依然会使人厌烦。
-	偶尔会出现无法加载提示文档的错误（*修改：M14 版本发布后，这个问题已被修复*）

目前 JetBrains 正致力于完善发布 1.0 版本而不是添加新的功能，期待这些问题能够得到修复。

第二个我遇到的比较大的问题是，有时与 Java 的交互会受到局限。

一个典型的 Bug 是 Java 的类型系统无法防止你改变 Map 中 Key 的类型。按理来说，这样操作应该导致编译器报错，例如使用类型错误的 Key 删除元素。有些 JDK 中的集合使用了泛型，它们某些重要方法的泛型参数是 Obejct，所以编译器不会提示。当在 IntelliJ IDE 中编写 Java 代码时会有静态分析的警告，但是目前 Kotlin 环境还没有这个功能。因为 Kotlin 使用的是 Java 的集合框架没有自己实现，所以这导致了一些类型安全方面的问题，我已经遇到好几次了。
（*修改：1.0 Beta 版本中这个问题已经解决了，Java 中集合框架的类型安全缺陷在 Kotlin 已经不复存在。哟呵！*）

另一个例子是，当调用或使用 Java 代码时 Kotlin 的 Null 安全特性无法发挥作用（可以借助注解弥补）。作为 Kotlin 的初学者，刚开始你可能会写许多调用 Java 库的代码，但是因为以上的问题它们并没有你想象中那么好用。这种情况的改善只能等待 Kotlin 使用人数的增长。[JetBrains 一直在尝试使 Null 安全特性能体现在 Java 交互中](http://blog.jetbrains.com/kotlin/2015/04/upcoming-change-more-null-safety-for-java/)，这种想法是好的，但有时考虑并太周全。（*修改: 从 M13 版本开始，在 Java 代码中将自动以 @NotNull @Nullable 等注解实现 Kotlin 的 Null 安全特性*）

虽然有以上的问题存在，但同时也使得我们能更流畅的使用 Java API，我觉得这种权衡是值得的，只是在开发中要注意。

其它需要考虑的问题:

-	Kotlin 的社区还比较小。虽然目前没有多少 Kotlin 的库可以使用，但是凭借优秀的 Java 交互能力，Kotlin 可以使用现有成熟的 Java 库。
-	如果你喜欢看书来学习，那么你需要等到今年晚些时候才能看到 Kotlin 开发者写的书（译者注：[Kotlin in Action](https://manning.com/books/kotlin-in-action)）
-	纯粹的函数编程风格开发者可能会觉得类型系统中缺乏一些 Scala 或 Haskell 拥有的高级功能。如果你对类型系统一些功能比较看重，那么 Kotlin 可能不适合你。
-	Kotlin 还能编译成 Javascript 代码，但是比较少用，所以可能会遇到更多的问题，这是我从论坛中得到的印象。（*修改: 目前 Kotlin 的开发重心在于完成 1.0 版本并使其稳定运行在 JVM 中，Javascript 方面的问题将会在 1.0 发布后着手解决*）
-	没有标准的编程风格指南，目前 Kotlin 提供了多种语法可供选择。不同人写出来的 Kotlin 代码很可能完全不一样。这与 Go 严格的风格形成了鲜明的对比。（*修改: Kotlin 1.0 版本开始，一些灵活的语法已经被移除了，例如现在重载运算符以及定义中缀函数时必须分别使用 operator 和  infix 关键字进行标记*）
-	Kotlin 的编译速度稍稍慢于 Java，以及 IntelliJ IDE 的智能提示反应有点缓慢，不算严重而且比 Scala 快多了。（*修改：Kotlin 1.0 开始编译速度有了明显提升*）
-	Kotlin 有一个 Eclipse 插件，但是很明显没有 IntelliJ 的好用。
-	Kotlin 在某些方面比 Java 要严格。它不会自动将 Int 转换为 Long 类型，需要开发者显示的转换。这是因为 Kotlin 关注正确性和试图解决《Java Puzzlers》一书中提出的问题。JetBrains 声称他们已经搞定一半了。
-	Kotlin 基于 Java 6，因此会受到它的局限。Kotlin 与 C# 在很多领域都很相似甚至比 C# 做得更好，但是它缺少一些功能，例如 Java 平台尚未支持的值类型。

---

### 为什么应该开始考虑使用 JVM
最近一段时间我遇到了很多使用动态脚本语言（JavaScript 或者 Go —— 译者注：Go 应该是静态编译型语言）的创业公司。
我在 Bitcoin Space 工作的时候，使用动态语言是非常痛苦的事情。在这些语言里没有安全性的类型，这已经导致了[巨大的货币损失](https://medium.com/@octskyward/type-safety-and-rngs-40e3ec71ab3a)。Go 比较少出错，但是在基础层面上给人的体验依然很差，比如说缺少好的调试工具，快速 GC 机制，稳健的管理器以及可靠的分析工具。
过去 15 年或者更长时间里，Java 变得越来越健壮，越来越冗长，甚至有过度设计的迹象，这些变化很大程度上源于它的声誉。企业级 Java 类的名字 [PathVariableMapMethodArgumentResolver](http://docs.spring.io/autorepo/docs/spring/3.2.3.RELEASE/javadoc-api/org/springframework/web/servlet/mvc/method/annotation/PathVariableMapMethodArgumentResolver.html) 就是例证。在很长一段时间里我没有考虑 JVM，我确信这种环境并不适合我。

最终我因为 Android 被迫回到 Java，发现 Java 的开发环境已经改变了。虽然 XML 仍然不合时宜的频繁出现在各种场合，但是一些基础功能十分完善，令人印象深刻。 IntelliJ 是比 Eclipse 更快并且更智能的 IDE。Maven 一出现就得到了迅速的发展，拥有许多原本我想要其它构建/依赖系统增加的功能。较新的 Web 框架像 Ninja 和 Play 从类似 Ruby on Rails 的框架中学到了轻量简洁。有大量的库可供使用。硬件性能变得更高以及 JVM 变得更有效率，等等转变。

没有真正改变的是语言本身，Java 代码写起来依然是令人不快的冗长。

现在有了 Kotlin，完全无需承受离开 Java 现有的生态系统的疼苦。你可以编写更富有表现力的代码，但是却比脚本语言更简洁，同时拥有更好的性能和更少的错误。

如果你喜欢 JavaScript，可以尝试 Kotlin 的 JS 后端，或者在 [Nashorn JS](http://winterbe.com/posts/2014/04/05/java8-nashorn-tutorial/) 引擎里运行你现有的代码。

最后，如果你喜欢 Go 语言是因为它可以编译独立运行的程序，那么试试 javapackager 工具。Kotlin 在本地为每个平台创建了捆绑包，这意味着在 linux 上不需要 JRE 的依赖就可以独立自主的获取 DEBs（linux 的安装包）或者压缩包。当然，它拆包之后不是单个文件而是单个目录，从部署的角度来看并不难操作。

简而言之：如果你之前因为看 Java 不顺眼而忽略了 JVM 的生态系统，那么你应该借着 Kotlin 这门新语言进入这个世界瞧瞧。

### 译文更新历史
* 2015 年 11 月 08 日 - 初稿
* 2015 年 12 月 11 日 - 将段落 “[目前存在哪些问题](#目前存在哪些问题？)” 末尾的 value types 翻译改为“值类型”

  [1]: https://medium.com/@octskyward
  [2]: https://medium.com/@octskyward/why-kotlin-is-my-next-programming-language-c25c001e26e3?source=latest---
