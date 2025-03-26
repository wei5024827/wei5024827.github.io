## Python的所有类型

| Text Type:      | `str`                              |
| --------------- | ---------------------------------- |
| Numeric Types:  | `int`, `float`, `complex`          |
| Sequence Types: | `list`, `tuple`, `range`           |
| Mapping Type:   | `dict`                             |
| Set Types:      | `set`, `frozenset`                 |
| Boolean Type:   | `bool`                             |
| Binary Types:   | `bytes`, `bytearray`, `memoryview` |
| None Type:      | `NoneType`                         |

###  字符型String

- 用法

```python
b = "Hello, World!"
print(b[2:5]) # returns "llo"

b = "Hello, World!"
print(b[:5]) # returns "Hello"

a = " Hello, World! "
print(a.strip()) # returns "Hello, World!" 去掉空格

price = 59
txt = f"The price is {price:.2f} dollars"
print(txt)  # returns The price is 59.00 dollars
```
- 方法

| 方法             | 描述                                                   |
| ---------------- | ------------------------------------------------------ |
| `capitalize()`   | 将第一个字符转换为大写                                 |
| `casefold()`     | 将字符串转换为小写                                     |
| `center()`       | 返回一个居中的字符串                                   |
| `count()`        | 返回指定值在字符串中出现的次数                         |
| `encode()`       | 返回字符串的编码版本                                   |
| `endswith()`     | 如果字符串以指定值结尾，则返回 `true`                  |
| `expandtabs()`   | 设置字符串的制表符大小                                 |
| `find()`         | 在字符串中搜索指定值，并返回找到它的位置               |
| `format()`       | 在字符串中格式化指定值                                 |
| `format_map()`   | 在字符串中格式化指定值                                 |
| `index()`        | 在字符串中搜索指定值，并返回找到它的位置               |
| `isalnum()`      | 如果字符串中的所有字符都是字母数字，则返回 `True`      |
| `isalpha()`      | 如果字符串中的所有字符都在字母表中，则返回 `True`      |
| `isascii()`      | 如果字符串中的所有字符都是 `ASCII` 字符，则返回 `True` |
| `isdecimal()`    | 如果字符串中的所有字符都是十进制数，则返回 `True`      |
| `isdigit()`      | 如果字符串中的所有字符都是数字，则返回 `True`          |
| `isidentifier()` | 如果字符串是一个标识符，则返回 `True`                  |
| `islower()`      | 如果字符串中的所有字符都是小写，则返回 `True`          |
| `isnumeric()`    | 如果字符串中的所有字符都是数字，则返回 `True`          |
| `isprintable()`  | 如果字符串中的所有字符都是可打印的，则返回 `True`      |
| `isspace()`      | 如果字符串中的所有字符都是空白字符，则返回 `True`      |
| `istitle()`      | 如果字符串遵循标题规则，则返回 `True`                  |
| `isupper()`      | 如果字符串中的所有字符都是大写，则返回 `True`          |
| `join()`         | 将可迭代对象的元素连接到字符串的末尾                   |
| `ljust()`        | 返回一个左对齐的字符串版本                             |
| `lower()`        | 将字符串转换为小写                                     |
| `lstrip()`       | 返回一个左修剪的字符串版本                             |
| `maketrans()`    | 返回用于转换的转换表                                   |
| `partition()`    | 返回一个元组，字符串被分成三部分                       |
| `replace()`      | 返回一个字符串，其中指定的值被替换为指定的值           |
| `rfind()`        | 在字符串中搜索指定值，并返回找到它的最后一个位置       |
| `rindex()`       | 在字符串中搜索指定值，并返回找到它的最后一个位置       |
| `rjust()`        | 返回一个右对齐的字符串版本                             |
| `rpartition()`   | 返回一个元组，字符串被分成三部分                       |
| `rsplit()`       | 在指定的分隔符处拆分字符串，并返回一个列表             |
| `rstrip()`       | 返回一个右修剪的字符串版本                             |
| `split()`        | 在指定的分隔符处拆分字符串，并返回一个列表             |
| `splitlines()`   | 在换行符处拆分字符串并返回一个列表                     |
| `startswith()`   | 如果字符串以指定值开头，则返回 `true`                  |
| `strip()`        | 返回一个修剪过的字符串版本                             |
| `swapcase()`     | 交换大小写，小写变大写，反之亦然                       |
| `title()`        | 将每个单词的第一个字符转换为大写                       |
| `translate()`    | 返回一个翻译后的字符串                                 |
| `upper()`        | 将字符串转换为大写                                     |
| `zfill()`        | 在字符串开头填充指定数量的 `0` 值                      |

