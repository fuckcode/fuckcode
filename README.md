### 记录编程语言非常糟糕的代码(经常容易忽略的或者设计语言的设计缺陷)

# java

## [条件运算符会做数值类型的类型提升](https://github.com/m-fuckcode/fuckcode/issues/1)

你认为自己知道什么时候该使用条件表达式？面对现实吧，你还不知道。大部分人会认为下面的2段代码是等价的：
```java
Object o1 = true ? new Integer(1) : new Double(2.0);
```
等同于：
```java
Object o2;

if (true)
    o2 = new Integer(1);
else
    o2 = new Double(2.0);
```
让你失望了。来做个简单的测试吧：
```java
System.out.println(o1);
System.out.println(o2);
```
打印结果是：
```
1.0
1
```
哦！如果『需要』，条件运算符会做数值类型的类型提升，这个『需要』有非常非常非常强的引号。因为…… 你觉得下面的程序会抛出NullPointerException吗？
```java
Integer i = new Integer(1);
if (i.equals(1))
    i = null;
Double d = new Double(2.0);
Object o = true ? i : d; // NullPointerException!
System.out.println(o);
```


```java
Object o1 = true
  ? (Object) new Integer(1) 
  : new Double(2.0);
System.out.println(o1);
```
才能得到正确的结果`1`

--- 
