# JavaScript中的数据结构

### Introduction

&emsp;&emsp;对于语言的学习中，一门语言的数据结构是一个非常基础也非常重要的问题。在一些开发实例中，后端与数据分析过程中，按照特定组件的需求指定数据形式，但是前端在数据的应用过程中，也需要对数据的形式进行二次加工，比如数据的维度与视觉效果的映射，悬停的Tooltip也需要数据的二次加工等。

> &emsp;&emsp;作为前端的工程师，我们依赖像**React**这样的库来开发view层,同时又依赖**Redux**这样的库来管理数据状态，两者组合起来作为响应式编程，当数据动态变化时，UI层可以实时的更新。渐渐地，后端可以专注于api的开发，仅仅提供数据的检索和更新。事实上，工程师的经验水平可以从他区分何时以及为什么使用特定数据结构的能力中推断出来。

> Bad programmers worry about the code. Good programmers worry about **data structures and their relationships**.  
>
> — Linus Torvalds, Creator of Linux and Git

### 一、整体理解

&emsp;&emsp;粗劣的来划分的话，有三种类型的数据结构：

- 栈和队列的类数组的结构，和数组结构不同的是，他们的插入和删除数据上有所不同
- 链表、树和图是拥有节点的结构，并且，每个节点有对其他节点的指针
- 哈希表是通过哈希函数来定位和存储数据，一般来说，通过哈希表来索引，都会有较低的时间复杂度

&emsp;&emsp;从复杂性来看的话，队列和栈最简单，可以通过链表来构造，树和图最复杂，因为它们在链表的结构上进行了扩展，哈希表则需要这些数据结构来可靠地执行。

&emsp;&emsp;从时间效率上来看的话，链表最适合记录和存储数据，哈希表最适合检索数据，其时间效率很高。

### 二、类数组

#### 1. Stack

&emsp;&emsp;JavaScript中最重要的是调用堆栈，每当函数执行的时候，会把函数的作用域推入栈中。

&emsp;&emsp;编程方式上来说的话，栈是一个包含Pop和Push操作的数组结构：

- Push：增加元素到栈的顶端
- Pop：移除顶端的元素

&emsp;&emsp;栈结构遵循"后进先出"的原则(Last In First Out, LIFO)

```javascript
class Stack {
  constructor() {
    this.list = []
  }
  
  push(...item) {
    this.list.push(...item)
  }
  
  pop() {
   this.list.pop() 
  }
}
```

#### 2.Queue

&emsp;&emsp;**JavaScript是一种以事件驱动的编程语言，在浏览器内部，只有一个线程运行所有的JavaScript代码，JS使用时间循环来注册事件，那么为了支持单线程环境的异步性（节省CPU资源和增强web体验），回调函数只有在调用堆栈为空时才会退出队列并执行。**

> &emsp;&emsp;JavaScript是一种事件驱动的编程语言，它支持非阻塞操作。在浏览器内部，只有一个线程来运行所有的JavaScript代码，使用事件循环来注册事件，为了支持单线程环境中的异步性(为了节省CPU资源和增强web体验)，回调函数只有在调用堆栈为空时才会退出队列并执行。**Promise**依赖于这个事件驱动的体系结构，允许异步代码的“同步风格”执行，而不会阻塞其他操作。

&emsp;&emsp;编程方式上来看，Queue是只包含一个Unshift和Pop操作的数据结构：

- Unshift: 将数据项加入队列的末尾
- Pop: 将数组的顶部元素弹出

&emsp;&emsp;队列遵循"先进先出"的原则(First In First Out)

```javascript
class Queue {
  constructor() {
    this.list = []
  }
  
  enqueue(...item) {
    this.list.unshift(...item)
  }
  
  dequeue(){
    this.list.pop()
  }
}
```

### 三、链表、树和图

#### 1. Linked List

&emsp;&emsp;链表按照顺序来存储数据元素，链表不保存索引，而是保存指向其他数据项的指针。第一个节点为头节点，最后一个节点为尾节点。单链表中，每个节点只有指向下一个节点的指针，头部是每次检索开始的地方，每个节点还有指向前一个节点的指针，因此双链表可以从尾部向前检索。

&emsp;&emsp;如果需要查找或者编辑链表中的元素，可能需要遍历整个链表，相对于数组的索引方式，如果链表的长度足够长，则链表的索引方式，时间效率就较低。

&emsp;&emsp;有序链表和数组一样，单链表也可以作为堆栈来操作，只要让头部成为唯一可以插入和移除元素的地方。双链表也可以用作队列来操作，只要在尾部插入元素，在头部移除元素。**在数据量很大的情况下，链表实现队列的方法比数组的性能更好，因为数组的shift和unshift操作需要线性的时间在后续重新索引每一个元素。**

> 链表结构在客户端和服务端都是常用的。在客户端，像**Rudex**这样的状态管理库以链表的方式构建其中间件逻辑。当**action**被**dispatch**后，它们从一个中间件到另外一个中间件直到到达**ruducer**。在服务端，像**Express**这样的web框架也以类似的方式构造它的中间件逻辑,当一个**request**到达时，它会按顺序从一个中间件到另一个中间件，直到发出响应。

&emsp;&emsp;链表的简单实现：

