Java 备忘清单
===

该备忘单是针对 Java 初学者的速成课程，有助于复习 Java 语言的基本语法。

入门
--------

### Hello.java
<!--rehype:wrap-class=row-span-2-->

```java
public class Hello {
  // 主要方法
  public static void main(String[] args)
  {
    // 输出: Hello, world!
    System.out.println("Hello, world!");
  }
}
```

编译和运行

```shell
$ javac Hello.java
$ java Hello
Hello, world!
```

### 变量 Variables

```java
int num = 5;
float floatNum = 5.99f;
char letter = 'D';
boolean bool = true;
String site = "jaywcjlove.github.io";
```

### 原始数据类型
<!--rehype:wrap-class=row-span-2-->

| 数据类型 | 大小   | 默认 | 范围               |
|-----------|--------|---------|---------------------|
| `byte`    | 1 byte | 0       | -128 ^to^ 127       |
| `short`   | 2 byte | 0       | -2^15^ ^to^ 2^15^-1 |
| `int`     | 4 byte | 0       | -2^31^ ^to^ 2^31^-1 |
| `long`    | 8 byte | 0       | -2^63^ ^to^ 2^63^-1 |
| `float`   | 4 byte | 0.0f    | _N/A_               |
| `double`  | 8 byte | 0.0d    | _N/A_               |
| `char`    | 2 byte | \\u0000 | 0 ^to^ 65535        |
| `boolean` | _N/A_  | false   | true / false        |
<!--rehype:className=show-header-->

### 字符串 Strings

```java
String first = "John";
String last = "Doe";
String name = first + " " + last;
System.out.println(name);
```

