# ios开发学习文档



[**Objective-C中的实例方法、类方法、Category、Protocol**](http://www.devtalking.com/articles/method-category-protocol/)

[**Learn Objective-C**](http://cocoadevcentral.com/d/learn_objectivec/)  这也是广受推荐的一份文档，短小精练，适合入门。

[Programming with Objective-C: About Objective-C](https://developer.apple.com/library/content/documentation/Cocoa/Conceptual/ProgrammingWithObjectiveC/Introduction/Introduction.html) Apple 撰写的一份关于 Objective-C 2.0 的一份文档，不建议入门读

[Objective C 基础知识| 菜鸟教程](http://www.runoob.com/ios/ios-objective-c.html)



[**Objective-C基本数据类型**](https://segmentfault.com/a/1190000005726614)

> 因为Objective－C（下称ObjC）本质是一个C语言的超集，所以所有C语言支持的基本数据类型，ObjC同样支持，并且ObjC还支持一些其它的常用数据类型。

- int 与 NSInteger

  ```
  #if __LP64__ || (TARGET_OS_EMBEDDED && !TARGET_OS_IPHONE) || TARGET_OS_WIN32 || NS_BUILD_32_LIKE_64
  typedef long NSInteger;
  typedef unsigned long NSUInteger;
  #else
  typedef int NSInteger;
  typedef unsigned int NSUInteger;
  #endif
  ```

  > 注意，这里主要是为了同时匹配64位和32位处理器，在上面官方框架的代码中我们看到，64位内核中NSInteger为long型，而在32位内核中为int型，使用NSInteger，就不用特意去考虑内核位宽问题。

- bool 与 BOOL

  > C语言标准中没有布尔型变量，C++中的bool类型，为true和false，这在许多其他的类C语言中都是一样的，例如java、C#、php等，但在ObjC中，你可以使用bool类型，但更建议使用ObjC专用的BOOL类型，这个基本布尔型的值为YES和NO。

- float 与 CGFloat

  ```
  #if defined(__LP64__) && __LP64__
  # define CGFLOAT_TYPE double
  # define CGFLOAT_IS_DOUBLE 1
  # define CGFLOAT_MIN DBL_MIN
  # define CGFLOAT_MAX DBL_MAX
  #else
  # define CGFLOAT_TYPE float
  # define CGFLOAT_IS_DOUBLE 0
  # define CGFLOAT_MIN FLT_MIN
  # define CGFLOAT_MAX FLT_MAX
  #endif

  /* Definition of the `CGFloat' type and `CGFLOAT_DEFINED'. */

  typedef CGFLOAT_TYPE CGFloat;
  ```

  >可以看到，64位中CGFloat是double类型，32位中则是float类型。CGFloat 不是Foundation框架的基础变量，而是定义在UIKit框架中，CG代表CoreGraphic（核心绘图框架）

- Char,string 与NSString

  ```
  NSString* textA = @"123";     
  NSString* textB = textA;
  textA = @"456";
  NSLog(@"%@",textA); //输出 456
  NSLog(@"%@",textB); //输出 123
  ```

  >注意到没有，按道理说将textB指针指向textA以后，textA值改变，textB应该也跟着变。但实际情况并没有，这是因为对于NSString类型来说，等号赋值，实际是深度拷贝。textA＝@"456"这一步textA的指针已经改变，实际操作等同于 textA = [@"456" copy]。
  >
  >textB = textA，实际操作等同于 textB = [textA copy]。
  >
  >这里的copy函数，是NSObject的不可变拷贝方法。

- NSValue

  ​

- NSNumber

- NSArray