### 布尔型Booleans

- 方法

  ```python
  print(bool("Hello"))
  print(bool(15))
  ```

### 列表List  框括号

- 用法

  ```python
  thislist = ["apple", "banana", "cherry", "orange", "kiwi", "melon", "mango"]
  print(thislist[2:5]) ## returns ['cherry', 'orange', 'kiwi']
  
  thislist = ["apple", "banana", "cherry"]
  thislist[1:3] = ["watermelon"]
  print(thislist) ## returns ['apple', 'watermelon']
  
  thislist = ["apple", "banana", "cherry"]
  thislist.insert(2, "watermelon")
  print(thislist) # retruns ['apple', 'banana', 'watermelon', 'cherry']  insert(index,value) = list[2] insert value 
  
  thislist = ["apple", "banana", "cherry"]
  tropical = ["mango", "pineapple", "papaya"]
  thislist.extend(tropical)
  print(thislist) # retruns ['apple', 'banana', 'cherry', 'mango', 'pineapple', 'papaya']
  
  thislist = ["apple", "banana", "cherry", "banana", "kiwi"]
  thislist.remove("banana")
  print(thislist)
  
  thislist = ["apple", "banana", "cherry"]
  thislist.pop(1)
  print(thislist) # retruns ["apple", "banana"] pop() method removes the last item
  
  thislist = ["apple", "banana", "cherry"]
  [print(x) for x in thislist]
  """
  returns:
  apple
  banana
  cherry
  """
  
  fruits = ["apple", "banana", "cherry", "kiwi", "mango"]
  newlist = [x if x != "banana" else "orange" for x in fruits]
  print (newlist) #returns ['apple', 'orange', 'cherry', 'kiwi', 'mango']
  
  """
  newlist = [x if x != "banana" else "orange" for x in fruits] 相当于
  
  for x in fruits:
      if x != "banana":
          newlist.append(x)
      else:
          newlist.append("orange")
  """
  
  def myfunc(n):
    return abs(n - 50)
  
  thislist = [100, 50, 65, 82, 23]
  thislist.sort(key = myfunc)
  print(thislist) #returns [50, 65, 23, 82, 100]  参数 key = function 可以将list的每个元素带入function运算，并给运算后的值小到大排序，然后在给原列表排序
  
  
  ```
  
- 方法

  |    方法     |                            描述                            |
  | :---------: | :--------------------------------------------------------: |
  | `append()`  |                  在列表末尾添加一个元素。                  |
  |  `clear()`  |                   移除列表中的所有元素。                   |
  |  `copy()`   |                    返回列表的一个副本。                    |
  |  `count()`  |                 返回具有指定值的元素数量。                 |
  | `extend()`  | 将一个列表（或任何可迭代对象）的元素添加到当前列表的末尾。 |
  |  `index()`  |             返回具有指定值的第一个元素的索引。             |
  | `insert()`  |                  在指定位置添加一个元素。                  |
  |   `pop()`   |                    移除指定位置的元素。                    |
  | `remove()`  |                    移除具有指定值的项。                    |
  | `reverse()` |                   反转列表中元素的顺序。                   |
  |  `sort()`   |                      对列表进行排序。                      |

​	 

### 元组Tuple  圆括号

