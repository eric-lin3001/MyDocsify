## JVM

### OK:

1. "==" vs .equals():
   - "==": memory address
   - .equals(): content

### QUESTIONS:

​	1.1 What is "memory address" exactly mean?  why 'a' and 97.0 share the same memory address?

why 'a' always has the same memory address?

   1.2 

![Screen Shot 2020-10-12 at 10.24.00](/Users/linzeyang/Library/Application Support/typora-user-images/Screen Shot 2020-10-12 at 10.24.00.png)

s1 == s2: false (different memory address) 

解释：

1) new String()会在代码运行的时候在堆中开辟一个空间存放new String("geek"), new String("geek")。

2) 而栈中的s1,s2引用的堆的地址是不一样的（虽然它们都为new String("geek")）

s1.equals(s2): true(same value)

![Screen Shot 2020-10-12 at 10.24.35](/Users/linzeyang/Library/Application Support/typora-user-images/Screen Shot 2020-10-12 at 10.24.35.png)

s1==s2: true. Why? 

解释：

1) jvm在编译的时候会先查看s1字面量geek是否存放在字符串常量池中,有则直接引用字符串常量池里面的地址，没有则在字符串常量池新创建一个。

2) s2发现字符串常量池里面已经有了geek则直接把字符串常量池里面的地址拿了过来。

3) 最终s1和s2的地址都是相同的结果肯定为true啦。

ref:

1.  String直接赋值与使用new String的区别： https://blog.csdn.net/weixin_41098980/article/details/80060200

2. 字符串常量池：https://www.cnblogs.com/fengzheng/p/12782844.html

3. ##### [java字符串常量池——字符串==比较的一个误区](https://www.cnblogs.com/maohuidong/p/10074674.html)

   