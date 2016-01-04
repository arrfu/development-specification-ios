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
      -	(void)doSomethingWithString:(NSString *)theString 
      {
  						...
      }
 ```

星号前的空格是可选的。当写新的代码时，要与先前代码保持一致。
如果一行有非常多的参数，更好的方式是将每个参数单独拆成一行。如果使用多行，将每个参数前的冒号对齐。
 ```java
      - (void)doSomethingWith:(GTMFoo *)theFoo
                         rect:(NSRect)theRect
                     interval:(float)theInterval
      {
               ...
      }
 ```

当第一个关键字比其它的短时，保证下一行至少有 4 个空格的缩进。这样可以使关键字垂直对齐，而不是使用冒号对齐：
 ```java
      - (void)short:(GTMFoo *)theFoo
    	    longKeyword:(NSRect)theRect
    	    evenLongerKeyword:(float)theInterval
      {
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


##4.	注释：
##5.	项目中的错误和警告：


参考资料
####1.[http://zh-google-styleguide.readthedocs.org/en/latest/google-objc-styleguide/spacing](http://zh-google-styleguide.readthedocs.org/en/latest/google-objc-styleguide/spacing)
####2.[https://developer.apple.com/library/mac/documentation/Cocoa/Conceptual/CodingGuidelines/CodingGuidelines.html](https://developer.apple.com/library/mac/documentation/Cocoa/Conceptual/CodingGuidelines/CodingGuidelines.html)
####3.[https://en.wikipedia.org/wiki/Acronym#Nomenclature](https://en.wikipedia.org/wiki/Acronym#Nomenclature)

##6. 在项目结构中，不建议使用单纯的Group，直接采用文件夹的形式。
