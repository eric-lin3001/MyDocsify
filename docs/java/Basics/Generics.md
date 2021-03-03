##### Generics



###### **常用的通配符为： T，E，K，V，？**

- ？ 表示不确定的 java 类型
- T (type) 表示具体的一个 java 类型
- K V (key value) 分别代表 java 键值中的 Key Value
- E (element) 代表 Element

###### Notes

- 在调用方法时，程序会先找和参数匹配的方法，如找不到，再找泛型方法。
- 基础类型不可以作为泛型方法的参数。

###### Example

```java
package basics.generics;

public class MainClass {
    public static void main(String[] args) {
        Integer[] ints = new Integer[]{1,2};
        Character[] chars = new Character[]{'a','b'};
        printMe(ints);
        printMe(chars);

        System.out.println(max(1,2,1));
    }

    /**
     * Example 1
     * @param array
     * @param <T>
     */
//    public void printMe(int[] a){
//        for(int i:a){
//            System.out.println(i);
//        }
//    }

//    void printMe(char[] a){
//        for(char i:a){
//            System.out.println(i);
//        }
//    }

    static <T> void printMe(T[] array){
        for(T i:array){
            System.out.printf("%s ",i);
        }
        System.out.println();
    }

    /**
     * Example 2
     * @param <T>
     * @param <T>
     */

  // <T extends Comparable<T>> means only objects that extends Comparable<T> can use this method.
    static <T extends Comparable<T>> T max(T a,T b,T c){
        T tempMax = a;
        if(b.compareTo(tempMax)>0){
            tempMax = b;
        }
        if(c.compareTo(tempMax)>0){
            tempMax = c;
        }

        return tempMax;
    }
}

```

