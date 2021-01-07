1. List接口具有的特征：元素都按顺序存储，且都可以通过索引查找到，且元素可以重复。
2. List接口下三个实现类： ArrayList, LinkedList, Vector。其中Vector是线程安全的。为什么？既然是线程安全，为什么Vector用得少？

3. methods:

   1) 删除myList列表中index[2,3,4]的元素：

   ```java
   myList.subList(2,5).clear()
   ```

4. 将列表倒序输出:

   ```java
   private static void reverseMe(List<Integer> l){
     ListIterator<Integer> it = l.listIterator(l.size());
     while (it.hasPrevious()){
       System.out.println(it.previous());
     }
   }
   ```

   ListIterator和Iterator区别？

