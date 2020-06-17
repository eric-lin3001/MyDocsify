## JAVA容器

### OK:

1. ArrayList: 查询,修改效率高<O(1)>，插入，删除效率低<O(N)>。
2. LinkedList: 插入，删除效率高<O(1)>，查询,修改效率低<O(N)>。

### NOT OK -> OK

1. hashMap:

   1) put方法：简言之先判断hashCode，如果hashCode相同，则可以确定属于同一个slot（单链表），如果equals也相同则覆盖值，如果hashCode相同，equals不同则添加一个链表节点。

2. ![img](https://github.com/lvminghui/Java-Notes/raw/master/docs/imgs/put%E6%96%B9%E6%B3%95%E6%B5%81%E7%A8%8B%E5%9B%BE.png)

### STILL NOT OK：

1. 对相同的key插入2个不同的值，debug时怎么没看到链表？
2. ConcurrentHashMap
3. HashSet
4. LinkedHashMap
5. TreeMap
6. 为什么JDK1.8加入红黑树？