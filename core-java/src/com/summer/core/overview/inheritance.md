# 继承
关键字extends表明正在构造的新类派生于一个已存在的类。这个已存在的类称为超类（superclass）、基类（baseclass）或父类（parent class）；
新类称为子类（subclass）、派生类（derived class）或孩子类（child class）。</br>
有些人认为super与this引用是类似的概念，实际上，这样比较不太恰当。这是因为super不是一个对象的引用，例如，不能将值super赋给另一个对象变量，他只是一个指示编译器调用超类方法的特殊关键字。
### 多态与动态绑定
一个对象变量可以指示多种实际类型的现象称为多态（polymorphism）。在运行时能够自动地选择适当的方法，称为动态绑定（dynamic binding）。
### 阻止继承：final类和方法
不允许扩展的类被称为final类。如果在定义类的时候使用了final修饰符就表明这个类是final类。
### 强制类型转换
强转时需要使用 instanceof 操作符判断是否为同类型。
+ 只能在继承层次内进行强制类型转换。
+ 再将超类强制类转换成子类之前，应该使用instanceof进行检查。
