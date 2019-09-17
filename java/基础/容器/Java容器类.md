# Java容器类

## `Collection`

### `List`

有序序列，提供精确搜索，与插入，允许重复元素

#### `LinkedList`链表

​	实现原理: 队列(`Deque`)和数组(`List`)

​	线程安全: **否**

​	一种可以在任何位置进行高效的插入和删除操作的有序序列,并且**允许null值**

​	通过`Collections.synchronizedList`方法创建的列表以保证**线程同步**

​	插入，删除均只要O(1),但在随机查找上为O(n)

#### `ArrayList`顺序结构动态数组类

​	实现原理：**数组**

​	线程安全:  **否**

​	一种可以动态增长和缩减的索引序列(注: 默认初始化容量为10), 插入数据的时间复杂度为**O(n)**, 随机查找为**O(1)**,有剩余空间，并且是追加的到数组末尾则为O(1)

​	**删除操作O(n)**

```java
 public E remove(int index) {
        rangeCheck(index);

        modCount++;
        E oldValue = elementData(index);

        int numMoved = size - index - 1;
   			// 如果数组大小减去需要移除的元素的下标减1依然大于0，则将删除元素之后的元素进行移动
        if (numMoved > 0)
            System.arraycopy(elementData, index+1, elementData, index,
                             numMoved);
        elementData[--size] = null; // clear to let GC do its work

        return oldValue;
    }
```



#### `Vector`向量

​	实现原理：数组

​	线程安全：是

​	和`ArrayList`一样可以自增长大小同时支持索引组件，并根据添加删除数据进行自动调整大小。

##### `Stack`堆栈

​	实现原理：堆栈，后进先出(LIFO)，继承`Vector`

​	线程安全：是

​	`Deque`接口实现了更加完善的**堆栈**操作，建议使用如下: 

​	`Deque<Integer> stack = new ArrayDeque<Integer>();`

### `Set`

​	不包含重复元素的集合，即不存在 `e1.equals(e2)`的情况,内容不会相同

#### `HashSet`

​	实现原理: 实际由**HashMap**维护 

​	线程安全: 否

​	没有重复元素的无序集合, 实际内部实现是采用`HashMap`

##### `LinkedHashSet`

​	实现原理: 继承HashSet，它维护了一个贯穿其所有条目的双向链表。map+双向链表

​	线程安全: 否

​	一种可以记住元素插入次序的集合

#### `TreeSet`

​	实现原理: **TreeMap**

​	线程安全:否

使用一下方法实现线程安全

```java
SortedSet s = Collections.synchronizedSortedSet（new TreeSet（...））;
```

​	一种有序集合	

##### `SortedSet`

​	实现原理：继承**TreeSet**

​	线程安全: 否

​	可以按照自然排序，或者给定排序规则进行排序

### `Queue`

实现了队列，先进先出(FIFO)

#### `PriorityQueue`

实现原理： 优先级堆

线程安全: 否

 一种基于优先级堆实现的优先级队列，可根据自然顺序或者预先提供排序规则进行排序，不允许**NUll**

#### `ConcurrentLinkedQueue`

实现原理：链表，非阻塞算法

线程安全: 是

一种基于链表实现的安全队列

与其他并发集合类一样，不允许null值

#### `ConcurrentLinkedDeque`

​	实现原理：基于链表的双端队列

​	线程安全：是

​	线程安全的双端队列

#### `Deque`

​	双端队列，支持两端插入和移除元素

##### `ArrayDeque`

​	实现原理：

​	线程安全： 否

​	用作堆栈时快于 `Stack`，在用作队列时快于 `LinkedList`

​	时间复杂度，基本在线性时间

## `Map`

一种不允许重复键的键值对

### `HashMap`

实现原理：数组, 链表

线程安全：否

一种基于哈希表实现的map，并允许使用 `null` 值和 `null` 键

以下方法实现同步

```java
Map m = Collections.synchronizedMap(new HashMap(...));
```

### `Hashtable`

实现原理：map

线程安全：是

任何非 `null` 对象都可以用作键或值。

### `TreeMap`

线程安全: 否

一种键值有序排序映射表

### `LinkedHashMap`

线程安全：否

一种具有顺序的HashMap,链接列表定义了迭代顺序

### `WeakHashMap`

一种当某个键不再使用时，gc会自动进行回收，null 值和 null 键都被支持

对于一个给定的键，其映射的存在并不阻止垃圾回收器对该键的丢弃，这就使该键成为可终止的，被终止，然后被回收

### `ConcurrentHashMap`

线程安全: 是

一种以原子操作的map实现，