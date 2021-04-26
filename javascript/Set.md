# Set

## 构造

```
const s = new Set();
const s = new Set([1,2,3,4]);
const s = new Set();
```

## 性质

成员都是唯一的，没有重复

向Set添加值时，不会发生类型转换。5和“5” 是两个不同的值

原理：same value quality 类似于“===”、但是在Set中NaN等于自身

```
NaN == NaN
false
NaN === NaN
false
但是在Set中NaN等于自身
```

两个对象总是不相等

两个空对象是不精确相等，

## 方法

#### 增删改查

size()

add();

delete()

has()

clear();

#### 遍历

keys();

values();

entries();

forEach();



map

filter

```
let set = new Set([1,2,3,4,5]);
set = new Set([...set].map(x => x * 2));
set = new Set([...set].filter(x => (x % 2) == 0));
```



# 遍历方式

```
const s = new Set([1,2,3,4]);

for(let i of s){
	console.log(i);
}

forEach((value,key) => conole.log()))

```



#### 实现并集、交集、差集？

```
let a = new Set([1,2,3]);
let b = new Set([4,3,2]);

let union = new Set([...a,...b]);
let intersect = new Set([...a].filter(x => b.has(x)));
let difference = new Set([...a].filter(x => !b.has(x)));
```

