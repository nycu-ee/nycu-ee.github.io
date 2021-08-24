---
layout: post
title: Python Note And Some Useful Tips
categories: Dev
tags: [beginner, python]
---
# python筆記

動態類型, 不用聲明, 變量類型可以隨時改變.

是一個oop的語言.

<!-- more -->

### 數據類型

#### basic type 

- **int/ float/complex** 
- **str**
- **bool**

#### container

- **list/tuple**
- **dict/ set**

dict是用來存儲鍵值對結構的數據的，set其實也是存儲的鍵值對，只是默認鍵和值是相同的。

Python中的dict和set都是通過散列表來實現的

tuple 、int 、 str are immutable and called by value.

 list、dict are mutable and called by reference。

list 的方法有: insert、remove、slice、index、interate。

#### range

range($x$) 產生一個0到的 range object.`list(range(10))`

index是 左閉右開的. 比如`list(range(1,11))` 從1到10

TypeError: 'int' object is not subscriptable此報錯一般是在整數上加了下標：

#### list

list沒泛型，leetcode的List有

```python
list中加入tuple
res += (i, j)是不對的, 就是加了兩個int
res.append((i, j)) correct
xy = (i, j)
res.append(xy) correct

遍歷list
for i in list

初始化list
li = [i for i in range(8)]
list中find查找: if a in list :就可以了.
找有幾個dog:flashcard_list.count('dog')
```

負索引表示從末尾開始，-1 表示最後一個項目，-2 表示倒數第二個項目

```python
list 中元素個數 : len(prices)

獲得最後一個
print(list1[-1])

刪除:
list1.remove("banana")remove方法只會刪除掉該元素在列表中第一次出現的位置
list1.pop()有insert方法可以直接在對應下標處插入元素，pop方法也可以帶參數使用，從而刪除指定下標處的元素
del thislist[0]
del thislist

複製:
mylist = list(thislist)
mylist = thislist.copy()

追加
您可以使用 extend() 方法，其目的是將一個列表中的元素添加到另一列表中：

表示棧
st.append(str)
res += st.pop()
```

##### 錯誤

1 : Shadows built-in name 'list'

意思是你的你的變量名起的不好；最好要具體有意思，不要太隨意，起像str、list、len等太隨意的名字。

#### dict

所有mutable object是不能做key的.

```python
大括號來產生一個dict
例如 band = {'drum': 'saya' , 'vocal' : 'kani'}
get 也可以用[],但是如果用字典里沒有的鍵訪問數據，會輸出錯誤
dict['drum'] = "joe" # 更新
dict['guitar'] = "peter" # 添加

判斷python字典中key是否存在
band.has_key('name')
'name' in band.keys() 除了使用in還可以使用not in，判定這個key不存在

遍歷 dict
for key in dict: 或者 for key in dict.keys():
for value in dict.values():
for key,value in dict.items():
    
刪除元素
pop(key[,default])key: 要刪除的鍵值default: 如果沒有 key，返回 default 值
del dict['Name'] # 刪除鍵是'Name'的條目

找最大值
max(m.values())

統計list成dict
freq = collections.Counter(tasks)
freq = Counter([0])
```

##### defaultdict類

除了接受類型名稱作為初始化函數的參數之外，還可以使用任何不帶參數的可調用函數，到時該函數的返回結果作為默認值，這樣使得默認值的取值更加靈活。

```python
from collections import defaultdict
>>> def zero():
... return 0
>>> dd = defaultdict(zero)
>>> dd['foo']
0
接受類型名稱作為初始化函數的參數
freq = defaultdict(int)
freq[0] =1
```

#### tuple

不可變的序列

#### set

