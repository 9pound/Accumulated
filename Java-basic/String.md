# Java天问——String篇

### 1、String 为什么是不可变的？String为啥要设计为不可变的？



```java
public final class String
    implements java.io.Serializable, Comparable<String>, CharSequence {
    /** The value is used for character storage. */
    private final char value[];
```

- 类是final的
- value[] 是private final 



1. 安全和StringBuilder比较，特别是它们的引用作为参数的时候，StringBuilder对象容易被改变
2. String用在HashMap，如果String可以改变，容易出现重复值，String的不可变性，保证的hash的唯一
3. url 