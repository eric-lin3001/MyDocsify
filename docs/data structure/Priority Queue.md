优先队列本质是最大/最小堆

以最大堆为例：

1. offer(): 取最大堆根元素，时间复杂度O(logn)
2. poll(): 返回并删除最大堆根元素，时间复杂度O(logn)

代码：

```java
// 上浮
private void swim(int k) {
    while(k > 1 && less(k/2, k))  { //index=k/2的元素小于index=k的元素
        swap(k/2, k);               //交换index=k/2和index=k的元素
        k = k/2;
    }
}

// 下沉
private void sink(int k) {
    while(2*k <= N) {
        int j = 2*k;
        if(j < N && less(j, j+1))  //取得k节点的两个子节点中大一点的那个节点的下标
          j++;
        swap(k, j);                //交换下沉节点和那个子节点的元素
        k = j;
    }
}
```