```python
可以使用大括號 { } 或者 set() 函數創建集合，注意：創建一個空集合必須用 set() 而不是 { }，因為 { } 是用來創建一個空字典。
>>> thisset = set(("Google", "Amazon", "Microsoft"))
>>> thisset.update({1,3})
{1, 3, 'Google', 'Amazon', 'Microsoft'}
>>> thisset.update([1,4],[5,6])
{1, 3, 4, 5, 6, 'Google', 'Taobao', 'Runoob'}
或者可以thisset.add("Facebook")
s.remove( x )如果元素不存在，則會發生錯誤
```

#### 優先隊列

`heapq`是二叉堆，通常用普通列表實現`heapq`模塊是在Python中不錯的優先級隊列實現。由於heapq在技術上只提供最小堆實現，因此必須添加額外步驟來確保排序穩定性，以此來獲得“實際”的優先級隊列中所含有的預期特性。

```python
import heapq
q = []
heapq.heappush(q, (2, 'code'))
heapq.heappush(q, (1, 'eat'))
heapq.heappush(q, (3, 'sleep'))
while q:
next_item = heapq.heappop(q)
print(next_item)
# 結果：
# (1, 'eat')
# (2, 'code')
# (3, 'sleep')

from queue import PriorityQueue as PQ
q = PriorityQueue()
>>> q.put((2, "Lisa"))
>>> q.put((1, "Lucy"))
>>> q.put((0, "Tom"))
The lowest valued entries are retrieved first
與 heapq 模塊不同的是，PriorityQueue 是基於類實現的，其提供的操作是同步的，提供鎖操作，支持併發的生產者和消費者。
Queue objects (Queue, LifoQueue, or PriorityQueue) provide the public methods described below.
Queue.get(block=True, timeout=None)
Remove and return an item from the queue.
Queue.put(item, block=True, timeout=None)
Put item into the queue.
```

#### deque

```python
from collections import deque
d = deque(['a','b','c','d','e','f'])
d.extendleft
如果使用deque進行切片的話會拋出異常,比如print(d[:-1])不行
print(dq.count(1))
計算隊列元素的個數是否等於1個，假設大於或等於都返回True。否則返回False
count不能用來求deque元素個數, 要用len
```

#### array

```python
array.index(x)
# 方法返回x 在數組中第一次出現的下標, 下標從零開始,如果沒有找到該元素會報異常.
ValueError: array.index(x): x not in list
其實這個沒啥用, 因為只能一維, 一般都用二維的 np.array
```

#### for/while loop

在for循環內修改i值，只會對當前一次的循環體內有效

跳躍的話, 要使用 while 替換 for

#### sort

```python
# 降序
vowels.sort(reverse=True)

a = [('b', 4), ('a', 12), ('d', 7), ('h', 6), ('j', 3)]
a.sort(key=lambda x: x[0])
list.sort(key=lambda x: (key1, key2))
```

### typing 數據類型

collections是Python內建的一個集合模塊，提供了許多有用的集合類。

### typing模塊的作用

- 類型檢查，防止運行時出現參數和返回值類型不符合。
- 作為開發文檔附加說明，方便使用者調用時傳入和返回參數類型。
- 該模塊加入后並不會影響程序的運行，不會報正式的錯誤，只有提醒。

- 在傳入參數時通過"參數名:類型"的形式聲明參數的類型
- 返回結果通過"-> 結果類型"的形式聲明結果的類型。

### 運算符

- 沒有++、--
- 沒有? : (conditional operator)
- 可以用兩個乘表示平方, 兩個除表示整除
- 可以用and 、or
- in 判斷名字是否存在list之中
- is 判斷是否為同一個對象
- is和 == 不同
- pass //還沒想好寫啥, 先pass
- for-in for語句不需要int i 變量

- `for it in s` 類似於 cpp中的 `for(auto it : s)`可以同時返回多個值.

### 類

```python
class Circle:
    
def __init__(self,v):
	self.__value=v
def getArea(self):
	return 3.1415926*self.__value**2
def getPerimeter(self):
	return 3.1415926*self.__value*2

c=Circle(5)
```

