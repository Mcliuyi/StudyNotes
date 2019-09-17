[TOC]

# ArraryList 和 LinkedList的区别

## ArraryList

### 简介

​	基于数组进行的实现，擅长随机访问，但是在插入和移除元素时比较慢

### add方法源代码

可以看到无论是直接在结尾插入还是，指定位置插入均需要先扩充数组大小

```java
/**
 * Appends the specified element to the end of this list.
 *
 * @param e element to be appended to this list
 * @return <tt>true</tt> (as specified by {@link Collection#add})
 */
public boolean add(E e) {
    ensureCapacityInternal(size + 1);  //扩充数组
    elementData[size++] = e; 
    return true;
}

    /**
     * Inserts the specified element at the specified position in this
     * list. Shifts the element currently at that position (if any) and
     * any subsequent elements to the right (adds one to their indices).
     *
     * @param index index at which the specified element is to be inserted
     * @param element element to be inserted
     * @throws IndexOutOfBoundsException {@inheritDoc}
     */
    public void add(int index, E element) {
        rangeCheckForAdd(index);

        ensureCapacityInternal(size + 1);  // 扩充数组
        System.arraycopy(elementData, index, elementData, index + 1,
                         size - index); //拷贝数组
        elementData[index] = element;
        size++;
    }
```

## LinkedList

### 简介

​	`List` 接口的链接列表实现,插入删除较快，以及顺序访问，但是对随机访问较慢



### 能够直接实现栈的所有功能

​	通过`addFirst(),getFirst(),removeFirst(),isEmpty()`方法可以实现栈的操作



### 支持队列的行为实现了`Queue`接口