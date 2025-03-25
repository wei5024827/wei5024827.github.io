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

###  string

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

### Booleans

- 方法

  ```python
  print(bool("Hello"))
  print(bool(15))
  ```

### Lists

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
  
  
  
  
  ```

  