1. np.where(condition,x,y) 當where內有三個參數時，第一個參數表示條件，當條件成立時where方法返回x，當條件不成立時where返回y
2. np.where(condition) 當where內只有一個參數時，那個參數表示條件，當條件成立時，where返回的是每個符合condition條件元素的坐標,返回的是以元組的形式.

#### eq怎麼用?

```python
print(cat_1.__eq__(cat_2))
```

#### == 運算符是比較哪些?

- `is`比較的是兩個整數對象的id值是否相等，也就是比較兩個引用是否代表了內存中同一個地址。
- `==`比較的是兩個整數對象的內容是否相等，使用`==`時其實是調用了對象的`__eq__()`方法。

對於整數對象，Python把一些頻繁使用的整數對象緩存起來，保存到一個叫small_ints的鏈表中。在Python的整個生命周期內，任何需要引用這些整數對象的地方，都不再重新創建新的對象，而是直接引用緩存中的對象。Python把頻繁使用的整數對象的值定在[-5, 256]這個區間。如果需要這個範圍的整數，就直接從small_ints中獲取引用而不是臨時創建新的對象。因為大於256或小於-5的整數不在該範圍之內，所以就算兩個整數的值是一樣，但它們是不同的對象。

所以python會顯示: `257 is not 257`

通過比較它的b屬性建立堆排序(heap soft):

```python
def __lt__(self, other):
    if self.b :
    	return True
a = P(3,1)
b = P(2,3)
c = P(10,0)
d = P(3,1)

h = []
heapq.heappush(h,a)
heapq.heappush(h,b)
heapq.heappush(h,c)
heapq.heappop(h)
就會把10,0 排在第一個,彈出
```

#### 類內方法

因為類裡面調用屬性需要先加實例化，那是不是寫**Chinese().name**?是的，這樣寫沒有錯，但是我們沒必要這樣寫。我們上面說過self就是類的實例化，所以我們寫成**self.name** 就可以調用屬性了。類的屬性調用前面加**self.屬性名**就可以了。self在類中就是Chinese()，我們完全可以把全部的self寫成Chinese()，傳參時也不會傳給他。



寫了self就隔離開,不寫就可以通用? 

為啥n可以傳入sum不行? 因為n是比較, sum不能在類內改變.

```pseudocode
def waysToBuildRooms(self, prevRoom: List[int]) -> int:
n = len(prevRoom) #寫了self就隔離開,不寫就可以通用
sum = 0
def dfs(num:int) -> None:
if num == n:
sum +=1
return
```

綜上，所以我們說self代表的是類的實例本身，方便數據的流轉。對此，我們需要記住兩點：

1. 只要在類中用def創建方法時，就必須把第一個參數位置留給 self，並在調用方法時忽略它（不用給self傳參）。
2. **：當在類的方法內部想調用類屬性或其他方法時，就要採用self.屬性名或self.方法名的格式。**

接下來我們說說類中的初始化

定義初始化方法的格式是def \_\_init\_\_(self)，是由init加左右兩邊的【雙】下劃線組成（ initialize “初始化”的縮寫）。

初始化方法的作用在於：實例對象創建時，該方法內的代碼無須調用就會自動運行。

### 矩陣

TypeError: list indices must be integers or slices, not tuple

在取矩陣某一列時會出現報錯,這是因為此時矩陣存儲在列表(list)中，而列表中的每一個元素大小可能不同，因此不能直接取其某一列進行操作

可以利用`numpy.array`函數將其轉變為標準矩陣，再對其進行取某一列的操作：

```python
matrix = [[0, 1, 2], [3, 4, 5]]
matrix = numpy.array(matrix)
vector = matrix[:, 0]
print(vector)
```

運行時處理的時候把self.cx賦成list或者array 非常容易出錯!!!

### 切片