```javascript
class LinkList {
  constructor() {
    this.head = null
  }
  
  // 当前节点
  find(value) {
    let curNode = this.head
    while (curNode.value !== value) {
      curNode = curNode.next
    }
    return curNode
  }
  
  // 前一节点
  findPrev(value) {
    let curNode = this.head
    while (curNode.next !== null && curNode.next.value !== value) {
      curNode = curNode.next
    }
    return curNode
  }
  
  insert(newValue, value) {
    const newNode = new Node(newValue)
    const curNode = this.find(value)
    newNode.next = curNode.next
    curNode.next = newNode
  }
  
  delete(value) {
    const preNode = this.findPrev(value)
    const curNode = preNode.next
    // 改变前一节点的指针
    preNode.next = preNode.next.next
    return curNode
  }
  
  class Node {
    constructor(value, next) {
      this.value = value
      this.next = null
    }
  }
}
```

#### 四、Hash表

#### 1. Hash Table

&emsp;&emsp;哈希表类似于字典结构，由键值对组成。每个对在内存中的地址有一个**哈希函数**确定，该函数接受一个key作为参数，并返回一个检索该对的内存地址。如果两个或者多个key转为相同的地址，则可能会发送冲突。为了健壮性，**getter和setter**应该预测这些事件，以确保所有数据都可以恢复，并且没有覆盖任何数据。

&emsp;&emsp;如果已经知道的地址是整数序列，可以简单地使用数组来存储键值对。对于更复杂的映射，我们可以使用**maps**或者**objects**, 哈希表的插入和查找元素的时间平均为常数，如果key表示地址，就不需要散列，一个简单的对象就足够了。哈希表实现键和值之间的简单对应，键和地址之间的简单关联，但是牺牲了数据之间的关系。所以，**哈希表在存储数据方面不是最优的**。

&emsp;&emsp;如果一个应用倾向于检索而不是存储数据，那么在查找、插入和删除方面，没有其他数据结构能够与哈希表的速度相匹配。因此哈希表被广泛应用也就不足为奇了。

> &emsp;&emsp;从数据库到服务端，再到客户端，哈希表尤其是哈希函数对应用程序的性能和安全方面是至关重要的。**数据库的查询**速度很大程度上依赖于指向记录的索引按顺序保存。这样，二进制搜索就可以在对数时间内完成，特别是对于**大的数据**来说，这是一个巨大的性能优势。

&emsp;&emsp;在客户端和服务端，许多流行的库都用缓存来最大程度提升性能。通过在哈希表中保存输入和输出的记录,对于相同的输入，函数仅运行一次。

> &emsp;&emsp;流行的**Reselect**库使用这种缓存策略来优化启动了**Redux**应用程序的**mapStateToProps**函数。实际上，JavaScript引擎还利用名为调用栈的哈希表存储所有我们创建的变量。这些变量可以通过调用栈上的指针被访问到。

> &emsp;&emsp;互联网本身也依赖于哈希算法来安全运行。互联网的结构是这样的：任何计算机都可以通过互相连接的web设备与其他计算机通信。每当一个设备登录到互联网上，它也可以成为一个路由器，数据流可以通过它进行传输。然而这是一把双刃剑。分散式架构意味着网络中的任何设备都可以监听并篡改它帮助转发的数据包。**MD5**和**SHA256**等哈希函数在防止中间人攻击方面发挥着关键作用。HTTPS上的电子商务之所以安全，只是因为使用了这些**散列函数**。

> &emsp;&emsp;从结构上看，**区块链**就是加密散列的二叉树单链表。哈希非常神秘，任何人都可以创建和更新一个财务交易数据库。曾经只有政府和中央银行才能做到的事情，现在任何人都可以安全地创造自己的货币!

&emsp;&emsp;一个简单的不做冲突处理的哈希表：

```javascript
class HashTable {
  constructor(size) {
    this.table = new Array(size)
  }
  
  // hash函数
  hash(key) {
    // 将字符串中每个字符的ASCII码值相加，再对数组的长度取余数
    let total = 0
    for (let i = 0; i < key.length; k ++) {
      total += key.charCodeAt(i)
    }
    return total % this.table
  }
  
  // 插入值
  insert(key, value) {
    const hashKey = this.hash(key)
    this.table[hashKey] = value
  }
  
  // 通过key去索引值
  get(key) {
    const hashKey = this.hash(key)
    if (!this.table[hashKey]) {
      return null
    }
    else {
      return this.table[hashKey]
    }
  }
  
  getAll() {
    const table = []
    for (let  i = 0; i < this.table.length; i ++) {
      if (this.table[i] != undefined) {
        table.push(this.table[i])
      }
    }
    return table
  }
}
```

### Summary

&emsp;&emsp;系统的逻辑层可能会越来越往前端方向靠，在不同的需求和应用环境下，不同的数据结构也有不同的效果。一些数据结构的存储方面很高效，一些是在搜索方面很高效。极端情况下，链表是存储的最佳选择，可以分为堆栈和队列。哈希表的搜索速度最快（常数时间）。树的结构性能在两者之间（对数时间），图表则可以描述复杂的结构。

### Reference

[1] [GitHub: JavaScript中的数据结构](https://github.com/lvwxx/blog/issues/1)

[2] [InterviewMap: 计算机通识—数据结构](https://yuchengkai.cn/docs/cs/dataStruct.html#栈)