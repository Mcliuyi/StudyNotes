# Java填充List容器方法及源码介绍

`Collections`提供了两个填充容器的静态方法`fill,nCopies`

### 用法

```java
 // 创建一个存放int型的数组，同时填充四个整型对象1
        List<Integer> intArr = new ArrayList<Integer>(Collections.nCopies(4, 1));
        System.out.println(intArr.toString());
	//将intArr容器填充为2
        Collections.fill(intArr, 2);
        System.out.println(intArr.toString());

```

```shell
# out
[1, 1, 1, 1]
[2, 2, 2, 2]
```

### 源码介绍

#### fill源码

```java
 /**
     * Replaces all of the elements of the specified list with the specified
     * element. <p>
     *
     * This method runs in linear time.
     *
     * @param  <T> the class of the objects in the list
     * @param  list the list to be filled with the specified element.
     * @param  obj The element with which to fill the specified list.
     * @throws UnsupportedOperationException if the specified list or its
     *         list-iterator does not support the <tt>set</tt> operation.
     */
	/**
	* list - 使用指定元素填充的列表。
	* obj - 用来填充指定列表的对象。	
	*/
    public static <T> void fill(List<? super T> list, T obj) {
        int size = list.size();
		// 这里判断容器大小是否超过了默认设置的阀值25或者该容器是实现RandomAccess接口的
        if (size < FILL_THRESHOLD || list instanceof RandomAccess) {
            for (int i=0; i<size; i++)
                //直接填充
                list.set(i, obj);
        } else {
            //如果不是则调用List中的方法listIterator，返回迭代器进行设置,使用迭代器的目的是为了提高执行效率
            ListIterator<? super T> itr = list.listIterator();
            for (int i=0; i<size; i++) {
                itr.next();
                itr.set(obj);
            }
        }
    }
```

#### nCopies源码

```java
 /**
     * Returns an immutable list consisting of <tt>n</tt> copies of the
     * specified object.  The newly allocated data object is tiny (it contains
     * a single reference to the data object).  This method is useful in
     * combination with the <tt>List.addAll</tt> method to grow lists.
     * The returned list is serializable.
     *
     * @param  <T> the class of the object to copy and of the objects
     *         in the returned list.
     * @param  n the number of elements in the returned list.
     * @param  o the element to appear repeatedly in the returned list.
     * @return an immutable list consisting of <tt>n</tt> copies of the
     *         specified object.
     * @throws IllegalArgumentException if {@code n < 0}
     * @see    List#addAll(Collection)
     * @see    List#addAll(int, Collection)
     */
	/**
	* n - 返回列表中的元素数, 即需要填充的数量。
	* o - 填充的对象。
	* 返回值：由指定对象 n 个副本组成的不可变列表。
	*/
    public static <T> List<T> nCopies(int n, T o) {
        if (n < 0)
            throw new IllegalArgumentException("List length = " + n);
        return new CopiesList<>(n, o);
    }
```

