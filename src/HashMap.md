1. HashMap的内部结构？

   底层使用哈希表(数组+单向链表)，当链表长度大于8会把链表转换成红黑树以实现O(logn)时间复杂度内查找。

2. 讲一下HashMap中的put方法过程？

   - 对key求Hash值，然后再计算下标
   - 如果没有碰撞，直接放入桶中。
   - 如果碰撞了，以链表的方式连接到后面。
   - 如果链表的长度超过阈值8，就把链表转换成红黑树。
   - 如果节点已经存在就替换旧值。
   - 如果桶满了，就需要resize。

3. HashMap中hash函数是怎么实现的？还有哪些hash的实现方式？

   - 高16bit不变，低16bit与高16bit做一个异或运算。
   - （n-1) & hash  ---->得到下标

4. HashMap怎样解决冲突，讲一下扩容过程，假如一个在原数组中，现在移动了新数组，位置肯定改变了，那是什么定位到这个值新数组中的位置。

   - 将新节点加到链表后
   - 容量扩充为原来的两倍，然后对每个节点重新计算哈希值。
   - 这个值只可能在两个地方，一个是原下标的位置，另一种是在下表为<原下标+原容量>的位置。

5. 抛开HashMap，hash冲突有哪些解决办法？

   - 开放地址，链地址法

6. 针对HashMap中某个Entry链太长，查找的时间复杂度可能达到O(n)怎么优化？

   - 将链表转为红黑树，JDK1.8已经实现
