# 数组

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

