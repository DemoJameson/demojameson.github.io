title: Java 与 Kotlin 中各种 findViewById 的方式
tags: [Kotlin, Java, Android]
categories: 编程
author: DemoJameson
date: 2017-05-22 00:09:00 
updated:  2017-05-22 00:09:00 
---

{% asset_img cover.png %}

# 前言

```java
private Button mButton;
...
mButton = (Button) findViewById(R.id.button);
```

findBiewById 是 Android 开发中必须使用，但是写起来又很无聊的语句，所以逐渐出现了各种代替它的方式，下面让我们看看都有哪些。

<!--more-->

# Java 中的方式

1. 从 [Android Support Library 26.0.0 Beta 1](https://developer.android.google.cn/topic/libraries/support-library/rev-archive.html) 开始 findViewById 将不再需要强转了。
  ```java
  private Button mButton;
  ...
  mButton = findViewById(R.id.button);
  ```

2. 使用注解来注入对应类型的 View，最流行的非 [ButterKnife](https://jakewharton.github.io/butterknife/) 莫属，搭配 [Android Butterknife Zelezny](https://github.com/avast/android-butterknife-zelezny) 插件自动生成以下的代码，不再需要手写 findViewById 了。需要注意的是重构布局时，如果 id 对应的 View 类型发生了变化而又忘记修改代码，则会在运行时产生异常。

  ```java
  @BindView(R.id.button)
  Button mButton;
  ```

3. 使用 [Data Binding Library](https://developer.android.google.cn/topic/libraries/data-binding/index.html) 自动查找所有 View 并缓存到 binding 实例中以供访问。性能超过手写的 findViewById，因为它只遍历了一遍 XML 布局，而 findViewById 每次都会去遍历 XML 布局；include 布局中的 view 也能同样能访问，并且保留结构。
   ```java
   ActivityMainBinding binding = DataBindingUtil.setContentView(this, R.layout.activity_main);
   binding.button.setText("DataBinding 是坠吼的");
   binding.include_layout_id.textView.setText("对对对");
   ```


# Kotlin 中的方式

Java 中的方式 Kotlin 当然也能用了，下面介绍一些 Kotlin 特有的写法。

1. 对应 Java 中的方式 1，并将 View 优化为非空类型。lateinit 关键字代表延迟初始化，假如没有初始化就访问会抛异常。
   ```kotlin
   private lateinit var button:Button
   ...
   button = findViewById(R.id.button)
   ```

2. 改为使用 lazy 代理延迟初始化，使用 val 限制属性不可重新赋值，并做些许封装。这时长得就比较像 Java 中的方式 2 了。
   ```kotlin
   private val button by bindView<Button>(R.id.button)
   // 或者
   private val button:Button by bindView(R.id.button)
   ...
   fun <T : View> Activity.bindView(@IdRes res: Int): Lazy<T> {
       return lazy { findViewById<T>(res) }
   }
   ```

3. 使用 [Kotlin Android Extensions](https://kotlinlang.org/docs/tutorials/android-plugin.html) 直接生成对应的 View 作为属性。不需要 findViewById，不需要定义变量，直接使用。使用时需要注意访问的 View 属于哪个 Layout，因为智能提示的候选项会提供所有布局中的 View 供你选择，然后帮你 import 对应包以便你访问这个 View；假如 import 的多个同一层级的 layout 中具有相同的 id，则这个 id 对应的 View 将无法访问。

  ```kotlin
  import kotlinx.android.synthetic.main.activity_kotlin_main.*
  import kotlinx.android.synthetic.main.activity_kotlin_main.view.*
  ...
  button.setText("Kotlin Android Extensions 我不太喜欢")
  inflateView.textView.setText("因为比较混乱，容易出错")
  ```

# 小结

就目前来说，以上这么多方式我最喜欢的还是使用 Data Binding Library，具有性能强，类型安全，结构化等优点。