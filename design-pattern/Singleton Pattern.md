# Singleton Pattern

## 如何保证一个对象只能被实例化一次？

### 全局变量

#### 缺点

- 必须在程序一开始就创建好
- 可能非常耗费资源，我们想要在需要的时候才创建对象

### 静态变量+静态方法+适当访问修饰符

### 单例模式

**定义：**确保一个类只有一个实例，并提供一个全局访问点。

**作用：**创建独一无二的对象。

**优点：**延迟实例化

#### 经典单例模式

线程不安全

```
public class Singleton() {
	private static Singleton uniqueInstance;
	private Singleton(){}
	public static Singleton getInstance(){
		if(uniqueInstance == null){
			uniqueInstance = new Singleton();
		}
		return uniquInstance;
	}
}
```



#### 同步单例模式

问题：getinstance方法只有在第一次执行时，才需要真正的同步；同步一个方法可能造成程序执行效率下降100倍

```
public class Singleton() {
	private static Singleton uniqueInstance;
	private Singleton(){}
	public static synchronized Singleton getInstance(){
		if(uniqueInstance == null){
			uniqueInstance = new Singleton();
		}
		return uniquInstance;
	}
}
```

#### 急切单例模式

- 线程安全

- 不用同步

```
public class Singleton() {
	private static Singleton uniqueInstance = new Singleton();;
	private Singleton(){}
	public static synchronized Singleton getInstance(){	
		return uniquInstance;
	}
}
```

#### 双重检查加锁单例模式

```
public class Singleton() {
	private volatile static Singleton uniqueInstance;
	private Singleton(){}
	public static Singleton getInstance(){	
		if(uniqueInstance == null) {
			synchronized(Singleton.class) {
				if(uniqueInstance == null){
					uniqueInstance = new Singleton();
				}
			}
		}
	}
}
```



#### 什么需要volatile关键字?

```
uniqueInstance = new Singleton();
```

可以分解为3个步骤：

1. memory=allocate();// 分配内存 相当于c的malloc
2. ctorInstanc(memory) //初始化对象
3.  s=memory //设置s指向刚分配的地址


上面的代码在编译器运行时，可能会出现重排序 从1-2-3 排序为1-3-2

如此在多线程下就会出现问题

例如现在有2个线程A,B

线程A在执行第5行代码时，B线程进来，而此时A执行了 1和3，没有执行2，此时B线程判断s不为null 直接返回一个未初始化的对象，就会出现问题