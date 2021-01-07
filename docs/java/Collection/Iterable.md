0. hierarchy:

   ![Screen Shot 2020-11-17 at 16.24.07](/Users/linzeyang/Desktop/shots/Screen Shot 2020-11-17 at 16.24.07.png)

所有集合类（除Map）都要实现Iterable接口，Iterable接口内有3个方法（这里只展示了一个），另外两个是forEach() 和 spliterator()。iterator方法返回的类型又是一个接口Iterator，该接口内有3个方法，分别是hasNext(),next()和remove()。



1. 为什么把两个接口分开？

   原因是实现了`Iterable`的类可以再实现多个`Iterator`内部类。例如`LinkedList`中的`ListItr`和`DescendingIterator`两个内部类，就分别实现了双向遍历和逆序遍历。通过返回不同的`Iterator`实现不同的遍历方式，这样更加灵活。如果把两个接口合并，就没法返回不同的`Iterator`实现类了。



