 平常时，我们在使用Android Studio看开源库源码的时候，可以发现有些注释文档在Render之后带有可跳转的链接或引用，可方便我们跳转查看相关的信息，如下图的ViewGroup和User Interface这两个标蓝的短语。
![[1_源码中可跳转实例.png]]

这些可跳转的链接和引用在我们平常时开发是经常遇到的，对其使用并不陌生，但如果说到如何在自己的注释中创建这些跳转的链接和引用，其实会有点懵，一来不知道有哪些内容是可以用来引用的，二来不清楚如何编写引用的相关语法。如果在我们的项目中利用好链接和引用，可方便去溯源代码和理解类和方法所实现的功能，做到一目了然，减少代码熟悉的成本，提高代码的可阅读性。

本文将介绍Java和Kotlin的注释文档中可添加的链接和引用，并详细介绍如何编写链接和引用。

# 注释文档
在Java和Kotlin中，使用如以下格式所编写的注释即注释文档，注释内容使用的Markdown语法规则，可使用HTML的标签
``` java
/**
 * 注释内容
 * 多行注释内容
 * ...
 * n行注释内容
 **/
```

# 链接通用格式
在Java中使用链接的通用格式为
`{@link 类/方法/属性 链接标题(可选)}`
`<a href="网页链接地址">链接标题</a>`

在Kotlin中使用链接的通用格式为
`[链接标题(可选)][类/方法/属性]`
`[链接标题](链接地址)`

其中，对Java和Kotlin中，部分`链接标题`为可选的内容，其是Render注释文档之后，显示在文档中的一个引用字符串，点击其可跳转到链接地址的内容。简单示例如下：
## Java
![[2_Java通用引用格式一览.png| 500]]

``` Java
/**  
* {@link android.view.View}  
* <p>  
* {@link android.view.View 标题}  
* <p>  
* <a href="http://www.example.com">网页引用</a>  
*  
* @see android.view.View  
*/  
public class TestJava {  
}
```

## Kotlin
![[3_Kotlin通用引用格式一览.png| 500]]

``` Java
/**  
 * [android.view.View]  
 *  
 * [引用标题][android.view.View]  
 *  
 * [网页](http://www.example.com/somePage.html)  
 * * @see android.view.View  
 */  
class TestKotlin {  
}
```

# 跳转到包/类的链接
## Java
基本通用格式: `{@link 包名/类名或类全限定名 链接标题(可选)}`
若类中已使用import关键字引入了相关类，则可使用类名进行引用，否则使用全限定名进行引用
![[4_Java跳转到包或类.png]]

``` Java
import android.view.View;  
  
/**  
 * 跳转到包 {@link android.view}  
 * <p>  
 * 跳转到类 {@link View}  
 * <p>  
 * 跳转到类(全限定名) {@link android.view.ViewGroup}  
 * <p>  
 * 带引用标题的跳转到类 {@link View 引用标题}  
 */
 public class TestJava {  
}
```


## Kotlin
基本通用格式：`[链接标题(可选)][包名/类名或类全限定名]`
若类中已使用import关键字引入了相关类，则可使用类名进行引用，否则使用全限定名进行引用
![[5_Kotlin跳转到包或类.png]]

``` Java
import android.view.View  
  
/**  
 * 跳转到包 [android.view]  
 *  
 * 跳转到类 [View]  
 *  
 * 跳转到类(全限定名) [android.view.ViewGroup]  
 *  
 * 带引用标题的跳转到类 [引用标题][View]  
 */  
class TestKotlin {  
}
```

# 跳转到方法/属性的链接
## Java
基本通用格式为：`{@link (类名或类全限定名)#方法名(参数类型(可选))/属性名}`

如示例所示，核心格式为 `{@link #方法名/属性名}`，若是方法/属性非本类的方法，则需类名或类全限定名，若方法的参数类型不为空，则需要添加参数类型。
![[8_Java引用方法.png]]

``` Java
/**
 * 引用自身方法/变量：{@link #test()}  
 * <p>  
 * 引用自身方法/变量：{@link #testValue}
 * <p>  
 * 引用自身方法（无参可省略括号)：{@link #test}
 * <p>  
 * 引用自身方法（带参数)：{@link #test(int)}
 * <p>  
 * 引用自身方法/变量(显示自定义标题)：{@link #test() Test方法}
 * <p>  
 * 引用外部方法/变量：{@link View#invalidate()}  
 * <p>  
 * 引用外部方法/变量(全限定名）：{@link android.view.ViewGroup#FOCUS_BEFORE_DESCENDANT}  
 */
 public class TestJava {  
    public String testValue = "test";  
  
    public void test() {  
    }  
  
    public void test(int i) {  
    }  
}
```


## Kotlin
基本通用格式`[链接标题(可选)][(类名或类全限定名.)方法名/属性名]`

如示例所示，核心格式为`[方法名/属性名]`，若是方法/属性非本类的方法，则需类名或类全限定名。Kotlin无法像Java一样，引用有参数的方法。
![[9_Kotlin引用方法.png]]

``` Java
import android.view.View

/**
 * 引用自身方法/变量：[test]
 *
 * 引用自身方法/变量：[testValue]
 *
 * 引用自身方法/变量(显示自定义标题)： [Test方法][test]
 *
 * 引用外部方法/变量：[View.invalidate]
 *
 * 引用外部方法/变量（全限定名）：[android.view.ViewGroup.FOCUS_BEFORE_DESCENDANTS]
 */
class TestKotlin {
    private val testValue = "test"

    fun test() {
    }
}
```

## 跳转到网页的链接
|      | Java                        | Kotlin                 |
| ---- | --------------------------- | ---------------------- |
| 通用格式 | `<a href="网页链接地址">链接标题</a>` | `[链接标题](链接地址)`         |
| 引用网页 | ![[10_Java引用网页.png]]        | ![[11_Kotlin引用网页.png]] |
``` Java
/**
 * 跳转网页的链接: <a href="http://www.example.com">网页链接</a>
 */
public class TestJava {
}



/**
 * 跳转网页的链接: [网页](http://www.example.com)
 */
class TestKotlin {
}
```

## @see关键字
在Java 和 Kotlin中，有一个`@see` 的注解，其作用是在Render之后会生成一个`See Also`的标签，指引代码阅读者参阅其它代码，以帮助理解当前代码。

`@see` 关键字可以指向包、类、方法、属性，`@see`关键字必须位于一行注释的开头。其语法结构如下:
Java: `@see 包名.类名#方法名/属性名`
Kotlin: `@see [包名.类名.方法名/属性名]`

示例如下: 

Java: 
![[14_Java @see关键字.png]]

``` Java
import android.view.View;  
  
/**  
 * @see android.view  
 * @see View  
 * @see android.view.ViewGroup.LayoutParams#MATCH_PARENT  
 * @see #test  
 * @see #test()  
 * @see #test(int)  
 * @see #testValue  
 */public class TestJava {  
    public String testValue = "test";  
  
    public void test() {  
  
    }  
  
    public void test(int i) {  
  
    }  
}
```



Kotlin: 
![[15_Kotlin @see关键字.png]]

``` Java
import android.view.View  
  
/**  
 * @see [android.view]  
 *  
 * @see [View]  
 *  
 * @see [android.view.ViewGroup.LayoutParams.MATCH_PARENT]  
 *  
 * @see test  
 *  
 * @see testValue  
 */  
class TestKotlin {  
    var testValue = "test"  
  
    fun test() {}  
}
```
