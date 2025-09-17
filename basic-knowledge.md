# 数组

数组是一块连续的内存空间，然后数组名就是这个内存空间的首地址，通过索引的方式可以查找数组中对应的元素

==动态数组的实现==

```python
class myarraylist:
    INIT_CAP = 1

    def __init__(self,init_capacity = None):
        self.data = [None] * (init_capacity if init_capacity is None else INIT_CAP)
        self.size = 0

    def add_last(self,e):
        #先获取当前数组的长度
        cap = len(self.data)
        #比较有效元素个数和数组长度
        if(self.size == cap):
            self._resize(2 * len(self.data))#扩容
        self.data[self.size] = e
        #因为size是当前有效元素的个数（0->size-1）所以新添加的元素的索引是size
        self.size += 1
    
    def _resize(self,newcapacity):
        #创建一个新数组
        temp = [None] * newcapacity
        #把原始数组复制到现在的数组
        for i in range(self.size):
            temp[i] = self.data[i]
        #让self.data指向新数组
        self.data = temp

    def _is_position_index(self,index):
        return (0<=index<=self.size)
    
    def _is_element_size(self,index):
        return (0<=index<=self.size)
        
    def _check_position_index(index):
        #用于检查当前index是否超出了有效添加的范围
        if not self._is_position_index(index):
            raise IndexError(f"Index:{index},Size:{self.size}")

    def _check_element_index(index):
        #这个是用于检查在查询等时候是否在有效元素范围内
        if not self._is_element_index(index):
            raise IndexError(f"Index:{index},Size:{self.size}")

    def add(self,index,e):
        #检查我要加入的位置是否是一个有效位置
        self._check_position_index(index)

        #检查加入元素之后，数组的大小是否合适
        cap = len(self.data)
        if(cap == self.size):
            self._resize(2 * self.size)

        #这个时候，由于是在随机位置（index）添加元素，我要把index这个索引位置后的元素都向后推移一个位置
        #在向后推移的过程中，要先把后面的元素复制到更后面的位置，防止元素被覆盖
        #在循环的时候直接从最后一个元素开始，到原本index的位置，但是range循环中第二位是不包括的所以到index-1
        for i in range(self.size-1,index-1,-1):
            self.data[i+1] = self.data[i]

        self.data[index] = e

        self.size  += 1
    
    def add_first(self,e)
        self.add(0,e)
    
    def remove_last(self):
        if self.size == 0:
            raise Exception("NoSuchElementException")

        cap = len(self.data)
        if (cap//4 > self.size):
            self._resize(cap//2)
        
        deleted_val = self.data[self.size-1]
        self.data[self.size-1] = None
        self.size -= 1

        return deleted_val
    
    def remove(self,index):
        self._check_element_position(index)

        cap = len(self.data)

        if(cap//4 > self.data):
            self._resize(cap//2)
        
        deleted_val = self.data[index]

        for i in range(index,self.size):
            self.data[i] = self.data[i+1]
        
        self.data[self.size-1] = None

        self.size -= 1

        return deleted_val

    def remove_first(self):
        return self.remove(0)
        #在这里出现了函数中调用函数的问题，函数与函数之间的信息是如何传递的呢？
        #remove（0）时会return一个deleted_val，在python中函数返回值不会直接返回实际内容，而是一个内存地址，这个内存地址指向函数内具体计算出的内容
        #当remove_first调用remove（0），需要这个返回结果时，remove函数的结果会存在CPU寄存器（如RAX），然后remove_first会从寄存器中找到这个存着的内存地址，然后去heap当中寻找对应的实际计算结果

    def get(self,index):
        self._check_element_index(index)

        return self.data[index]

    def set(self,index,e):
        self._check_element_index(index)

        old_val = self.data[index]
        self.data[index] = e

        return old_val

    def display(self):
        print(f"size={self.size},cap={len(self.data)}")
        print(self.data)

if __name__ == "main":
    arr = myarraylist(init_capacity = 3)
    
    for i in tange(1,6):
        arr.add_lkast(i)
    
    arr.remove(3)
    arr.add(1,9)
    arr.add_first(100)
    val = arr.remove_last()

    for i in range(self.size):
        print(arr.get(i))


```

# 链表

==单链表==

```python
class ListNode:
    def __init__(self,input):
        self.val = input
        self.next = None

class Node:
    def __init__(self,prev,element,next):
        self.val = element
        self.next = next
        self.prev = prev
```

链表不需要像数组那样分配连续的内存空间，通过next和prev两个指针将散落在内存空间中的存储内容链接在一起

```python
       
    #单链表的基本操作
class ListNode:
    def __init__(self,x):
        self.val = x
        self.next = None
    
    #输入数组，输出单链表
    def createLinkedList(arr:'List[int]') -> 'ListNode':
        if arr is None or len(arr) == 0:
            return None
        
        head = Listnode(arr[0])
        cur = head
        for i in range(i,len(arr)):
            cur = ListNode(arr[i])
            cur = cur.next

        return head
    

    def add_first(self,e,head):
        newNode = ListNode(e)
        newNode.next = head
        head = newNode
    
    def add_last(self,e,head):
        newNode = ListNode(e)

        p = head

        while p.next is not None :
            p = p.next
        
        p.next = newNode
    
    def add(self,e,head,index):
        newNode = ListNode(e)

        self._check_position_index(index)

        p = head 

        for i in range(index):
            p = p.next

        newNode.next = p.next
        p.next = newNode

    
    def remove(self,index,head):
        self._check_position_index(index)

        p = head

        for i in range(index):
            p = p.next
        
        p = p.next.next
```

