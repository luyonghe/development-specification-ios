# snaillove-development-specification-iOS

## 编码规范
苹果公司已经有了一套完整的编码规范，google也有一套属于c的一套编码规范。我结合这两套规范，总结出了这套规范，如果有错误或者不恰当之处，联系我或者拿出来讨论。

##1.	留白：
留白有助于代码的可读性
###（1）	不要求在@interface,@implementation和@end前后空行，如果你在@interface声明了实例变量，则必须在大括号关闭之后空一行。
###（2）	特殊情况下可以不空行，像接口或者实现的特别短，比如一些私有方法或者桥接类。
###（3）	包括一些类的声明也需要空格，方便查看代码。
###（4）	代码缩进方式
####1.	行宽
方法尽量控制在80行之内，如果一个方法超过80行大概也就是超过了一个屏幕的高度，代码的阅读性就降低了。
Xcode中通过设置 Xcode > Preferences > Text Editing > Show page guide，来使越界更容易被发现。
####2.方法声明和定义
  +-方法和返回类型之间须空格，参数列表中参数可以添加空格，但这并不是必须的。
 ```java
      -	(void)doSomethingWithString:(NSString *)theString {
  						...
      }
 ```

星号前的空格是可选的。当写新的代码时，要与先前代码保持一致。
如果一行有非常多的参数，更好的方式是将每个参数单独拆成一行。如果使用多行，将每个参数前的冒号对齐。
 ```java
      - (void)doSomethingWith:(GTMFoo *)theFoo
                         rect:(NSRect)theRect
                     interval:(float)theInterval{
               ...
      }
 ```

当第一个关键字比其它的短时，保证下一行至少有 4 个空格的缩进。这样可以使关键字垂直对齐，而不是使用冒号对齐：
 ```java
      - (void)short:(GTMFoo *)theFoo
    	    longKeyword:(NSRect)theRect
    	    evenLongerKeyword:(float)theInterval{
  	        ...
      }
 ```

####3.方法调用
方法的调用应尽量保持与方法生命的格式一致。
调用时所有参数应该在同一行：
 ```java
        [myObject doFooWith:arg1 name:arg2 error:arg3];
 ```
或者每行一个参数，以冒号对齐：
 ```java
        [myObject doFooWith:arg1
                       name:arg2
                      error:arg3];
 ```

不要使用下面的缩进方式，下面的方式都让你的代码的可读性降低了。
 ```java
        [myObject doFooWith:arg1 name:arg2  // some lines with >1 arg
                      error:arg3];
        
        [myObject doFooWith:arg1
                       name:arg2 error:arg3];
        
        [myObject doFooWith:arg1
                  name:arg2  // aligning keywords instead of colons
                  error:arg3];
```

方法定义与方法声明一样，当关键字的长度不足以以冒号对齐时，下一行都要以四个空格进行缩进。
```java
        [myObj short:arg1
           	longKeyword:arg2
            evenLongerKeyword:arg3];
```
###（5） @public和@private
用@pubic和@private修饰时，应该以一个空格缩进。
###（6）异常
每个 @ 标签应该有独立的一行，在 @ 与 {} 之间需要有一个空格， @catch 与被捕捉到的异常对象的声明之间也要有一个空格。或者在编码风格上把｛｝的前括号移植到下行。