- 用法

   ```python
   thistuple = ("apple", "banana", "cherry", "orange", "kiwi", "melon", "mango")
   print(thistuple[2:5]) #returns ('cherry', 'orange', 'kiwi')
   
   
   #如果想对tuple进行数值操作，需先转为list，对list进行操作，再转回tuple
   thistuple = ("apple", "banana", "cherry")
   y = list(thistuple)
   y.append("orange")
   thistuple = tuple(y) #returns ("apple", "banana", "cherry","orange")
   
   
   #解包
   fruits = ("apple", "banana", "cherry", "strawberry", "raspberry")
   
   (green, yellow, *red) = fruits
   
   print(green)  #returns apple
   print(yellow) #returns banana
   print(red)	#returns ["cherry", "strawberry", "raspberry"]
   

- 方法

  |   方法    |                        描述                        |
  | :-------: | :------------------------------------------------: |
  | `count()` |           返回指定值在元组中出现的次数。           |
  | `index()` | 在元组中搜索指定的值，并返回其找到的位置（索引）。 |



### 集合set  花括号

- 用法

  ```python
  # 不重复的
  thisset = {"apple", "banana", "cherry", "apple"}
  print(thisset)
  
  # true 和 1是一个值
  thisset = {"apple", "banana", "cherry", True, 1, 2}
  print(thisset) #return {True, 2, 'apple', 'cherry', 'banana'}
  
  
  #update可以将另一个集合叠加到当前集合 经验证，数组，元组，字典也可
  thisset = {"apple", "banana", "cherry"}
  tropical = {"pineapple", "mango", "papaya"}
  thisset.update(tropical)
  print(thisset)
  
  
  # remove() 和discard() 区别，remove碰到找不到的元素会返回报错，discard不会
  
  
  #join
  set1 = {"a", "b", "c"}
  set2 = {1, 2, 3}
  
  set3 = set1 | set2
  print(set3)
  ```

- 方法

  |              方法               | 快捷键 |                             描述                             |
  | :-----------------------------: | :----: | :----------------------------------------------------------: |
  |             `add()`             |        |                    向集合中添加一个元素。                    |
  |            `clear()`            |        |                    移除集合中的所有元素。                    |
  |            `copy()`             |        |                     返回集合的一个副本。                     |
  |         `difference()`          |  `-`   |           返回包含两个或多个集合之间差异的新集合。           |
  |      `difference_update()`      |  `-=`  |        移除此集合中同时存在于另一个指定集合中的元素。        |
  |           `discard()`           |        |       移除指定的元素。如果元素不存在，则不会引发错误。       |
  |        `intersection()`         |  `&`   | 返回两个集合的交集，即同时存在于这两个集合中的元素组成的新集合。 |
  |     `intersection_update()`     |  `&=`  | 移除此集合中不存在于其他指定集合中的元素，使本集合成为这些集合的交集。 |
  |         `isdisjoint()`          |        | 判断两个集合是否没有交集。如果两个集合没有共同元素，则返回 `True`，否则返回 `False`。 |
  |          `issubset()`           |  `<=`  | 判断本集合是否是另一个集合的子集，即本集合中的所有元素是否都存在于另一个集合中。如果 `other` 包含所有本集合的元素，则返回 `True`。 |
  |                                 |  `<`   | 判断本集合是否是另一个集合的真子集，即本集合是另一个集合的子集且两者不相等。如果本集合是 `other` 的真子集，则返回 `True`。 |
  |         `issuperset()`          |  `>=`  | 判断本集合是否是另一个集合的超集，即另一个集合中的所有元素是否都存在于本集合中。如果本集合包含 `other` 的所有元素，则返回 `True`。 |
  |                                 |  `>`   | 判断本集合是否是另一个集合的真超集，即本集合是另一个集合的超集且两者不相等。如果本集合是 `other` 的真超集，则返回 `True`。 |
  |             `pop()`             |        | 移除并返回集合中的任意一个元素。如果集合为空，则会引发 `KeyError`。 |
  |           `remove()`            |        |    移除指定的元素。如果元素不存在，则会引发 `KeyError`。     |
  |    `symmetric_difference()`     |  `^`   | 返回两个集合的对称差集，即只存在于其中一个集合中的元素组成的新集合。 |
  | `symmetric_difference_update()` |  `^=`  | 将本集合更新为与另一个集合的对称差集，即移除两个集合中共有的元素，并添加只存在于其中一个集合中的元素。 |
  |            `union()`            |   \|   |                返回一个包含集合的并集的集合。                |
  |           `update()`            |  \|=   |           使用此集合与其他集合的并集来更新此集合。           |

### 字典 dict 花括号

- 用法

```python
thisdict = {
  "brand": "Ford",
  "model": "Mustang",
  "year": 1964
}
# 获取值
x = thisdict["model"]
x = thisdict.values()
# 获取键
x = thisdict.keys()
# 修改值 
thisdict.update({"year": 2020})
# 添加值
thisdict.update({"color": "red"})
# 删除值
thisdict.pop("model")
thisdict.popitem()
thisdict.clear() #清空dict

```

- 方法

  |     方法     |                          描述                          |
  | :----------: | :----------------------------------------------------: |
  |   clear()    |                  移除字典中的所有元素                  |
  |    copy()    |                   返回字典的一个副本                   |
  |  fromkeys()  |              返回一个具有指定键和值的字典              |
  |    get()     |                     返回指定键的值                     |
  |   items()    |       返回一个列表，其中每个键值对以元组形式存在       |
  |    keys()    |              返回一个包含字典所有键的列表              |
  |    pop()     |                  移除具有指定键的元素                  |
  |  popitem()   |                  移除最后插入的键值对                  |
  | setdefault() | 返回指定键的值。如果键不存在：插入该键，并赋予指定的值 |
  |   update()   |                 用指定的键值对更新字典                 |
  |   values()   |                 返回字典中所有值的列表                 |

