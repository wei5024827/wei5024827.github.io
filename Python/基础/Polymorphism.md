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