```python
>>> L[-2:] 后兩個數
['Bob', 'Jack']

>>> L[-2:-1]
['Bob']


>>> L[:10:2] 前10個數，每兩個取一個：
[0, 2, 4, 6, 8]

>>> L[::5] 所有數，每5個取一個：
L[::-1] 反轉

childs.append(curr_state[:idx - 1] + curr_state[idx:idx + 1] + curr_state[idx - 1:idx] + curr_state[idx + 1:])
兩行交換, 越界了也不會報錯.
交換二維list中兩個元素,和np中array不一樣.
curr_state.state[:row] + [
curr_state.state[row][:col] + curr_state.state[row + 1][col:col + 1] + curr_state.state[row][col + 1:]] + [curr_state.state[row + 1][:col] + curr_state.state[row][col:col + 1] + curr_state.state[row + 1][ col + 1:]] + curr_state.state[row + 2:]
```

### 垃圾回收

python採用的是引用計數機制為主，標記-清除和分代收集（隔代回收）兩種機制為輔的策略。

PyObject是每個對象必有的內容，其中ob_refcnt就是做為引用計數。當一個對象有新的引用時，它的ob_refcnt就會增加，當引用它的對象被刪除，它的ob_refcnt就會減少。

#### **導致引用計數+1的情況**

- 對象被創建，例如a = 23
- 對象被引用，例如b = a
- 對象被作為參數，傳入到一個函數中，例如`func(a)`
- 對象作為一個元素，存儲在容器中，例如`list1=[a,a]`

#### **導致引用計數-1的情況**

- 對象的別名被顯式銷毀，例如`del a`
- 對象的別名被賦予新的對象，例如`a = 24`
- 一個對象離開它的作用域，例如:func函數執行完畢時，func函數中的局部變量（全局變量不會）
- 對象所在的容器被銷毀，或從容器中刪除對象

#### **分代回收**

- 分代回收是一種以空間換時間的操作方式，Python將內存根據對象的存活時間劃分為不同的集合，每個集合稱為一個代，Python將內存分為了3“代”，分別為年輕代（第0代）、中年代（第1代）、老年代（第2代），他們對應的是3個鏈表，它們的垃圾收集頻率隨着對象存活時間的增大而減小。
- 新創建的對象都會分配在**年輕代**，年輕代鏈表的總數達到上限時，Python垃圾收集機制就會被觸發，把那些可以被回收的對象回收掉，而那些不會回收的對象就會被移到**中年代**去，依此類推，**老年代**中的對象是存活時間最久的對象，甚至是存活於整個系統的生命周期內。
- 同時，分代回收是建立在標記清除技術基礎之上。分代回收同樣作為Python的輔助垃圾收集技術處理那些容器對象

#### 交換

Python中沒有swap()函數,交換兩個數的方式

```python
a,b = b,a
```

#### pycharm tips

pycharm 一鍵註釋: ctrl +/

pycharm無法最大化, pycharm最小化打不開。

解決方法: 重裝pycharm也不行, 換個項目就可以了。

#### numpy庫

```python
np.zeros(shape=(4, 4))
x.shape
x = np.array([[1, 2, 3], [4, 5, 6]], np.int32)
y = x[:,1] 就是array([2, 5])
y[0] = 9 # this also changes the corresponding element in x

y
array([9, 5])

x
array([[1, 9, 3],[4, 5, 6]])

x.sum(axis=0)
```

### 讀取文件夾

```python
import string
import os

for root, dirs, files in os.walk("./data/"): # os.walk會該目錄下的所有文件
print(files)

for file in files:
name = file.split("_")
score = float(name[0])
print(score)
```

### 字符串

