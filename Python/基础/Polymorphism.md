### iterators

- 创建类作为迭代器，必须实现方法 \__iter\__() 和 \__next\__()

  - \__iter\__() 类似\__init\__()，须对迭代器类做初始化，返回时必须返回对象本身
  -  \__next\__() 返回序列中的下一项

  ```python
  # 创建一个从1开始，到指定上限的平方数迭代器
  class SquareNumbers:
      def __init__(self, max_num):
          self.max_num = max_num  # 设置上限
          self.current = 0        # 初始化当前值
          
      def __iter__(self):
          return self  # 必须返回迭代器对象本身
      
      def __next__(self):
          self.current += 1
          if self.current ** 2 > self.max_num:
              raise StopIteration  # 超过上限时停止迭代
          return self.current ** 2  # 返回当前数字的平方
  
  # 使用迭代器
  squares = SquareNumbers(100)  # 创建生成不超过100的平方数的迭代器
  
  for num in squares:
      print(num)  # 输出: 1 4 9 16 25 36 49 64 81 100
  
  # 也可以手动调用
  squares = SquareNumbers(25)
  iterator = iter(squares)
  print(next(iterator))  # 输出: 1
  print(next(iterator))  # 输出: 4
  print(next(iterator))  # 输出: 9
  ```

  

### 多态

- “多态性”一词的意思是“多种形式”，在编程中，它指的是方法/函数/运算符，这些方法/函数/运算符具有相同的名称，可以在许多对象或类上执行。

  ```python
  # 简单示例 len就是一个多态的表现形式
  x = "Hello World!"
  print(len(x))
  mytuple = ("apple", "banana", "cherry")
  print(len(mytuple))
  thisdict = {
    "brand": "Ford",
    "model": "Mustang",
    "year": 1964
  }
  print(len(thisdict))
  ```

  - 多态在类中的形式

    ```python
    class Vehicle:
      def __init__(self, brand, model):
        self.brand = brand
        self.model = model
    
      def move(self):
        print("Move!")
    
    class Car(Vehicle):
      pass
    
    class Boat(Vehicle):
      def move(self):
        print("Sail!")
    
    class Plane(Vehicle):
      def move(self):
        print("Fly!")
    
    car1 = Car("Ford", "Mustang")       #Create a Car object
    boat1 = Boat("Ibiza", "Touring 20") #Create a Boat object
    plane1 = Plane("Boeing", "747")     #Create a Plane object
    
    for x in (car1, boat1, plane1):
      print(x.brand)  #retruns Ford Ibiza  Boeing
      print(x.model)  #returns Mustang  Touring 20   747
      x.move()  #returns Move!  Sail!  Fly!
    ```

    

### 作用域

- 局部作用域： 只能在函数内部使用

- 全局作用域： 在任何范围都可以使用

  ```python
  x = 100
  def myfunc():
    print(x)
  myfunc()  #returns 100
  print(x)	#returns 100
  ```

- Global关键字：被卡在本地作用域内，但需要创建一个全局变量，则可以使用 global 关键字

  ```python
  def myfunc():
    global x
    x = 100
  myfunc()
  print(x)
  ```



### 模块

- 模块实质上是文件名.py

  使用方法示例:

  mymodule.py:

  ```python
  def greeting(name):
    print("Hello, " + name)
  
  person1 = {
    "name": "John",
    "age": 36,
    "country": "Norway"
  }
  ```

  file2.py

  ```python
  from mymodule import persion1
  
  print (person1["age"])
  ```

### 日期模块(datetime)

