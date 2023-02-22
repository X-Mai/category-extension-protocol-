# category和extension区别,以及protocol
### ios category和extension区别,以及protocol的总结:

#### category和extension区别参考:
- https://www.jianshu.com/p/6706892a050e
- https://www.jianshu.com/p/e3d6b1aa7618
- https://www.shuzhiduo.com/A/gVdnyL6a5W/     上述两篇帖子重点讲解category,此帖子重点讲解extension

#### 关于iOS 类扩展Extension的进一步理解
很多人可能会问  iOS的分类和扩展的区别，网上很多的讲解，但是一般都是分类讲的多，而这也是我们平常比较常用的知识；但是，对于扩展，总觉得理解的朦朦胧胧，不够透彻。

这里就讲一下我自己的理解，但是这个理解也是集合了前辈的经验来的，只不过我用大白文再延伸一点。

对于类扩展，先看下面的概念：
```
能为某个类附加额外的属性，成员变量，方法声明
一般的类扩展写到.m文件中
一般的私有属性写到类扩展
```
使用格式：
```
@interface Mitchell()
//属性
//方法
@end
```
与分类的区别：
```
分类的小括号中必须有名字
 
@interface 类名（分类名字）
/*方法声明*/
@end
@implementation类名（分类名字）
/*方法实现*/
@end
分类只能扩充方法，不能扩展属性和成员变量（如果包含成员变量会直接报错，runtime实现除外）。
如果分类中声明了一个属性，那么分类只会生成这个属性的set、get方法声明，也就是不会有实现（不会生成成员变量）。
```
那么，如何创建一个扩展呢：
```
通过New File  -> Objective-C extension来创建，比如我选择ASStudent类，延展名叫hello，那么会自动创建一个.h文件叫ASStudent_hello.h，
 
没有.m文件，因为可以直接在类的.m里写即可。（这个也正是和分类的不同，分类会有.h 和 .m）
```
其实，对于只有.h文件这点，有些人可能就比较疑惑，只有一个头文件，怎么和分类不一样？

这正是扩展的不一样，它只会创建一个头文件，我们在里面可以添加成员变量、属性、方法等；如果要实现，只需要在它要扩展的类  .m文件去实现即可。

其实可以理解成原有类多了一个.h文件，但写在这个头文件里面的属性、方法等，都是私有的，只能被这个类所拥有访问。

到这里，大家有没有觉得和一种场景很熟悉？

对了，就是  .m文件里的定义属性，有时我们不会在.h里写属性，因为那样会变成public，只要import后，外部都可以访问。

如果我们只想当前类用一下，只需要写在.m里面，这样的属性或方法其实也是扩展的一种特殊情况啦。。。

摘自网上的一段话：

```
a：我们可以不通过创建文件来创建延展，可以直接在.m文件里写@interface和@implementation，
 
注意这两个都要写在.m文件里，因为如果把@interface写在.h里，那么里面的方法都是public的；
```
```
b：此外，我们也可以直接省略@interface，直接在.m文件里写方法即可，但还是建议书写@interface，这样的好处是可阅读性强，可以在文件一开始的几行就告知了哪些是私有方法。
```
这正好解释了，为什么大神会说扩展其实无处不在了。



根据网上大神总结帖子整理,供自己查阅使用