```python
str = "https://www.google.com/pdf/abcdefg.pdf"

# 把字符串分割:
print(str.split('/'))
>>>['https:', '', 'www.google.com', 'pdf', 'abcdefg.pdf']

# 輸出第一段字符串,>>>https:
print(str.split('/')[0])

#合併字符
" ".join(["A","B","C","D"])
'A B C D'

# 翻轉字符串三種方法:
str='Google'
print(str[::-1])
str='Google'
print(''.join(reversed(str)))
str='Google'
from functools import reduce
print(reduce(lambda x, y: y + x, str)) #strip() It returns a new string after removing any leading and trailing whitespaces including tabs (\t).

rstrip(): 去除右邊空格
    
排序:
s="abxc"
l1=list(s) #['a', 'b', 'x', 'c']
l1.sort() #['a', 'b', 'c', 'x']
s1="".join(l1) #'abcx'
str = '128-312-156'
char_ = '-'
# 從頭開始找第一個匹配的字符位置:
nPos = str.find(char_ )
print(nPos)# 輸出 3

# 從尾開始找第一個匹配的字符位置:
nPos = str.rfind(char_ )

# 轉ascii碼:
int()方法將字符轉換成ASCII碼
可以使用ord()函數和chr()函數進行ASCII碼轉換。
```

#### 報錯

python報錯: Non-ASCII character '\xe5'

解決方法：在Python源文件的最開始一行，加入一句：

coding=UTF-8 或者 -*- coding:UTF-8 -*-

python報錯: "IndentationError: unexpected indent"的兩三個解決方法

這個是縮進錯誤，我們可以通過下面幾步解決他：
首先檢查代碼是不是有錯誤的索引。
如果沒有，全都正確，可以看看是不是使用'''進行了整段的註釋，如果是，一定要保證其與上下相鄰代碼縮進一致，而#就無所謂。
如果還有錯，使用notepad++打開文件，選擇視圖->顯示符號->顯示空格和製表符，然後查看是不是有空格與製表符混用的情況。

vim可以用: set list 顯示空格和製表符.
unexpected indent 就是說“n”是一個“意外的”縮進。也就是說，這裡的問題就是指“n”是一個意外的縮進。通過查看源代碼可知這裡的確是縮進了一個字符位。
據此推斷，我們把這句話的縮進取消，也就是頂格寫，

python報錯: AttributeError: object 'L2Cache' has no attribute 'connectCPUSideBus'

(C++ object is not yet constructed, so wrapped C++ methods are unavail)
對象“l2cache”沒有屬性 ,很多是說不要用跟系統庫同樣名字,這裡則是因為之前的頂格寫,導致沒有定義到class中去.

python報錯: TypeError: super(type, obj): obj must be an instance or subtype of type

```python
class FooChild(FooParent):
def __init__(self):
super(FooChild,self)
```

#首先找到 FooChild 的父類（就是類 FooParent），然後把類 FooChild 的對象轉換為類 FooParent 的對象

python報錯: TypeError: 'type' object is not subscriptable

該對象是不可進行下標操作的.NameError: name 'List' is not defined

#### Sccons

Scons是一個開放源碼、以Python語言編碼的自動化構建工具，可用來替代make編寫複雜的makefile。並且scons是跨平台的，只要scons腳本寫的好，可以在Linux和Windows下隨意編譯。
在Java的集成開發環境中，比如Eclipse、IDEA中，有常常有三種與編譯相關的選項Compile、Make、Build三個選項。這三個選項最基本的功能都是完成編譯過程。但又有很大的區別，區別如下：

1. Compile：只編譯選定的目標，不管之前是否已經編譯過。
2. Make：編譯選定的目標，但是Make只編譯上次編譯變化過的文件，減少重複勞動，節省時間。（具體怎麼檢查未變化，這個就不用考慮了，IDE自己內部會搞定這些的）
3. Build：是對整個工程進行徹底的重新編譯，而不管是否已經編譯過。Build過程往往會生成發布包，這個具體要看對IDE的配置了，Build在實際中應用很少，因為開發時候基本上不用，發布生產時候一般都用ANT等工具來發布。Build因為要全部編譯，還要執行打包等額外工作，因此時間較長。