```python
#doublyList basic operations

class DoublyListNode:
    def __init__(self, x):
        self.val = x
        self.next = None
        self.prev = None
        
def createDoublyLinkedList(arr: List[int]) -> Optional[DoublyListNode]:
    if not arr:
        return None
    
    head = DoublyListNode(arr[0])
    cur = head
    
    # for 循环迭代创建双链表
    for val in arr[1:]:
        new_node = DoublyListNode(val)
        cur.next = new_node
        new_node.prev = cur
        cur = cur.next
    
    return head

    # 创建一条双链表
head = create_doubly_linked_list([1, 2, 3, 4, 5])

# 在双链表头部插入新节点 0
new_head = DoublyListNode(0)
new_head.next = head
head.prev = new_head
head = new_head
# 现在链表变成了 0 -> 1 -> 2 -> 3 -> 4 -> 5


# 创建一条双链表
head = createDoublyLinkedList([1, 2, 3, 4, 5])

# 删除第 4 个节点
# 先找到第 3 个节点
p = head
for i in range(2):
    p = p.next

# 现在 p 指向第 3 个节点，我们将它后面的那个节点摘除出去
toDelete = p.next

# 把 toDelete 从链表中摘除
p.next = toDelete.next
toDelete.next.prev = p

# 把 toDelete 的前后指针都置为 null 是个好习惯（可选）
toDelete.next = None
toDelete.prev = None

# 现在链表变成了 1 -> 2 -> 3 -> 5

```

MyLinkedList代码实现

1. 同时持有头尾节点的引用
2. 虚拟头尾节点：
    创建一个虚拟头节点和一个虚拟尾节点，无论双链表是否为空，这两个节点都存在；这样就不会有空指针
3. 防止内存泄漏


```python
class Node:
    def __init__(self,val):
        self.val = val
        self.next = None
        self.prev = None
    

class MyLinkedList:
    #virtual head and tail node
    def __init__(self):
        self.head = Node(None)
        self.tail = Node(None)
        self.head.next = self.tail
        self.tail.prev = self.head
        self.size = 0
    
    # add element
    def add_last(self,e):
        x = Node(e)
        
        temp = self.tail.prev
        temp.next = x
        x.prev = temp

        self.tail.prev = x
        x.next = self.tail

        self.size += 1
    
    def add_first(self,e):
        x = Node(e)

        temp = self.head.next
        temp.next = x
        x.prev = temp

        self.head.prev = x
        x.prev = self.head


    def add(self, index, element):
        self.check_position_index(index)
        if index == self.size:
            self.add_last(element)
            return

        # 找到 index 对应的 Node
        p = self.get_node(index)
        temp = p.prev
        # temp <-> p

        # 新要插入的 Node
        x = Node(element)

        p.prev = x
        temp.next = x

        x.prev = temp
        x.next = p

        # temp <-> x <-> p

        self.size += 1

    # ***** 删 *****

    def remove_first(self):
        if self.size < 1:
            raise IndexError("No elements to remove")
        # 虚拟节点的存在是我们不用考虑空指针的问题
        x = self.head.next
        temp = x.next
        # head <-> x <-> temp
        self.head.next = temp
        temp.prev = self.head

        # head <-> temp

        self.size -= 1
        return x.val

    def remove_last(self):
        if self.size < 1:
            raise IndexError("No elements to remove")
        x = self.tail.prev
        temp = x.prev
        # temp <-> x <-> tail

        self.tail.prev = temp
        temp.next = self.tail

        # temp <-> tail

        self.size -= 1
        return x.val

    def remove(self, index):
        self.check_element_index(index)
        # 找到 index 对应的 Node
        x = self.get_node(index)
        prev = x.prev
        next = x.next
        # prev <-> x <-> next
        prev.next = next
        next.prev = prev

        self.size -= 1

        return x.val

    # ***** 查 *****

    def get(self, index):
        self.check_element_index(index)
        # 找到 index 对应的 Node
        p = self.get_node(index)

        return p.val

    def get_first(self):
        if self.size < 1:
            raise IndexError("No elements in the list")

        return self.head.next.val

    def get_last(self):
        if self.size < 1:
            raise IndexError("No elements in the list")

        return self.tail.prev.val

    # ***** 改 *****

    def set(self, index, val):
        self.check_element_index(index)
        # 找到 index 对应的 Node
        p = self.get_node(index)

        old_val = p.val
        p.val = val

        return old_val

    # ***** 其他工具函数 *****

    def size(self):
        return self.size

    def is_empty(self):
        return self.size == 0

    def get_node(self, index):
        self.check_element_index(index)
        p = self.head.next
        # TODO: 可以优化，通过 index 判断从 head 还是 tail 开始遍历
        for _ in range(index):
            p = p.next
        return p

    def is_element_index(self, index):
        return 0 <= index < self.size

    def is_position_index(self, index):
        return 0 <= index <= self.size

    # 检查 index 索引位置是否可以存在元素
    def check_element_index(self, index):
        if not self.is_element_index(index):
            raise IndexError(f"Index: {index}, Size: {self.size}")

    # 检查 index 索引位置是否可以添加元素
    def check_position_index(self, index):
        if not self.is_position_index(index):
            raise IndexError(f"Index: {index}, Size: {self.size}")

    def display(self):
        print(f"size = {self.size}")
        p = self.head.next
        while p != self.tail:
            print(f"{p.val} <-> ", end="")
            p = p.next
        print("null\n")

if __name__ == "__main__":
    list = MyLinkedList()
    list.add_last(1)
    list.add_last(2)
    list.add_last(3)
    list.add_first(0)
    list.add(2, 100)

    list.display()
    # size = 5
    # 0 <-> 1 <-> 100 <-> 2 <-> 3 <-> null
        
```