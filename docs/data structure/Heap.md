Heap is just an array, but looks like a tree.

最大堆插入：

```java
//过程2： 向最大堆中插入数据
	public static void insert(ArrayList<Integer> maxHeap,int value){
		// 在数组尾部添加,且注意下标为0的位置不放元素
		if(maxHeap.size()==0)
			maxHeap.add(0);
		maxHeap.add(value);
		heapUp(maxHeap,maxHeap.size()-1);
	}
	//过程2：把"插入"的元素上浮
	public static void heapUp(ArrayList<Integer> maxHeap,int index){
		if(index>1){
			// 求出其父亲节点
			int parent = index/2;
			int parentValue = maxHeap.get(parent);
			int indexValue = maxHeap.get(index);
			// 如果父亲节点的值小于index节点的值，交换两者的位置
			if(parentValue<indexValue){
				Collections.swap(maxHeap, parent, index);
				heapUp(maxHeap,parent);
			}
		}
	}
```

参考：https://blog.csdn.net/sinat_27026243/article/details/77507745

