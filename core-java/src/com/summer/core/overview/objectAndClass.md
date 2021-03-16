# 对象和类
### 面向对象程序设计概述
面向对象（object-oriented programming，OOP）是当今主流的程序设计范型，它取代了20世纪70年代的“结构化”或过程式编程技术。
#### 类
+ 类（class）是构造对象的模板或蓝图。我们可以将类想象成制作小甜饼的模具，将对象想象为小甜饼。由类构造（construct）对象的过程为创建类的实例（instance）
+ 封装（encapsulation,有时称为数据隐藏）是处理的一个重要概念。对象中的数据称为实例字段（instance field），操作数据的过程称为方法（method）。
+ 通过扩展一个类来建立另外一个类的过程称为继承（inheritance）
#### 对象
+ 对象的行为（behavior）——可以对对象完成哪些操作，或者可以对对象应用那些方法？
+ 对象的状态（state）——当调用哪些方法时，对象会如何相应？
+ 对象的标识（identity）——如何区分具有相同行为而具有家族式的相似性。对象的行为是用可调用的方法来定义的。
#### 类之间的关系
+ 依赖（uses-a）dependence
+ 聚合（has-a）aggregation
+ 继承（is-a）inheritance
#### 构造器
+ 构造器与类名相同
+ 每个类可以有一个以上的构造器
+ 构造器可以有0个、1个或多个参数
+ 构造器没有返回值
+ 构造器总是伴随着new操作符一起调用
#### 用var声明局部变量
在Java 10中声明变量可以用var
```
var harry = new Employee();
```
注意var关键字只能用于方法中的局部变量。参数和字段的类型必须声明。
#### 使用null引用
在Java 9中，Object类对此提供了一个便利方法：
```
public Employee(String n){
    name = Objects.requireNonNullElse(n,"unknown");
}
```
"严格型"方法则干脆拒绝null参数：
```
public Employee(String n){
    Objects.requireNonNull(n,"The name cannot be null");
    name = n;
}
```
#### 封装的优点
一旦构造器中设置，就没有任何办法可以对它进行修改，这样我们可以确保name字段不会受到外界的破坏。
注意不要编写返回可变对象引用的访问器方法。
```
class Employee{
    private Date day;

    public Date getDay(){
        return day;//bad
    }
}
class Employee{
    public Date getDay(){
        return (Date)hireDay.clone();//ok
    }
}
```
#### 基于类的访问权限
Employee 类的方法可以访问任何Employee类型对象的私有字段
```
class Employee{
       public boolean equals(Empoyee other){
           return name.equals(other.name);
       }
   }  
```
#### final实例字段
可以将实例字段定义为final。这样的字段必须在构造对象时初始化。也就是说，必须确保在每一个构造器执行之后，这个字段的值已经设置，并且以后不能再修改这个字段。<br>
对于可变的类，使用final修饰符可能会造成混乱。
```
private final StringBuilder name;
name = new StringBuilder();
```
final关键字只是表示存储在name变量中的对象引用不会再指示另一个不同的StringBuilder对象。不过这个对象可以更改：
```
name.append("");
```
### 静态字段与静态方法
#### 静态字段
```
class Employee{
    private static int nextId = 1;
    
    private int id;
}
```
现在，每一个Employee对象都有一个自己的id字段，但这个类的所有实例将共享一个nextId字段。换句话说，
如果有1000个Employee类对象，则有1000个实例字段id，分别对应每一个对象。但是，只有一个静态字段nextId。
即使没有Employee对象，静态字段nextId也存在。它属于类，而不属于任何单个的对象。
#### 静态常量
```
class Math{
    public static final double PI = 3.14159265358979323846
}
```
如果省略关键字static，PI就变成了Math类的一个实例字段。也就是说，需要通过Math类的一个对象来访问PI，并且每一个Math对象都有它自己的一个PI副本。
#### 静态方法
在下面两种情况下可以使用静态方法：
+ 方法不需要访问对象状态，因为它需要的所有参数都通过显式参数提供。
+ 方法只需要访问类的静态字段