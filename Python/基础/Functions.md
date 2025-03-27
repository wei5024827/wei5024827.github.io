### 函数入参

- *args

  - 如果不知道入参是几个，可以在参数前加* ， 这样会传入一个元组

    ```python
    def my_function(*kids):
      print("The youngest child is " + kids[2])
    
    my_function("Emil", "Tobias", "Linus") #returns The youngest child is Linus
    ```

- **args

  - 如果不知道键参数是几个，可以在参数前加**，这样会传入一个字典

    ```python
    def my_function(**kid):
      print("His last name is " + kid["lname"])
    
    my_function(fname = "Tobias", lname = "Refsnes") # retruns His last name is Refsnes
    ```

- list作为参数

  ```python
  def my_function(food):
    for x in food:
      print(x)
  
  fruits = ["apple", "banana", "cherry"]
  
  my_function(fruits) 
  """""
  returns
  apple
  banana
  cherry
  """""
  ```

  

- 仅限位置参数

  - **`/`**（仅限位置参数）：**按参数定义顺序传递**，不指定参数名。

    ```python
    def f(x, /, y):
        print(x, y)
    
    f(1, 2)      # ✅ x=1（位置），y=2（位置）
    f(1, y=2)    # ✅ x=1（位置），y=2（关键字）
    f(x=1, y=2)  # ❌ x 不能关键字传递
    ```

  - **`*`**（仅限关键字参数）：**按参数名传递**，显式指定 `参数名=值`

    ```python
    def f(x, *, y):
        print(x, y)
    
    f(1, y=2)    # ✅ x=1（位置），y=2（关键字）
    f(1, 2)      # ❌ y 必须用关键字
    ```

### Lambda

- 基本用法

  ```python
  x = lambda a : a + 10
  print(x(5))  #retruns 15
  ```

- 匿名函数（高级用法）

  ```python
  def myfunc(n):
    return lambda a : a * n
  
  mydoubler = myfunc(2)
  
  print(mydoubler(11))
  
  """""
  #拆解
  myfunc(2) 返回的是lambda表达式
  所以mydoubler = myfunc(2) 相当于
  mydoubler = lambda a : a * 2
  
  根据基本用法可知
  mydoubler(11)  =  11 * 2 = 22
  """""
  ```


### 装饰器

- 基础装饰器固定格式

  ```
  def decorator(func): #接受参数为函数
  	def wrapper(*args, **kwargs): #定义包装函数
      	x = func(*args, **kwargs)
      	return x #必须返回原函数结果
      return wrapper # 必须返回包装函数
  
  @decorator
  def target_function():
  	pass
      
  ```

  



### Class

- \__init\__()函数

  - 初始化函数，用来定义类是如何初始化的

    ```python
    class Person:
      def __init__(self, name, age):
        self.name = name
        self.age = age
    
    p1 = Person("John", 36)
    
    print(p1.name)
    print(p1.age)
    ```

- \__str()\__ 函数

  - 控制类返回的字符串形式

  - 如果未设置该函数，则返回类的属性

    ```python
    class Person:
      def __init__(self, name, age):
        self.name = name
        self.age = age
    
    p1 = Person("John", 36)
    
    print(p1)   # returns 类的属性
    ```

  - 如果设置该函数，则返回该函数

    ```python
    class Person:
      def __init__(self, name, age):
        self.name = name
        self.age = age
    
      def __str__(self):
        return f"{self.name}({self.age})"
    
    p1 = Person("John", 36)
    
    print(p1) # returns John(36)
    ```

    