如果你决定使用 Objective-C 的异常，那么就按下面的格式。不过你最好先看看 [避免抛出异常] (http://zh-google-styleguide.readthedocs.org/en/latest/google-objc-styleguide/features/#avoid-throwing-exceptions) 了解下为什么不要使用异常。
```java
      @try {
        foo();
      }
      @catch (NSException *ex) {
        bar(ex);
      }
      @finally {
        baz();
      }
```


##2.	命名规范：

关于多语言下编写代码时的命名说明：

当编写 Objective-C++ 代码时，事情就不这么简单了。许多项目需要实现跨平台的 C++ API，并混合一些 Objective-C、Cocoa 代码，或者直接以 C++ 为后端，前端用本地 Cocoa 代码。这就导致了两种命名方式直接不统一。

解决方案：编码风格取决于方法/函数以哪种语言实现。如果在一个 @implementation 语句中，就使用 Objective-C 的风格。如果实现一个 C++ 的类，就使用 C++ 的风格。这样避免了一个函数里面实例变量和局部变量命名规则混乱，严重影响可读性。

关于c++和Cocoa的规范。这里说的是官方规范。


###（1）	命名前缀：
每个自己定义的类名都要加上类名前缀。为每个类都添加相同的前缀，可在不同的应用间重复使用。
###（2）	扩展名：
类别的文件名应该包含被扩展的类名，如Toast+UIView.h
###（3）	类名
类名应该首字母大写，并以驼峰格式分割单词。如：LXLightEffectHelper
###（4）	方法名：
方法名应该以小写字母开头，并混合驼峰格式。每个参数也应该以小写字母开头。详情参见
  [Apple’s Guide to Naming Methods] (https://developer.apple.com/library/mac/documentation/Cocoa/Conceptual/CodingGuidelines/Articles/NamingMethods.html)
###（5）	变量名：
变量名应该以小写字母开头，并用驼峰格式。类的成员变量以下划线作为后缀。如：myInstanceVariable_
####1.普通变量名
变量名称有描述性，有助于对代码的理解。
####2.实例变量
实例变量应该混合大小写，并以下划线作为后缀，如 usernameTextField_。然而，如果不能使用 Objective-C 2.0（操作系统版本的限制），并且使用了 KVO/KVC 绑定成员变量时，我们允许例外（KVO=Key Value Observing，KVC=Key Value Coding）。这种情况下，可以以一个下划线作为成员变量名字的前缀，这是苹果所接受的键/值命名惯例。如果可以使用 Objective-C 2.0，@property 以及 @synthesize 提供了遵从这一命名规则的解决方案。（官网翻译）
####3.常量
变量名（包括宏，枚举，静态局部变量等）以字母小写k开头，使用驼峰格式分割单词，如：kWritePerm



##3.	编码风格：
  每位开发人员都有自己的编码风格，但是很多时候，当加入一个新团队，就需要遵循特定的规范。
  
  虽然有些人可能会拒绝遵循严格的编码指南，但是为了提高代码的可读性和降低代码维护的难度，通常还是建议开发人员遵循规范。Sun公司的“[Java编程语言编码规范：为什么要有编码规范？](https://en.wikipedia.org/wiki/Coding_conventions#Software_maintenance)”（建议大家看一下）支持遵循规范进行编码的做法，原因如下：
  
•	一款软件的维护成本占软件整个生命周期总成本的40%-80%。

•	几乎没有软件在整个生命周期中都是由其作者进行维护。

•	编码规范提高了软件的可读性，使工程师可以更迅速、更彻底地读懂新代码。

•	如果开发人员要将源代码作为产品交付，那么他需要保证，该产品跟他创造的任何一款产品相比，都进行了精心地打包，而且同样简洁…

这些是其他公司的规范，可以让我们借鉴。

包括[Google](http://google-styleguide.googlecode.com/svn/trunk/objcguide.xml)、[GitHub](https://github.com/github/objective-c-style-guide)、[Adium](https://trac.adium.im/wiki/CodingStyle)、[Sam Soffes](https://gist.github.com/soffes/812796)、[CocoaDevCentral](http://cocoadevcentral.com/articles/000082.php)、[Luke Redpath](http://lukeredpath.co.uk/blog/my-objective-c-style-guide.html)或者[Marcus Zarra](http://www.cimgf.com/zds-code-style-guide/)。



##4.	注释：
注释在项目中起这至关重要的作用，他可以让我们用更少的时间来理解作者的代码。它还有一个作用那就是促进代码的封装性。（隐形属性）

###（1）	文件注释
每个文件的开头以文件内容的简要描述起始，紧接着是作者，最后是版权声明和许可证样板。
每个文件应该按照这种顺序来做下面的事情

*文件内容的简要描述

*代码作者

*版本信息声明（比如Copyright 2008 Google Inc. ）（非必须）

*必要的话，加上许可证样板，尾项目选择一个合适的授权样板。（非必须）

如果你对其他人的原始代码作出重大的修改，请把你自己的名字添加到作者里面。当另外一个代码贡献者对文件有问题时，他需要知道怎么联系你，这十分有用。
###（2）	声明注释
每个接口、类别一节协议应辅以注释，以描述它的目的及整个项目的关系。

```java
        // A delegate for NSApplication to handle notifications about app
        // launch and shutdown. Owned by the main app controller.
        @interface MyAppDelegate : NSObject{
         		 ...
         }
        @end
```
如果你已经在文件头部详细描述了接口，可以直接说明 “完整的描述请参见文件头部”，但是一定要有这部分注释。
另外，公共接口的每个方法，都应该有注释来解释它的作用、参数、返回值以及其它影响。

为类的线程安全性作注释，如果有的话。如果类的实例可以被多个线程访问，记得注释多线程条件下的使用规则。

###（3）	实现注释
使用 | 来引用注释中的变量名及符号名而不是使用引号。

 这会避免二义性，尤其是当符号是一个常用词汇，这使用语句读起来很糟糕。例如，对于符号 count ：
 
      // Sometimes we need |count| to be less than zero.
或者当引用已经包含引号的符号：

      // Remember to call |StringWithoutSpaces("foo bar baz")|
###（4）	其他
对象所有权

当与 Objective-C 最常规的作法不同时，尽量使指针的所有权模型尽量明确。
    继承自 NSObject 的对象的实例变量指针，通常被假定是强引用关系（retained），某些情况下也可以注释为弱引用（weak）或使用 __weak 生命周期限定符。同样，声明的属性如果没有被类 retained，必须指定是弱引用或赋予 @property 属性。然而，Mac 软件中标记上 IBOutlets 的实例变量，被认为是不会被类 retained 的。
    
    当实例变量指向 CoreFoundation、C++ 或者其它非 Objective-C 对象时，不论指针是否会被 retained，都需要使用 __strong 和 __weak 类型修饰符明确指明。CoreFoundation 和其它非 Objective-C 对象指针需要显式的内存管理，即便使用了自动引用计数或垃圾回收机制。当不允许使用 __weak 类型修饰符（比如，使用 clang 编译时的 C++ 成员变量），应使用注释替代说明。
    
注意：Objective-C 对象中的 C++ 对象的自动封装，缺省是不允许的，参见 这里 的说明。
强引用及弱引用声明的例子：
```java
        @interface MyDelegate : NSObject {
         @private
            IBOutlet NSButton *okButton_;  // normal NSControl; implicitly weak on Mac only
          
            AnObjcObject* doohickey_;  // my doohickey
            __weak MyObjcParent *parent_;  // so we can send msgs back (owns me)
          
            // non-NSObject pointers...
            __strong CWackyCPPClass *wacky_;  // some cross-platform object
            __strong CFDictionaryRef *dict_;
        }
        @property(strong, nonatomic) NSString *doohickey;
        @property(weak, nonatomic) NSString *parent;
        @end
```
（强引用 - 对象被类 retained。弱引用 - 对象没有被类 retained，如委托）


##5.	项目中的错误和警告：

##6. 在项目结构中，不建议使用单纯的Group，直接采用文件夹的形式。



参考资料
####1.[http://zh-google-styleguide.readthedocs.org/en/latest/google-objc-styleguide/spacing](http://zh-google-styleguide.readthedocs.org/en/latest/google-objc-styleguide/spacing)
####2.[https://developer.apple.com/library/mac/documentation/Cocoa/Conceptual/CodingGuidelines/CodingGuidelines.html](https://developer.apple.com/library/mac/documentation/Cocoa/Conceptual/CodingGuidelines/CodingGuidelines.html)
####3.[https://en.wikipedia.org/wiki/Acronym#Nomenclature](https://en.wikipedia.org/wiki/Acronym#Nomenclature)


