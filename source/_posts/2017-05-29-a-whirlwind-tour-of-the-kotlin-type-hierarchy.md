title: 【译】Kotlin 类型层级结构一览
tags: [Kotlin, Java]
categories: 编程
author: DemoJameson
date: 2017-05-29 05:10:00
updated:  2017-05-29 05:10:00
---

{% asset_img entire-hierarchy.png %}

| 作者                                       | 原文                                       |
| ---------------------------------------- | ---------------------------------------- |
| [Nat Pryce](http://natpryce.com/bio.html) | [A Whirlwind Tour of the Kotlin Type Hierarchy](http://natpryce.com/articles/000818.html) |

Kotlin 有大量优秀的[语言文档](https://kotlinlang.org/docs/reference/)和[教程](https://kotlinlang.org/docs/tutorials/)。但是我没有找到任何描述 Kotlin 类型层级结构（type hierarchy）是如何组成的文章。那真是太可惜了，因为我觉得这个类型系统很棒<sup>[1](#neat)</sup>。

关于 Kotlin 的类型层级结构只有很少的几条规则需要了解，这些规则一致和可预测地结合在一起。得益于这些规则，Kotlin 可以提供一些有用的语言特性——空安全性（null safety）、多态性（polymorphism）、不可达代码分析（unreachable code analysis），而不需要在编译器和 IDE 中使用一些手段进行特殊处理。

<!--more-->

# 顶层类型

Kotlin 中所有类型被组织成父类型/子类型（supertype/subtype）关系的层级结构。

这个层级结构的**顶层**是 `Any` 类型。例如 `String` 和 `Int` 都是 `Any` 的子类型。

{% asset_img any-intrinsics.png %}

`Any` 相当于 Java 中的 `Object` 类型。与 Java 不同的是 Kotlin 不区分**原始类型**（primitive type）和其它的类型。它们都是同一类型层级结构的一部分。

如果定义了一个没有指定父类型的类型，则该类型将是 `Any` 的直接子类型。

```kotlin
class Fruit(val ripeness: Double)
```

{% asset_img any-user-defined-type.png %}

如果你为定义的类型指定了父类型，则该父类型将是新类型的直接父类型，并且新类型的最终祖先为 `Any`。

```kotlin
abstract class Fruit(val ripeness: Double)
class Banana(ripeness: Double, val bendiness: Double): 
    Fruit(ripeness)
class Peach(ripeness: Double, val fuzziness: Double): 
    Fruit(ripeness)
```

{% asset_img any-user-defined-type-hierarchy.png %}

如果你的类型实现了多个接口，那么它将具有多个直接的父类型，而 `Any` 同样是最终的祖先。

```kotlin
interface ICanGoInASalad
interface ICanBeSunDried

class Tomato(ripeness: Double): 
    Fruit(ripeness), 
    ICanGoInASalad, 
    ICanBeSunDried 
```

{% asset_img interfaces.png %}

Kotlin 的类型检查器实施父类型/子类型关系。

例如你可以将子类型值存储到父类型变量中：

```kotlin
var f: Fruit = Banana(bendiness=0.5)
f = Peach(fuzziness=0.8)
```

但是你不能将父类型值存储到子类型变量中：

```kotlin
val b = Banana(bendiness=0.5)
val f: Fruit = b
val b2: Banana = f
// Error: Type mismatch: inferred type is Fruit but Banana was expected 
```

# 可空类型（Nullable Types）

与 Java 不同，Kotlin 区分**非空**（non-null）和**可空**（nullable）类型。到目前为止，我们看到的类型都是**非空类型**，Kotlin 不允许 `null` 作为这些类型的值。访问**非空类型**的变量将永远不会抛出空指针异常。

类型检查器拒绝尝试在非空类型上使用 `null` 或可空类型的代码。

例如：

```kotlin
var s : String = null
// Error: Null can not be a value of a non-null type String
```

如果一个变量存储的值可能为空，则需要使用与值对应的可空类型。例如 `String?` 类型是与 `String` 对应的可空类型，`String?` 类型的变量可以存储任意的 `String` 值以及 `null`。

```kotlin
var s : String? = null
s = "foo"
s = null
s = bar
```

类型检查器能确保你在使用一个可空类型的变量前不会忘记检查是否非空。Kotlin 提供了一些操作符用以便捷的使用可空类型。有关例子请参阅 [Kotlin 语言文档的 Null Safety 部分](https://kotlinlang.org/docs/reference/null-safety.html)。

可空类型具有与对应的非空类型相同的层级结构。例如 `String` 是 `Any` 的子类型，则 `String?` 是 `Any?` 的子类型；`Banana` 是 `Fruit` 的子类型，则 `Banana?` 是 `Fruit?` 的子类型。

 `Any` 是非空类型层级结构的顶层，`Any?` 则是可空类型层级结构的顶层。因为 `Any?` 是 `Any` 的父类型，所以 `Any?` 是 Kotlin 类型层级结构的最顶端。

{% asset_img parallel-nullable-and-non-nullable-hierarchies.png %}

非空类型是其对应可空类型的子类型。例如 `String` 作为 `Any` 的子类型，同时也是 `String?` 的子类型。

{% asset_img nullable-string.png %}

这就是为什么可以将非空的 `String` 值存储到可空的 `String?` 变量中，但是不能将可空的 `String?` 值存储到非空的 `String` 变量中。Kotlin 的空安全性不是由特殊规则实施的，而是可空类型与非空类型之间父类型/子类型关系的结果。

这一规则也适用于自定义的类型。

{% asset_img nullable-hierarchy.png %}

# Unit

Kotlin 是一种表达式导向的语言，所有流程控制语句都是表达式。它没有 Java 和 C 中的 `void` 函数，函数总是会返回一个值。通常我们为了副作用（side effect）而调用的那些没有实际计算任何东西的函数，将会返回 `Unit`——一种只有一个值的类型。

大多数情况下，你不需要明确指定 `Unit` 作为返回类型或从函数返回 `Unit`。如果编写的函数具有块代码体，并且不指定返回类型，则编译器会将其视为返回 `Unit` 类型，否则编译器会使用推断的类型。

```kotlin
fun example() {
    println("block body and no explicit return type, so returns Unit")
}

val u: Unit = example()
```

`Unit` 并没什么特别之处。就像任何其他类型一样，它是 `Any` 的子类型，而 `Unit?` 是 `Any?` 的子类型。

{% asset_img nullable-unit.png %}

然而 `Unit?` 类型却是一个奇怪的特殊例子，这是 Kotlin 的类型系统一致性的结果。`Unit?` 类型只有两个值：`Unit` 单例和 `null`。我从来没有发现需要明确使用 `Unit?` 类型的地方，但是在类型系统中没有特殊的 `void` 这一事实，使得处理各种函数泛型变得更加容易。

# Nothing

在 Kotlin 类型层级结构的最底层是 `Nothing` 类型。

{% asset_img nothing.png %}

顾名思义，`Nothing` 是没有实例的类型。`Nothing` 类型的表达式不会产生任何值。

注意 `Unit` 和 `Nothing` 之间的区别，对 `Unit` 类型的表达式求值将返回 `Unit` 的单例，而对 `Nothing` 类型的表达式求值则永远都不会返回。

这意味着任何类型为 `Nothing` 的表达式之后的所有代码都是无法得到执行的（unreachable code），编译器和 IDE 会向你发出警告。

什么样的表达式类型为 `Nothing` 呢？[流程控制中与跳转相关的表达式](https://kotlinlang.org/docs/reference/grammar.html#jump)。

例如 `throw` 关键字打断表达式的计算，并从函数中抛出异常。因此 `throw` 就是 `Nothing` 类型的表达式。

通过将 `Nothing` 作为所有类型的子类型，类型系统允许程序中的任何表达求值失败。这是真实世界的模型，例如 JVM 在计算表达式时内存不足，或者是有人拔掉了计算机的电源插头。这也意味着我们可以从任何表达式中抛出异常。

```kotlin
fun formatCell(value: Double): String =
    if (value.isNaN()) 
        throw IllegalArgumentException("$value is not a number") 
    else 
        value.toString()
```

你可能会惊奇地发现，`return` 语句的类型也为 `Nothing`。`return` 是一个流程控制语句，它立即从函数中返回一个值，打断其所在表达式的求值。

```kotlin
fun formatCellRounded(value: Double): String =
    val rounded: Long = if (value.isNaN()) return "#ERROR" else Math.round(value)
    rounded.toString()
```

进入无限循环或杀死当前进程的函数返回类型也为 `Nothing`。例如 Kotlin 标准库将 `exitProcess` 函数声明为：

```kotlin
fun exitProcess(status: Int): Nothing
```

如果你编写返回 `Nothing` 的自定义函数，编译器同样能检查出调用函数后无法得到执行的代码，就像使用语言本身的流程控制语句一样。

```kotlin
inline fun forever(action: ()->Unit): Nothing {
    while(true) action()
}

fun example() {
    forever {
        println("doing...")
    }
    println("done") // Warning: Unreachable code
}
```

与空安全一样，不可达代码分析是类型系统的一个特性。无需像 Java 一样在编译器和 IDE 中使用一些手段进行特殊处理。

# 可空的 Nothing?

`Nothing` 像任何其他类型一样，如果允许其为空则可以得到对应的类型 `Nothing?`。`Nothing?` **只能**包含一个值：`null`。事实上 `Nothing?` 就是 `null` 的类型。

`Nothing?` 是所有可空类型的最终子类型，所以我们可以使用 `null` 作为任何可空类型的值。

{% asset_img nullable-nothing.png %}

# 结论

当你同时考虑这一切时，可能会觉得 Kotlin 的整个类型层级结构相当复杂。

{% asset_img entire-hierarchy.png %}

但不要害怕！

我希望这篇文章能够证明 Kotlin 有一个简单而一致的类型系统。只有很少的几条规则需要了解：这是一个父类型/子类型关系的层级结构，而 `Any?` 在顶层，`Nothing` 在底层，以及非空类型是对应可空类型的子类型。就这么多了，没有其它特殊规则。一些有用的语言特性，如空安全性、面向对象多态性、不可达代码分析都是由这些简单，可预测的规则引起的。得益于这种一致性，Kotlin 的类型检查器是一个强有力的工具，可以帮助你编写简洁正确的程序。

---

<span id="neat">1. “很棒（neat）” 的意思是 “优雅巧妙高效”，而不是[凯文 · 科斯特纳在麦当娜的舞台上表现出的含义](https://www.youtube.com/watch?v=wvZhW47mGNE)</span>