- strftime() : 用来获取格式化的日期

  | 指令 | 描述                            | 实例                     |
  | :--- | :------------------------------ | :----------------------- |
  | %a   | Weekday，短版本                 | Wed                      |
  | %A   | Weekday，完整版本               | Wednesday                |
  | %w   | Weekday，数字 0-6，0 为周日     | 3                        |
  | %d   | 日，数字 01-31                  | 31                       |
  | %b   | 月名称，短版本                  | Dec                      |
  | %B   | 月名称，完整版本                | December                 |
  | %m   | 月，数字01-12                   | 12                       |
  | %y   | 年，短版本，无世纪              | 18                       |
  | %Y   | 年，完整版本                    | 2018                     |
  | %H   | 小时，00-23                     | 17                       |
  | %I   | 小时，00-12                     | 05                       |
  | %p   | AM/PM                           | PM                       |
  | %M   | 分，00-59                       | 41                       |
  | %S   | 秒，00-59                       | 08                       |
  | %f   | 微妙，000000-999999             | 548513                   |
  | %z   | UTC 偏移                        | +0100                    |
  | %Z   | 时区                            | CST                      |
  | %j   | 天数，001-366                   | 365                      |
  | %U   | 周数，每周的第一天是周日，00-53 | 52                       |
  | %W   | 周数，每周的第一天是周一，00-53 | 52                       |
  | %c   | 日期和时间的本地版本            | Mon Dec 31 17:41:00 2018 |
  | %x   | 日期的本地版本                  | 12/31/18                 |
  | %X   | 时间的本地版本                  | 17:41:00                 |
  | %%   | A % character                   | %                        |



###  常见的模块及方法

- random模块
| 方法 | 描述 |
|------|------|
| `seed()` | 初始化随机数生成器 |
| `getstate()` | 返回随机数生成器的当前内部状态 |
| `setstate()` | 恢复随机数生成器的内部状态 |
| `getrandbits()` | 返回表示随机比特位的数字 |
| `randrange()` | 返回给定范围内的随机数 |
| `randint()` | 返回给定范围内的随机整数 |
| `choice()` | 从给定序列中返回随机元素 |
| `choices()` | 返回包含从给定序列中随机选取元素的列表 |
| `shuffle()` | 接收一个序列并返回其随机排序后的结果 |
| `sample()` | 返回序列的指定大小随机样本 |
| `random()` | 返回 0 到 1 之间的随机浮点数 |
| `uniform()` | 返回两个给定参数之间的随机浮点数 |
| `triangular()` | 返回两个给定参数之间的随机浮点数，可设置 mode 参数指定中间点 |
| `betavariate()` | 基于 Beta 分布返回 0 到 1 之间的随机浮点数（用于统计学） |
| `expovariate()` | 基于指数分布返回随机浮点数（用于统计学） |
| `gammavariate()` | 基于 Gamma 分布返回随机浮点数（用于统计学） |
| `gauss()` | 基于高斯分布返回随机浮点数（用于概率论） |
| `lognormvariate()` | 基于对数正态分布返回随机浮点数（用于概率论） |
| `normalvariate()` | 基于正态分布返回随机浮点数（用于概率论） |
| `vonmisesvariate()` | 基于冯·米塞斯分布返回随机浮点数（用于方向统计学） |
| `paretovariate()` | 基于帕累托分布返回随机浮点数（用于概率论） |
| `weibullvariate()` | 基于威布尔分布返回随机浮点数（用于统计学） |

- request 模块

