

1. map 遍历方法：

   ```java
   public class Main {
       public static void main(String[] args) {
           Map<String, Integer> map = new HashMap<>();
           map.put("apple", 123);
           map.put("pear", 456);
           map.put("banana", 789);
           for (Map.Entry<String, Integer> entry : map.entrySet()) {
               String key = entry.getKey();
               Integer value = entry.getValue();
               System.out.println(key + " = " + value);
           }
       }
   }
   ```

   entryset源码。

2. hashMap在发生hash碰撞的情况下，为什么map.get()方法能取到唯一的值？

   ```java
   p.next = newNode(hash, key,value,null);
   ```

   在map.put(k,v)方法中，若h=hash(key1) = hash(key2)，即形成hash冲突，这时会在数组哈希值为h对应的索引上建立链表，链表的节点包括：

   ![Screen Shot 2020-12-03 at 14.11.37](/Users/linzeyang/Library/Application Support/typora-user-images/Screen Shot 2020-12-03 at 14.11.37.png)

   将map.put(k,v)中的k,v插入链表，插入规则是，如果k存在，则覆盖原有的v，若不存在则新增。

   所以在map.get(k)时，会遍历链表，取出唯一的value值。







ref：https://tech.meituan.com/2016/06/24/java-hashmap.html