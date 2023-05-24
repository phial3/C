[设计模式分类参考1](https://blog.csdn.net/m0_37741420/article/details/106169752)

[创建型模式](https://blog.csdn.net/m0_37741420/article/details/106171863)

[结构型模式](https://blog.csdn.net/m0_37741420/article/details/106442936)

[行为型模式-上](https://blog.csdn.net/m0_37741420/article/details/106600250)

[行为型模式-下](https://blog.csdn.net/m0_37741420/article/details/107445024)

[设计模式应用](https://blog.csdn.net/m0_37741420/article/details/110133201)

# 设计模式的分类

- 根据其目的（模式是用来做什么的）可分为三种：

（1）创建型(Creational)： 主要用于创建对象。

（2）结构型(Structural)：主要用于处理类或对象的组合。

（3）行为型(Behavioral)：主要用于描述对类或对象怎样交互和怎样分配职责。

- 根据范围（模式主要是用于处理类之间关系还是处理对象之间的关系）可分为类模式和对象模式两种：

（1）类模式处理类和子类之间的关系，这些关系通过继承建立，在编译时刻就被确定下来，是属于静态的。

（2）对象模式处理对象间的关系，这些关系在运行时刻变化，更具动态性。

## 创建型模式

1. 抽象工厂模式(Abstract Factory)
2. 建造者模式(Builder)
3. 工厂方法模式(Factory Method)
4. 原型模式(Prototype)
5. 单例模式(Singleton)

## 结构型模式

1. 适配器模式(Adapter)
2. 桥接模式(Bridge)
3. 组合模式(Composite)
4. 装饰模式(Decorator)
5. 外观模式(Facade)
6. 享元模式(Flyweight)
7. 代理模式(Proxy)

## 行为型模式

1. 责任链模式(Chain of Responsibility)
2. 命令模式(Command)
3. 解释器模式(Interpreter)
4. 迭代器模式(Iterator)
5. 中介者模式(Mediator)
6. 备忘录模式(Memento)
7. 观察者模式(Observer)
8. 状态模式(State)
9. 策略模式(Strategy)
10. 模板方法模式(Template Method)
11. 访问者模式(Visitor)

## 设计模式的分类表:

|范围目的	|创建型模式|	结构型模式	| 行为型模式                              |
|:-----|:-----|:-----|:-----------------------------------|
|类模式	|工厂方法|	(类）适配器| 	模板方法、解释器                          |
|对象模式	|单例 原型 抽象工厂 建造者	|代理 (对象）适配器 桥接 装饰 外观 享元 组合	| 策略 命令 职责链 状态 观察者 中介者 迭代器 访问者 备忘录   |