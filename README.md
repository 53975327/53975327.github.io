# 欢迎！这是我对python中 类与对象的认识
##目录
================
* [1. 类的定义](#11-类的定义)

### 1.1类的定义？
类的实质是一种引用数据类型，就像基本数据类型int，double......等一样，只不过类要相对复杂一些因为它的本质是数据类型，而不是数据，所以不存在于内存中，不能被直接操作，只有被实例化为对象时，才会变得可操作。
### 1.2类和对象
类可以看作一种数据类型，而对象就是这个类型的具体的一个数据。就比如人类是一个类，而“你”你是人类中具体的一个人，你就是人类这个类中具体的一个数据，有着不同的“值”（身高体重）。同时，你就是这个类中一个具体的实例。

##如何定义一个类呢
如果你学过c++,类的定义方式大概与c++相同，在c++中我们会专门去声明类的数据成员
比如 person类中有年龄，我们就需要专门声明int age
而在python中是不需要的，这个会在我们的内置函数__init__中自动定义好
```markdown
class person:
  def __init__(self,age,name)
    self.age=age       /////  self.age就是你的类中的数据成员，他的名字叫"age"
    self.name=name
  def show(self):
    print("your age is",self.age)
    print("your name is",self.name)
```
如上，在定义一个具体的类对象时就会最先调用 _init_(self,age,name),但你并不需要去输入3个数据，其中self更像是对自己本身的一个调用，它相当于你这个类对象的本身
举个例子：你定义了一个类 person a(15,"帅哥")，但你发现了吗，你并没用输入那个self。因为在这里，self其实就是你定义的a，它会自动帮你输入。
这个__init__你可以理解成是c++中函数的构造函数，而self.age等就相当于在定义类时，自动帮你申请了两个新的变量给这个类，他们的名字分别叫self.age和self.name(a.age,a.name)
在这个类中的成员函数每当需要用到这些数据（name,age）的时候，就需要在函数的参数表中加入self，代表对自身数据的引用。

For more details see [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/).

### Jekyll Themes

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/53975327/53975327.github.io/settings). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://help.github.com/categories/github-pages-basics/) or [contact support](https://github.com/contact) and we’ll help you sort it out.
