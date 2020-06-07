# 欢迎！这是我对python中 类与对象的认识
姓名：周润林
学号：G1319208
## 目录
# 一、什么是类？
 * [1.1 类](#11-类)
 * [1.2 类和对象](#12-类和对象)
# 二、编程中类的定义
 * [2.1 如何定义一个类以及它的对象](#21-如何定义一个类以及它的对象)
 * [2.2 有关self](#22-有关self)
# 三、类的封装性
 * [3 有关对象的属性](#3-有关对象的属性)
# 四、类变量和实例变量
* [4 类变量与实例变量](#4-类变量与实例变量)
# 五、类之间的关系
* [5.1 继承](#51-继承)
* [5.2 多态](#52-多态)
# 六、对课程的建议
* [6、对课程的建议](#6-对课程的建议)
## 一、什么是类？
### 1.1 类
--------------------
类的实质是一种引用数据类型，就像基本数据类型int，double......等一样，只不过类要相对复杂一些因为它的本质是数据类型，而不是数据，所以不存在于内存中，不能被直接操作，只有被实例化为对象时，才会变得可操作。
### 1.2 类和对象
类可以看作一种数据类型，而对象就是这个类型的具体的一个数据。就比如人类是一个类，而“你”你是人类中具体的一个人，你就是人类这个类中具体的一个数据，有着不同的“值”（身高体重）。同时，你就是这个类中一个具体的实例。

## 二、编程中类的定义

### 2.1 如何定义一个类以及它的对象
-------------------------
### 如何定义一个类？
如果你学过c++,类的定义方式大概与c++相同，在c++中我们会专门去声明类的数据成员
比如 person类中有年龄，我们就需要专门声明int age
而在python中是不需要的，这个会在我们的内置函数__init__中自动定义好
```python
class person:
  def __init__(self,age,name)
    self.age=age       /////  self.age就是你的类中的数据成员，他的名字叫"age"
    self.name=name
  def show(self):
    print("your age is",self.age)
    print("your name is",self.name)
```
  ### 如何定义一个类的对象呢？
  ```python
class person:
  def __init__(self,age,name):
    self.age=age        #self.age就是你的类中的数据成员,他的名字叫"age"
    self.name=name
  def show(self):
    print("your age is",self.age)
    print("your name is",self.name)

def main():
  a=person(3,5)
  a.show()
  print("your age is",a.age)
  print("your name is",a.name)

if __name__=='__main__':
  main()
```
  ## 注意！
  在这里定义的方式与c++不同，是使用=的方式进行定义，你可以理解为一切皆变量，定义的class person也是一个变量
  
 如上，在定义一个具体的类对象时就会最先调用__init__(self,age,name),但你并不需要去输入3个数据，其中self更像是对自己本身的一个调用，它相当于你这个类对象的本身
### 
举个例子：比如这里的show函数，你在python中定义它时加入了self，而在c++中则可以直接选择参数为空，如果你去调用它，你并不用输入那个self。因为在python中，self其实就是你定义的a，它会自动帮你输入。
### 2.2 有关self
--------------------------
首先，self的取名是大家的约定俗成，你可以不叫他self，甚至可以随便取名，只不过在很多教程上都是建议大家使用self，便于识别
因为在函数调用中你需要用到自身的数据，你输出age和name时，需要去引用自身的变量，如果不引用，会报错
在这个类中的成员函数每当需要用到这些数据name和age的时候，就需要在函数的参数表中加入self，代表对自身数据的引用。
其实一开始我在python学习中也很困惑，这个self到底是什么呢？其实最开始我并不是很理解为什么要这么做，直到后来有一天突然从知乎上看到......
你可以认为里面的函数是在你定义时自动帮你生成的，可不同的对象对应同样的函数名。，怎么区分呢？就是靠你的self，当不同的对象调用函数时，就自动对应了不同的参数，也因此能够区分。

## 三、类的封装性
### 3 有关对象的属性
---------------------
在c++、java等编程语言中，都会在定义一个类时对数据成员进行声明，分为public，protected，private三类，大部分情况我们都会将数据成员定义成private以保证无法从外部直接调用类对象的数据，以保证类的封装性
我们在刚才对类的定义的时候，相关的数据age和name的属性是什么呢？
其实不难发现，我们在上述文件中我们直接调用了a的age和name，所以它的属性是public
让我们将上述代码进行一点小小的修改
```python
class person:
  def __init__(self,age,name):
    self.__age=age        
    self.__name=name
  def show(self):
    print("your __age is",self.__age)
    print("your __name is",self.__name)

def main():
  a=person(3,5)
  a.show()
  print("your __age is",a.__age)             #error
  print("your __name is",a.__name)


if __name__=='__main__':
  main()
```
在这段代码中，程序运行到print时候会报错，而在a.show()处可以正常运行。仔细观察我们发现，我们在age和name前面加入了__（两个下划线）
在python中，我们用在数据前加入两个下划线__，将数据成员定义成为private，一个下划线_,将数据成员定义为protected.
### 有一个小点要注意
在前文中我们提到了类在定义时会有一个__init__函数，这个函数虽然有两个开头有两个下划线，但同时在结尾也有下划线，所以呢他并不是私有的属性。__init__是一个特殊的函数，在类初始化时调用，相当于将类实例化。（实例化是什么呢？我们马上讲）
## 四、类变量与实例变量
### 4 类变量与实例变量
### 类变量
---------------------------------
类变量其实很好理解，就是你在类中定义的变量
举例如下：
```python
class person:
  age=0
  def __init__(self,name):
    self.name=name

def main():
  a=person('xiaohong')
  b=person('xiaoming')
  person.age=6
  person.name='xiaolan'
  print('a.age',a.age)
  print('a.name',a.name)
  print('b.age:',b.age)
  print('b.name',b.name)

if __name__=='__main__':
  main()
```
这段代码会输出
```markdown
a.age 6
a.name xiaohong
b.age: 6
b.name xiaoming
```
这其中，age就相当于是类变量，所以当我们对age进行改变时会使a与b的age都发生改变，你可以将它看作静态变量，不过在python3中已经不成立,让我们往下看
### 实例变量
---------------------------
还是刚才这段代码我们做一点小小的改变
```python
class person:
  age=0
  name='null'
  def __init__(self,name):
    self.name=name

def main():
  a=person('xiaohong')
  b=person('xiaoming')
  a.age=6
  person.name='xiaolan'
  print('a.age',a.age)
  print('a.name',a.name)
  print('b.age:',b.age)
  print('b.name',b.name)

if __name__=='__main__':
  main()

```
首先我们针对两个对象的name研究，name的值都没有发生改变，所以这里的name是他们每个独有的实例变量。而在上文提到过__init__是一个实例化的过程，而self.name就是每个对象独占的数据。无论你对person中的name怎么进行更改，都不会改变self.name值

接着我们说一下这里的age,如果问age的值大家理所当然都会认为a与b中的age都发生了改变，可实际的输出确是
```markdown
a.age 6
a.name xiaohong
b.age: 0
b.name xiaoming
```
在python3中，如果你单独对某一个类对象改变了他的类变量，这个<strong>类变量</strong>就会变成类对象的<strong>实例变量</strong>，而其他的类中的类变量并不会发生改变。
这是一个初学者很容易跳进去的坑（因为我跳过很多次 emm......)
所以当类中存在类变量的时候（特别是你希望他以静态变量的形式存在时）一定要注意对类变量进行改变时是否是通过类对象进行改变。

##五、继承与多态
### 5.1 继承
---------------------------
先看下面一段代码
```python
class person(object):
  def __init__(self, name, age):
    self.name = name
    self.age = age
      
class student(person):
  def __init__(self, name, age, score):
    super(student, self).__init__(name, age)
    self.score=score  


def main():
  a=student('xiaolan',19,96)
  print('a.age:', a.age)
  print('a.name:',a.name)
  print('a.score:', a.score)

if __name__=='__main__':
  main()
 ```
 这里要介绍一下super(,)._init_()函数
 这个函数是专门用来对父类进行初始化的，也就是说你在定义student类的对象时，在内部也要对person类的数据进行初始化
 继承的方式很简单，直接在类名字后面加上括号，在括号里面加入父类即可，不像c++中那样复杂。可以对父类中的所有数据进行使用。
 
 ### 5.2 多态
 -----------------------
 子类在继承了父类的方法后，可以对父类已有的方法给出新的实现版本，这个动作称之为方法<strong>重写</strong>。通过方法重写我们可以让父类的同一个行为在子类中拥有不同的实现版本，当我们调用这个经过子类重写的方法时，不同的子类对象会表现出不同的行为，这个就是<strong>多态</strong>
 ```python
 class Person(object):
    def __init__(self, name):
        self.name = name
    def whoAmI(self):
        print('I am a Person, my name is %s' % self.name)

class Student(object):
  def __init__(self, name):
    self.name = name

  def whoAmI(self):
    print('I am a Student, my name is %s' % self.name)

class Teacher(object):
  def __init__(self, name):
    self.name = name

  def whoAmI(self):
    print('I am a Teacher, my name is %s' % self.name)

class Worker(object):
  def __init__(self, name):
    self.name = name

  def whoAmI(self):
    print('I am a Worker, my name is %s' % self.name)

person=[Student("小明"),Teacher("大明"),Worker('老明')]
for a in person:
  a.whoAmI()
  ```
  输出的结果是
  ```markdown
  I am a Student, my name is 小明
I am a Teacher, my name is 大明
I am a Worker, my name is 老明
```
  Student、Teacher、Worker同时继承了Person类，当调用名字相同的函数时，却有着不同的表现形式，这就是类的多态
  
  
 
 # 六关于对课程的建议
 ### 6 对课程的建议
 --------------------
 感谢老师这一学期的辛勤付出，虽然我才刚刚大一，编程了解的也不够深入，但老师讲课还是能够听懂（虽然可能我觉得自己是个半吊子）
 
 我觉得这学期的选修课收获很多，尤其是在编程这一方面，对编程有了更深的认识，同时也在编程的规范上进了一步。
 
 如果提什么建议的话，我觉得老师上课一次干货太多了，没次下来要消化很久，久了不用又会有一点忘，很多时候得下来重新看PPT才能跟得上节奏（可能是课时太少了，也能理解）
 
 总之，很感谢老师这学期的辛勤付出，祝老师新的一学年身体健康，在各方面都能更上一层楼！
  