查看: [Strings](#java-字符串)

### 循环 Loops

```java
String word = "QuickRef";
for (char c: word.toCharArray()) {
  System.out.print(c + "-");
}
// 输出: Q-u-i-c-k-R-e-f-
```

查看: [Loops](#java-循环)

### 数组 Arrays

```java
char[] chars = new char[10];
chars[0] = 'a'
chars[1] = 'b'
String[] letters = {"A", "B", "C"};
int[] mylist = {100, 200};
boolean[] answers = {true, false};
```

查看: [Arrays](#java-数组)

### 交换变量 Swap

```java
int a = 1;
int b = 2;
System.out.println(a + " " + b); // 1 2
int temp = a;
a = b;
b = temp;
System.out.println(a + " " + b); // 2 1
```

### 类型转换 Type Casting

```java
// Widening
// byte<short<int<long<float<double
int i = 10;
long l = i;               // 10
// Narrowing 
double d = 10.02;
long l = (long)d;         // 10
String.valueOf(10);       // "10"
Integer.parseInt("10");   // 10
Double.parseDouble("10"); // 10.0
```

### 条件语句 Conditionals

```java
int j = 10;
if (j == 10) {
  System.out.println("I get printed");
} else if (j > 10) {
  System.out.println("I don't");
} else {
  System.out.println("I also don't");
}
```

查看: [Conditionals](#条件语句 Conditionals)

### 用户输入

```java
Scanner in = new Scanner(System.in);
String str = in.nextLine();
System.out.println(str);
int num = in.nextInt();
System.out.println(num);
```

Java 字符串
-------

### 基本的

```java
String str1 = "value"; 
String str2 = new String("value");
String str3 = String.valueOf(123);
```

### 字符串连接

```java
String s = 3 + "str" + 3;     // 3str3
String s = 3 + 3 + "str";     // 6str
String s = "3" + 3 + "str";   // 33str
String s = "3" + "3" + "23";  // 3323
String s = "" + 3 + 3 + "23"; // 3323
String s = 3 + 3 + 23;        // 29
```

### 字符串生成器
<!--rehype:wrap-class=row-span-3-->

```java
StringBuilder sb = new StringBuilder(10);
```

---

```java
┌───┬───┬───┬───┬───┬───┬───┬───┬───┐
|   |   |   |   |   |   |   |   |   |
└───┴───┴───┴───┴───┴───┴───┴───┴───┘
0   1   2   3   4   5   6   7   8   9
```

---

```java
sb.append("Reference");
```

---

```java
┌───┬───┬───┬───┬───┬───┬───┬───┬───┐
| R | e | f | e | r | e | n | c | e |
└───┴───┴───┴───┴───┴───┴───┴───┴───┘
0   1   2   3   4   5   6   7   8   9
```

---

```java
sb.delete(3, 9);
```

---

```java
┌───┬───┬───┬───┬───┬───┬───┬───┬───┐
| R | e | f |   |   |   |   |   |   |
└───┴───┴───┴───┴───┴───┴───┴───┴───┘
0   1   2   3   4   5   6   7   8   9
```

---

```java
sb.insert(0, "My ");
```

---

```java
┌───┬───┬───┬───┬───┬───┬───┬───┬───┐
| M | y |   | R | e | f |   |   |   |
└───┴───┴───┴───┴───┴───┴───┴───┴───┘
0   1   2   3   4   5   6   7   8   9
```

---

```java
sb.append("!");
```

---

```java
┌───┬───┬───┬───┬───┬───┬───┬───┬───┐
| M | y |   | R | e | f | ! |   |   |
└───┴───┴───┴───┴───┴───┴───┴───┴───┘
0   1   2   3   4   5   6   7   8   9
```

### 比较

```java
String s1 = new String("QuickRef"); 
String s2 = new String("QuickRef"); 
s1 == s2          // false
s1.equals(s2)     // true
"AB".equalsIgnoreCase("ab")  // true
```

### 操纵

```java
String str = "Abcd";
str.toUpperCase();     // ABCD
str.toLowerCase();     // abcd
str.concat("#");       // Abcd#
str.replace("b", "-"); // A-cd
"  abc ".trim();       // abc
"ab".toCharArray();    // {'a', 'b'}
```

### 信息

```java
String str = "abcd";
str.charAt(2);       // c
str.indexOf("a")     // 0
str.indexOf("z")     // -1
str.length();        // 4
str.toString();      // abcd
str.substring(2);    // cd
str.substring(2,3);  // c
str.contains("c");   // true
str.endsWith("d");   // true
str.startsWith("a"); // true
str.isEmpty();       // false
```

### 不可变

```java
String str = "hello";
str.concat("world");
// 输出: hello
System.out.println(str);
```

---

```java
String str = "hello";
String concat = str.concat("world");
// 输出: helloworld
System.out.println(concat);
```

一旦创建就不能修改，任何修改都会创建一个新的String

Java 数组
-------

### 声明 Declare

```java
int[] a1;
int[] a2 = {1, 2, 3};
int[] a3 = new int[]{1, 2, 3};
int[] a4 = new int[3];
a4[0] = 1;
a4[2] = 2;
a4[3] = 3;
```

### 修改 Modify

```java
int[] a = {1, 2, 3};
System.out.println(a[0]); // 1
a[0] = 9;
System.out.println(a[0]); // 9
System.out.println(a.length); // 3
```

### 循环 (读 & 写)

```java
int[] arr = {1, 2, 3};
for (int i=0; i < arr.length; i++) {
    arr[i] = arr[i] * 2;
    System.out.print(arr[i] + " ");
}
// 输出: 2 4 6
```

### Loop (Read)

```java
String[] arr = {"a", "b", "c"};
for (int a: arr) {
    System.out.print(a + " ");
}
// 输出: a b c 
```

### 二维数组 Multidimensional Arrays

```java
int[][] matrix = { {1, 2, 3}, {4, 5} };
int x = matrix[1][0];  // 4
// [[1, 2, 3], [4, 5]]
Arrays.deepToString(matrix)
for (int i = 0; i < a.length; ++i) {
  for(int j = 0; j < a[i].length; ++j) {
    System.out.println(a[i][j]);
  }
}
// 输出: 1 2 3 4 5 6 7 
```

### 排序 Sort

```java
char[] chars = {'b', 'a', 'c'};
Arrays.sort(chars);
// [a, b, c]
Arrays.toString(chars);
```

Java 条件语句
-----------

### 运算符
<!--rehype:wrap-class=row-span-3-->

- `+` _(加法运算符(也用于字符串连接))_
- `-` _(减法运算符)_
- `*` _(乘法运算符)_
- `/` _(分区运算符)_
- `%` _(余数运算符)_
- `=` _(简单赋值运算符)_
- `++` _(增量运算符；将值增加 1)_
- `--` _(递减运算符；将值减 1)_
- `!` _(逻辑补码运算符；反转布尔值)_
<!--rehype:className=style-round-->

---

- `==` _(等于)_
- `!=` _(不等于)_
- `>` _(比...更棒)_
- `>=` _(大于或等于)_
- `<` _(少于)_
- `<=` _(小于或等于)_
<!--rehype:className=cols-2 style-round-->

---

- `&&` _条件与_
- `||` _条件或_
- [?:](#三元运算符) _三元(if-then-else 语句的简写)_
<!--rehype:className=style-round-->

---

- `instanceof` _(将对象与指定类型进行比较)_
<!--rehype:className=style-round-->

---

- `~` _(一元按位补码)_
- `<<` _(签名左移)_
- `>>` _(有符号右移)_
- `>>>` _(无符号右移)_
- `&` _(按位与)_
- `^` _(按位异或)_
- `|` _(按位包含 OR)_
<!--rehype:className=cols-2 style-round-->

### If else

```java
int k = 15;
if (k > 20) {
  System.out.println(1);
} else if (k > 10) {
  System.out.println(2);
} else {
  System.out.println(3);
}
```

### Switch
<!--rehype:wrap-class=row-span-2-->

```java
int month = 3;
String str;
switch (month) {
  case 1:
    str = "January";
    break;
  case 2:
    str = "February";
    break;
  case 3:
    str = "March";
    break;
  default:
    str = "Some other month";
    break;
}
// 输出: Result March
System.out.println("Result " + str);
```

### 三元运算符

```java
int a = 10;
int b = 20;
int max = (a > b) ? a : b;
// 输出: 20
System.out.println(max);
```

Java 循环
----

### For 循环

```java
for (int i = 0; i < 10; i++) {
  System.out.print(i);
}
// 输出: 0123456789
```

---

```java
for (int i = 0,j = 0; i < 3; i++,j--) {
  System.out.print(j + "|" + i + " ");
}
// 输出: 0|0 -1|1 -2|2
```

### 增强的 For 循环

```java
int[] numbers = {1,2,3,4,5};
for (int number: numbers) {
  System.out.print(number);
}
// 输出: 12345
```

用于循环数组或列表

### While 循环

```java
int count = 0;
while (count < 5) {
  System.out.print(count);
  count++;
}
// 输出: 01234
```

### Do While 循环

```java
int count = 0;
do {
  System.out.print(count);
  count++;
} while (count < 5);
// 输出: 01234
```

### 继续声明

```java
for (int i = 0; i < 5; i++) {
  if (i == 3) {
    continue;
  }
  System.out.print(i);
}
// 输出: 01245
```

### 中断语句

```java
for (int i = 0; i < 5; i++) {
  System.out.print(i);
  if (i == 3) {
    break;
  }
}
// 输出: 0123
```

Java 框架搜集
--------------------

### Java 集合
<!--rehype:wrap-class=col-span-2 row-span-2-->

集合 | Interface   | 有序 | 已排序 | 线程安全 | 复制 | Nullable
:-|:-|:-|:-|:-|:-|:-
[ArrayList](https://docs.oracle.com/javase/8/docs/api/java/util/ArrayList.html)                                    | List        | Y       | _N_    | _N_         | Y         | Y
[Vector](https://docs.oracle.com/javase/8/docs/api/java/util/Vector.html)                                          | List        | Y       | _N_    | Y           | Y         | Y
[LinkedList](https://docs.oracle.com/javase/8/docs/api/java/util/LinkedList.html)                                  | List, Deque | Y       | _N_    | _N_         | Y         | Y
[CopyOnWriteArrayList](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/CopyOnWriteArrayList.html)   | List        | Y       | _N_    | Y           | Y         | Y
[HashSet](https://docs.oracle.com/javase/8/docs/api/java/util/HashSet.html)                                        | Set         | _N_     | _N_    | _N_         | _N_       | One `null`
[LinkedHashSet](https://docs.oracle.com/javase/8/docs/api/java/util/LinkedHashSet.html)                            | Set         | Y       | _N_    | _N_         | _N_       | One `null`
[TreeSet](https://docs.oracle.com/javase/8/docs/api/java/util/TreeSet.html)                                        | Set         | Y       | Y      | _N_         | _N_       | _N_
[CopyOnWriteArraySet](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/CopyOnWriteArraySet.html)     | Set         | Y       | _N_    | Y           | _N_       | One `null`
[ConcurrentSkipListSet](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/ConcurrentSkipListSet.html) | Set         | Y       | Y      | Y           | _N_       | _N_
[HashMap](https://docs.oracle.com/javase/8/docs/api/java/util/HashMap.html)                                        | Map         | _N_     | _N_    | _N_         | _N (key)_ | One `null` _(key)_
[HashTable](https://docs.oracle.com/javase/8/docs/api/java/util/Hashtable.html)                                    | Map         | _N_     | _N_    | Y           | _N (key)_ | _N (key)_
[LinkedHashMap](https://docs.oracle.com/javase/8/docs/api/java/util/LinkedHashMap.html)                            | Map         | Y       | _N_    | _N_         | _N (key)_ | One `null` _(key)_
[TreeMap](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html)                                        | Map         | Y       | Y      | _N_         | _N (key)_ | _N (key)_
[ConcurrentHashMap](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/ConcurrentHashMap.html)         | Map         | _N_     | _N_    | Y           | _N (key)_ | _N_
[ConcurrentSkipListMap](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/ConcurrentSkipListMap.html) | Map         | Y       | Y      | Y           | _N (key)_ | _N_
[ArrayDeque](https://docs.oracle.com/javase/8/docs/api/java/util/ArrayDeque.html)                                  | Deque       | Y       | _N_    | _N_         | Y         | _N_
[PriorityQueue](https://docs.oracle.com/javase/8/docs/api/java/util/PriorityQueue.html)                            | Queue       | Y       | _N_    | _N_         | Y         | _N_
[ConcurrentLinkedQueue](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/ConcurrentLinkedQueue.html) | Queue       | Y       | _N_    | Y           | Y         | _N_
[ConcurrentLinkedDeque](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/ConcurrentLinkedDeque.html) | Deque       | Y       | _N_    | Y           | Y         | _N_
[ArrayBlockingQueue](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/ArrayBlockingQueue.html)       | Queue       | Y       | _N_    | Y           | Y         | _N_
[LinkedBlockingDeque](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/LinkedBlockingDeque.html)     | Deque       | Y       | _N_    | Y           | Y         | _N_
[PriorityBlockingQueue](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/PriorityBlockingQueue.html) | Queue       | Y       | _N_    | Y           | Y         | _N_
<!--rehype:className=show-header-->

### ArrayList

```java
List<Integer> nums = new ArrayList<>();
// 添加
nums.add(2);
nums.add(5);
nums.add(8);
// 检索
System.out.println(nums.get(0));
// 为循环迭代编制索引
for (int i = 0; i < nums.size(); i++) {
    System.out.println(nums.get(i));
}
nums.remove(nums.size() - 1);
nums.remove(0); // 非常慢
for (Integer value : nums) {
    System.out.println(value);
}
```

### HashMap

```java
Map<Integer, String> m = new HashMap<>();
m.put(5, "Five");
m.put(8, "Eight");
m.put(6, "Six");
m.put(4, "Four");
m.put(2, "Two");
// 检索
System.out.println(m.get(6));
// Lambda forEach
m.forEach((key, value) -> {
    String msg = key + ": " + value;
    System.out.println(msg);
});
```

### ConcurrentHashMap

```java
ConcurrentHashMap<Integer, String> m
            = new ConcurrentHashMap<>();
m.put(100, "Hello");
m.put(101, "Geeks");
m.put(102, "Geeks");
// 移除
m.remove(101, "Geeks");

// 如果不存在，就添加，存在就不变更
m.putIfAbsent(103, "Hello");
 
// 替换
m.replace(101, "Hello", "For");
System.out.println(m);
```

### HashSet

```java
Set<String> set = new HashSet<>();
if (set.isEmpty()) {
    System.out.println("Empty!");
}
set.add("dog");
set.add("cat");
set.add("mouse");
set.add("snake");
set.add("bear");
if (set.contains("cat")) {
    System.out.println("Contains cat");
}
set.remove("cat");
for (String element : set) {
    System.out.println(element);
}
```

### ArrayDeque

```java
Deque<String> a = new ArrayDeque<>();
// 使用 add()
a.add("Dog");
// 使用 addFirst()
a.addFirst("Cat");
// 使用 addLast()
a.addLast("Horse");
// [Cat, Dog, Horse]
System.out.println(a);
// 访问元素
System.out.println(a.peek());
// 移除元素
System.out.println(a.pop());
```

杂项 Misc
----

### 访问修饰符
<!--rehype:wrap-class=col-span-2-->

| 修饰符    | Class | Package | Subclass | World |
|-------------|-------|---------|----------|-------|
| public      | Y     | Y       | Y        | Y     |
| protected   | Y     | Y       | Y        | _N_   |
| no modifier | Y     | Y       | _N_      | _N_   |
| private     | Y     | _N_     | _N_      | _N_   |
<!--rehype:className=show-header-->

### 常用表达

```java
String text = "I am learning Java";
// 删除所有空格
text.replaceAll("\\s+", "");
// 拆分字符串
text.split("\\|");
text.split(Pattern.quote("|"));
```

查看: [Regex in java](./regex.md#java-中的正则表达式)

### 注释 Comment

```java
// 我是单行注释！
 
/*
而我是一个
多行注释！
*/
/**
  * 这个
  * 是
  * 文档
  * 注释
 */
```

### 关键字
<!--rehype:wrap-class=col-span-2-->

- abstract
- continue
- for
- new
- switch
- assert
- default
- goto
- package
- synchronized
- boolean
- do
- if
- private
- this
- break
- double
- implements
- protected
- throw
- byte
- else
- import
- public
- throws
- case
- enum
- instanceof
- return
- transient
- catch
- extends
- int
- short
- try
- char
- final
- interface
- static
- void
- class
- finally
- long
- strictfp
- volatile
- const
- float
- native
- super
- while
<!--rehype:className=cols-7 style-none-->

### 数学方法

方法 | 说明
:-|:-
`Math.max(a,b)`       | `a` 和 `b` 的最大值
`Math.min(a,b)`       | `a` 和 `b` 的最小值
`Math.abs(a)`         | 绝对值
`Math.sqrt(a)`        | `a` 的平方根
`Math.pow(a,b)`       | `b` 的幂
`Math.round(a)`       | 最接近的整数
`Math.sin(ang)`       | 正弦
`Math.cos(ang)`       | `ang` 的余弦
`Math.tan(ang)`       | `ang` 的切线
`Math.asin(ang)`      | `ang` 的反正弦
`Math.log(a)`         | `a` 的自然对数
`Math.toDegrees(rad)` | 以度为单位的角度弧度
`Math.toRadians(deg)` | 以弧度为单位的角度度

### 异常 Try/Catch/Finally

```java
try {
  // something
} catch (Exception e) {
  e.printStackTrace();
} finally {
  System.out.println("always printed");
}
```

### 反射

```java
/**
* 利用反射动态加载依赖库
* java9及以上版本可用
* @param jar jar文件
*/
Method method = URLClassLoader.class.getDeclaredMethod("addURL", URL.class);
method.setAccessible(true);
MethodHandle addURL = lookup.unreflect(method);
URL url = jar.toURI().toURL();
URLClassLoader urlClassLoader = new URLClassLoader(new URL[] {url});
addURL.invoke(urlClassLoader, url);
//java8
Method method = URLClassLoader.class.getDeclaredMethod("addURL", URL.class);
method.setAccessible(true);
method.invoke(classLoader, url);
```

### util工具类

- `ArrayDeque` 提供 resizable-array 并实现 Deque 接
- `Arrays` 包含一个静态工厂，允许将数组视为列表
- `Collections` 包含对集合进行操作或返回集合的静态方法
- `Date` 表示特定的时间瞬间，精度为毫秒
- `Dictionary` 是任何类的抽象父类，例如 Hashtable，它将键映射到值
- `EnumMap` 一个专门用于枚举键的 Map 实现
- `EnumSet` 一个专门用于枚举键的 Set 实现
- `Formatter` 提供对布局对齐和对齐、数字、字符串和日期/时间数据的常用格式以及特定于语言环境的输出的支持
- `SecureRandom` 实例用于生成安全的伪随机数流
- `UUID` 表示一个不可变的通用唯一标识符
- `Vector` 实现了一个可增长的对象数组
- `LocalDate` 表示没有时区的日期，只包含年月日，不可变并且线程安全的，java8 及以上版本可用
- `LocalTime` 表示没有时区的时间，只包含时分秒，不可变并且线程安全的，java8 及以上版本可用
- `LocalDateTime` 表示没有时区的日期时间，同时包含年月日时分秒，不可变并且线程安全的，java8 及以上版本可用

设计模式
----

### 设计原则总结
<!--rehype:wrap-class=col-span-3-->

| 设计原则 | 一句话归纳 | 目的 |
| --- | --- | --- |
| 开闭原则 | 对扩展开放，对修改关闭 | 降低维护带来的新风险 |
| 依赖倒置原则 | 高层不应该依赖低层，要面向接口编程 | 更利于代码结构的升级扩展 |
| 单一职责原则 | 一个类只干一件事，实现类要单一 | 便于理解，提高代码的可读性 |
| 接口隔离原则 | 一个接口只干一件事，接口要精简单一 | 功能解耦，高聚合、低耦合 |
| 迪米特法则 | 不该知道的不要知道，一个类应该保持对其它对象最少的了解，降低耦合度 | 只和朋友交流，不和陌生人说话，减少代码臃肿 |
| 里氏替换原则 | 不要破坏继承体系，子类重写方法功能发生改变，不应该影响父类方法的含义 | 防止继承泛滥 |
| 合成复用原则 | 尽量使用组合或者聚合关系实现代码复用，少使用继承 | 降低代码耦合 |
<!--rehype:className=show-header-->

### 设计模式总结
<!--rehype:wrap-class=col-span-3-->

| 分类 | 设计模式 | 简述 | 一句话归纳 | 目的 | 生活案例 |
| --- | --- | --- | --- | --- | --- |
| 创建型设计模式（简单来说就是用来创建对象的） | 工厂模式（Factory Pattern） | 不同条件下创建不同实例 | 产品标准化，生产更高效 | 封装创建细节 | 实体工厂 |
|  | 单例模式（Singleton Pattern） | 保证一个类仅有一个实例，并且提供一个全局访问点 | 世上只有一个我 | 保证独一无二 | CEO |
|  | 原型模式（Prototype Pattern） | 通过拷贝原型创建新的对象 | 拔一根猴毛，吹出千万个 | 高效创建对象 | 克隆 |
|  | 建造者模式（Builder Pattern） | 用来创建复杂的复合对象 | 高配中配和低配，想选哪配就哪配 | 开放个性配置步骤 | 选配 |
| 结构型设计模式（关注类和对象的组合） | 代理模式（Proxy Pattern） | 为其他对象提供一种代理以控制对这个对象的访问 | 没有资源没时间，得找别人来帮忙 | 增强职责 | 媒婆 |
|  | 外观模式（Facade Pattern） | 对外提供一个统一的接口用来访问子系统 | 打开一扇门，通向全世界 | 统一访问入口 | 前台 |
|  | 装饰器模式（Decorator Pattern） | 为对象添加新功能 | 他大舅他二舅都是他舅 | 灵活扩展、同宗同源 | 煎饼 |
|  | 享元模式（Flyweight Pattern） | 使用对象池来减少重复对象的创建 | 优化资源配置，减少重复浪费 | 共享资源池 | 全国社保联网 |
|  | 组合模式（Composite Pattern） | 将整体与局部（树形结构）进行递归组合，让客户端能够以一种的方式对其进行处理 | 人在一起叫团伙，心在一起叫团队 | 统一整体和个体 | 组织架构树 |
|  | 适配器模式（Adapter Pattern） | 将原来不兼容的两个类融合在一起 | 万能充电器 | 兼容转换 | 电源适配 |
|  | 桥接模式（Bridge Pattern） | 将两个能够独立变化的部分分离开来 | 约定优于配置 | 不允许用继承 | 桥 |
| 行为型设计模式（关注对象之间的通信） | 模板模式（Template Pattern） | 定义一套流程模板，根据需要实现模板中的操作 | 流程全部标准化，需要微调请覆盖 | 逻辑复用 | 把大象装进冰箱 |
|  | 策略模式（Strategy Pattern） | 封装不同的算法，算法之间能互相替换 | 条条大道通罗马，具体哪条你来定 | 把选择权交给用户 | 选择支付方式 |
|  | 责任链模式（Chain of Responsibility Pattern） | 拦截的类都实现统一接口，每个接收者都包含对下一个接收者的引用。将这些对象连接成一条链，并且沿着这条链传递请求，直到有对象处理它为止。 | 各人自扫门前雪，莫管他们瓦上霜 | 解耦处理逻辑 | 踢皮球 |
|  | 迭代器模式（Iterator Pattern） | 提供一种方法顺序访问一个聚合对象中的各个元素 | 流水线上坐一天，每个包裹扫一遍 | 统一对集合的访问方式 | 逐个检票进站 |
|  | 命令模式（Command Pattern） | 将请求封装成命令，并记录下来，能够撤销与重做 | 运筹帷幄之中，决胜千里之外 | 解耦请求和处理 | 遥控器 |
|  | 状态模式（State Pattern） | 根据不同的状态做出不同的行为 | 状态驱动行为，行为决定状态 | 绑定状态和行为 | 订单状态跟踪 |
|  | 备忘录模式（Memento Pattern） | 保存对象的状态，在需要时进行恢复 | 失足不成千古恨，想重来时就重来 | 备份、后悔机制 | 草稿箱 |
|  | 中介者模式（Mediator Pattern） | 将对象之间的通信关联关系封装到一个中介类中单独处理，从而使其耦合松散 | 联系方式我给你，怎么搞定我不管 | 统一管理网状资源 | 朋友圈 |
|  | 解释器模式（Interpreter Pattern） | 给定一个语言，定义它的语法表示，并定义一个解释器，这个解释器使用该标识来解释语言中的句子 | 我想说”方言“，一切解释权都归我 | 实现特定语法解析 | 摩斯密码 |
|  | 观察者模式（Observer Pattern） | 状态发生改变时通知观察者，一对多的关系 | 到点就通知我 | 解耦观察者与被观察者 | 闹钟 |
|  | 访问者模式（Visitor Pattern） | 稳定数据结构，定义新的操作行为 | 横看成岭侧成峰，远近高低各不同 | 解耦数据结构和数据操作 | KPI考核 |
|   | 委派模式（Delegate Pattern） | 允许对象组合实现与继承相同的代码重用，负责任务的调用和分配 | 这个需求很简单，怎么实现我不管 | 只对结果负责 | 授权委托书 |
<!--rehype:className=show-header-->

另见
---

- [Java 官网](https://www.java.com/zh-CN/) _(java.com)_
