PATTERN_UML_CODE
====================
`PATTERN_UML_CODE` 记录了设计模式章节的 UML 模型图相关代码。

## 1.单例模式

<div align="center"> <img src="images/11.singleton.png" width="280px"> </div><br>

```text
@startuml

skinparam classAttributeIconSize 0
class Singleton {
 - {static} singleton : Singleton
 - Singleton()
 + getSingleton() : Singleton
}

Singleton  -->  Singleton

note bottom  of Singleton
  <b>public static Singleton getInstance() {  </b>
  <b>     // 第一次检查，用来避免 singleton 已经被实例化之后的加锁操作</b>
  <b>     if (singleton != null) { </b>
  <b>           // 不创建  </b>
  <b>     }else { </b>
  <b>           synchronized (Singleton.class) { </b>
  <b>           // 第二次检查，加锁确保只有一个线程进行实例化操作 </b>
  <b>           if(singleton == null) { </b>
  <b>               singleton = new Singleton(); </b>
  <b>           }</b>
  <b>     }</b>
  <b>} </b>
end note
```

## 2.简单工厂模式

```text
@startuml

interface Product {
    + show() : void
}

class ConcreteProductA {
  + show() : void
}
Product <|.. ConcreteProductA
class ConcreteProductB {
  + show() : void
}
Product <|.. ConcreteProductB

class SimpleFactory{
    + createProduct() : Product
}
ConcreteProductA <-- SimpleFactory
ConcreteProductB <-- SimpleFactory

note bottom  of SimpleFactory
  <b>public Product createProduct(int type) {  </b>
  <b>     if (type == 1) { </b>
  <b>           return new ConcreteProductA();  </b>
  <b>     } else if (type == 2) { </b>
  <b>           return new ConcreteProductB(); </b>
  <b>     } </b>
  <b>} </b>
end note

@enduml
```

## 3.工厂方法模式

```text
@startuml

interface Product {
    + show() : void
}

interface FactoryMethod {
    + createProduct() : Product
}

class ConcreteProduct {
  + show() : void
}
Product <|.. ConcreteProduct

class ConcreteFactory {
   + createProduct() : Product
}
FactoryMethod <|.. ConcreteFactory

ConcreteProduct <-- ConcreteFactory

note bottom  of ConcreteFactory
  <b>public Product createProduct() {  </b>
  
  <b>    return new ConcreteProduct(); </b>
  <b>} </b>
end note

@enduml
```





