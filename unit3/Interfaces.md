##[第三章](https://github.com/kymjs/KotlinDoc-cn#第三章)
---
#接口

Kotlin 的接口很像 java 8。它们都可以包含抽象方法，以及方法的实现。和抽象类不同的是，接口不能保存状态。可以有属性但必须是抽象的。  
  
接口是通过关键字 interface 来定义的：
```kotlin
interface MyInterface {
    fun bar()
    fun foo() {
        //函数体是可选的
    }
}
```

###接口的实现

一个类或对象可以实现一个或多个接口

```kotlin
class Child : MyInterface {
    fun bar () {
        //函数体
    }
}
```

###接口中的属性
因为接口没有状态，所以中只允许有无状态的属性。
```kotlin
interface MyInterface {
    val property: Int //抽象属性
    fun foo() {
        print(property)
    }
}

class Child : MyInterface {
    override val property: Int = 29
}
```

###解决重写冲突
当我们在父类中声明了许多类型，有可能出现一个方法的多种实现。比如：
```kotlin
interdace A {
    fun foo() { print("A") }
    fun bar()
}

interface B {
    fun foo() { print("B") }
    fun bar() { print("bar") }
}

class C : A {
    override fun bar() { print("bar") }
}

class D : A, B {
    override fun foo() {
        super<A>.foo()
        super<B>.foo()
    }
}
```
A B 接口都有声明了 foo() bar() 函数。它们都实现了 foo() 方法，但只有 B 实现了 bar() ,bar() 在 A 中并没有声明它是抽象的，这是因为在接口中如果函数没有函数体，那么默认是抽像的。现在，如果我们从 A 中派生一个 C 实体类，显然我们需要重写 bar() ，并实现它。而我们从 A 和 B 派生一个 D ，我们不用重写 bar() 方法，因为我们的一个继承中有一个已经实现了它。但我们继承了俩个 foo() 的实现，因此编译器不知道应该选哪个，并强制我们重写 foo() 并且明确指出我们想怎么实现。