| Method                                                       | Description                                                  |
| :----------------------------------------------------------- | :----------------------------------------------------------- |
| [delete(*url*, *args*)](https://cn.w3schools.com/python/ref_requests_delete.asp) | Sends a DELETE request to the specified url                  |
| [get(*url*, *params, args*)](https://cn.w3schools.com/python/ref_requests_get.asp) | Sends a GET request to the specified url                     |
| [head(*url*, *args*)](https://cn.w3schools.com/python/ref_requests_head.asp) | Sends a HEAD request to the specified url                    |
| patch(*url*, *data, args*)                                   | Sends a PATCH request to the specified url                   |
| [post(*url*, *data, json, args*)](https://cn.w3schools.com/python/ref_requests_post.asp) | Sends a POST request to the specified url                    |
| put(*url*, *data, args*)                                     | Sends a PUT request to the specified url                     |
| request(*method*, *url*, *args*)                             | Sends a request of the specified method to the specified url |

- statistics 模块

| Method                      | Description                              |
| --------------------------- | ---------------------------------------- |
| statistics.harmonic_mean()  | 计算给定数据的调和平均值（中心位置）     |
| statistics.mean()           | 计算给定数据的平均值（均值）             |
| statistics.median()         | 计算给定数据的中位数（中间值）           |
| statistics.median_grouped() | 计算分组连续数据的中位数                 |
| statistics.median_high()    | 计算给定数据的高中位数                   |
| statistics.median_low()     | 计算给定数据的低中位数                   |
| statistics.mode()           | 计算给定数值或名义数据的众数（中心趋势） |
| statistics.pstdev()         | 计算整个总体的标准差                     |
| statistics.stdev()          | 计算样本数据的标准差                     |
| statistics.pvariance()      | 计算整个总体的方差                       |
| statistics.variance()       | 计算样本数据的方差                       |

- math 模块

| Method           | Description                                                  |
| ---------------- | ------------------------------------------------------------ |
| math.acos()      | 返回一个数的反余弦值                                         |
| math.acosh()     | 返回一个数的反双曲余弦值                                     |
| math.asin()      | 返回一个数的反正弦值                                         |
| math.asinh()     | 返回一个数的反双曲正弦值                                     |
| math.atan()      | 返回一个数的弧度反切线值                                     |
| math.atan2()     | 返回 y/x 的弧度反切线值                                      |
| math.atanh()     | 返回一个数的反双曲正切值                                     |
| math.ceil()      | 将一个数向上取整到最近的整数                                 |
| math.comb()      | 返回从 n 个元素中选择 k 个元素的方式数（无重复且无顺序）     |
| math.copysign()  | 返回一个浮点数，其值为第一个参数的值，符号为第二个参数的符号 |
| math.cos()       | 返回一个数的余弦值                                           |
| math.cosh()      | 返回一个数的双曲余弦值                                       |
| math.degrees()   | 将角度从弧度转换为度                                         |
| math.dist()      | 返回两点 (p 和 q) 之间的欧几里得距离，其中 p 和 q 是该点的坐标 |
| math.erf()       | 返回一个数的误差函数                                         |
| math.erfc()      | 返回一个数的互补误差函数                                     |
| math.exp()       | 返回 e 的 x 次幂                                             |
| math.expm1()     | 返回 e^x - 1                                                 |
| math.fabs()      | 返回一个数的绝对值                                           |
| math.factorial() | 返回一个数的阶乘                                             |
| math.floor()     | 将一个数向下取整到最近的整数                                 |
| math.fmod()      | 返回 x/y 的余数                                              |
| math.frexp()     | 返回一个指定数的尾数和指数                                   |
| math.fsum()      | 返回任何可迭代对象（元组、数组、列表等）中所有元素的总和     |
| math.gamma()     | 返回 x 处的伽马函数值                                        |
| math.gcd()       | 返回两个整数的最大公约数                                     |
| math.hypot()     | 返回欧几里得范数                                             |
| math.isclose()   | 检查两个值是否接近                                           |
| math.isfinite()  | 检查一个数是否为有限数                                       |
| math.isinf()     | 检查一个数是否为无穷大                                       |
| math.isnan()     | 检查一个值是否为 NaN（非数字）                               |
| math.isqrt()     | 返回一个平方根数的向下取整整数                               |
| math.ldexp()     | 返回 math.frexp() 的逆运算，即 x * (2**i) 的结果，其中 x 和 i 是给定的数 |
| math.lgamma()    | 返回 x 的对数伽马值                                          |
| math.log()       | 返回一个数的自然对数，或以指定底数的对数                     |
| math.log10()     | 返回 x 的以 10 为底的对数                                    |
| math.log1p()     | 返回 1+x 的自然对数                                          |
| math.log2()      | 返回 x 的以 2 为底的对数                                     |
| math.perm()      | 返回从 n 个元素中选择 k 个元素的方式数（有序且无重复）       |
| math.pow()       | 返回 x 的 y 次幂                                             |
| math.prod()      | 返回可迭代对象中所有元素的乘积                               |
| math.radians()   | 将度数值转换为弧度                                           |
| math.remainder() | 返回最接近的值，使得分子能被分母整除                         |
| math.sin()       | 返回一个数的正弦值                                           |
| math.sinh()      | 返回一个数的双曲正弦值                                       |
| math.sqrt()      | 返回一个数的平方根                                           |
| math.tan()       | 返回一个数的正切值                                           |
| math.tanh()      | 返回一个数的双曲正切值                                       |
| math.trunc()     | 返回一个数的截断整数部分                                     |
