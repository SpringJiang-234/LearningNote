## chapter2 变量和数据类型

### `Scanner`输入

#### 基础使用方法

```java
// 从控制台输入3位学生的成绩，然后计算平均分
public class Case03 {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        double score1 = scanner.nextDouble();
        double score2 = scanner.nextDouble();
        double score3 = scanner.nextDouble();
        double average = (score1 + score2 + score3) / 3;
        System.out.println("平均分：" + average);
    }
}
```

- 需要注意的是实例化时需要参数`System.in`

#### 输入验证

```java
Scanner sc = new Scanner(System.in);
System.out.println("请输入一个整数：");
//校验Scanner存储的数据中是否有下一个整数，如果Scanner中没有数据，
//则让用户输入,用户输入后再判断是否是整数
if(sc.hasNextInt()){ //sc.hasNextDouble();
    int number = sc.nextInt();//将Scanner中存储的整数取出来
    System.out.println(number);
} else {
    System.out.println("不要瞎整");
}
```

- 使用`hasNext`判断

  - 循环判断

    ```java
    Scanner scanner = new Scanner(System.in);
    int n = 0;
    while(!scanner.hasNextInt()){
        System.out.println("您输错了");
        scanner.next();
    }
    ```




## chapter4 循环结构

### `random`随机数

```java
// 获取 [0,1) 随机数
double r = Math.random();
```



## chapter5 多重循环

### Java 中的标号（标签 label）

```java
标号名称: 循环结构
```



## chapter6 数组

### 数组

####  基本数据类型的数组中默认值分别是什么

| 数据类型    | 数组中默认值 |
| ----------- | ------------ |
| `byte[]`    | `0`          |
| `short[]`   | `0`          |
| `int[]`     | `0`          |
| `long[]`    | `0`          |
| `double[]`  | `0.0`        |
| `float[]`   | `0.0f`       |
| `boolean[]` | `false`      |
| `char[]`    | `'\u0000'`   |
| `String[]`  | `null`       |



#### `arrayCopy`数组拷贝

语法：

```java
System.arrayCopy(原数组, 拷贝的开始位置, 目标数组, 存放的开始位置, 拷贝的元素个数);
```

实例：

```java
System.arraycopy(arr, 0, newArr, 0, count);
```

#### `copyOf`数组扩容

语法：

```java
数据类型[] 标识符 = Arrays.copyOf(原数组, 新数组的长度);
```

实例：

```java
String[] newArr = Arrays.copyOf(arr, arr.length + 1);
```



## chapter7 二维数组

### 数组排序

#### 冒泡排序

自己实现：

```java
// 冒泡排序：将数列10,70,55,80,25,60进行降序排列
int[] arr = new int[]{10,70,55,80,25,60};
// 外圈：排序比较次数
for(int i = 0; i < arr.length - 1; i ++){
    // 内侧：每次将最小的数字排到最后面
    for(int j = 0; j < arr.length - 1 - i; j ++){
        if(arr[j] < arr[j+1]){
            int t = arr[j];
            arr[j] = arr[j+1];
            arr[j+1] = t;
        }
    }
}

//输出结果看看
for(int i = 0; i < arr.length; i ++){
    System.out.print(arr[i]+" ");
}
```

##### 工具类`Arryas`实现排序`sort`

```java
Arrays.sort(数组名); //将数组中的元素进行升序排列
Arrays.toString(数组名);//将数组中的元素组装为一个字符串
```



#### 二分查找（折半查找）

有顺序的前提下才能进行查找。

自己实现：

```java
// 二分查找、折半查找：从数列95,93,87,86,79,72,60,53中快速找出元素60所处位置
int[] arr = new int[]{95,93,87,86,79,72,60,53};
int target = 60;

int left = 0;
int right = arr.length - 1;
int middle;

while(left < right){
    middle = (left + right) / 2;
    if(arr[middle] == target){
        System.out.println("目标所在位置： " + middle);
        return middle;
    }
    else if(arr[middle] > target){
        left = middle + 1;
    }
    else if(arr[middle] < target){
        right = middle - 1;
    }
}
System.out.println("找不到目标");
return -1;
```

要小心`left = middle + 1;`和`right = middle - 1;`写反。

### 二维数组

```java
// 从控制台录入5首音乐信息（包括名称、歌手、出版年月），并将这些信息存储在数组中。
String[][] music = new String[5][3];
Scanner scanner = new Scanner(System.in);
for(int i = 0; i < music.length; i ++){
    for(int j = 0; j < music[i].length; j ++){
        music[i][j] = scanner.next();
    }
}

System.out.println("[名称, 歌手, 出版年月]");
for(int i = 0; i < music.length; i ++){
    System.out.println(Arrays.toString(music[i]));
}
```

### 多维数组

```java
// 某学校一年级共有3个班，第一个班10人，第二个班8人，第三个班7人，现要求从控制台录入这3个班学生的成绩和年龄，并计算出每个班的平均成绩和平均年龄。

Scanner scanner = new Scanner(System.in);
double[][][] classrooms = new double[3][][];
classrooms[0] = new double[10][2];
classrooms[1] = new double[8][2];
classrooms[2] = new double[7][2];
for(int k = 0; k < classrooms.length; k ++){
    System.out.println("输入第" + (k + 1) + "个班的成绩和年龄：");
    System.out.println("[成绩, 年龄]");
    for(int i = 0; i < classrooms[k].length; i ++){
        for(int j = 0; j < classrooms[k][i].length; j ++){
            classrooms[k][i][j] = scanner.nextDouble();
        }
    }
}

for(int k = 0; k < classrooms.length; k ++){
    double averScore = 0;
    double averAge = 0;
    for(int i = 0; i < classrooms[k].length; i ++){
        averScore += classrooms[k][i][0];
        averAge += classrooms[k][i][1];
    }
    averScore /= classrooms[k].length;
    averAge /= classrooms[k].length;
    System.out.println("第" + (k + 1) + "个班的平均成绩和平均年龄分别为：" + averScore + "\t" + averAge);
}
```



## chapter11 封装

### 面向对象的三大特征

- 封装
- 继承
- 多态

### 常用包说明

`java.lang` 包：属于Java 语言开发包，该包中的类可以直接拿来使用，而不需要引入包。因此 `JVM` 会自动引入。比如我们经常使用的`System`、`String`、`Math`

`java.util` 包：属于Java 提供的一些使用类以及工具类。比如我们经常使用的`Scanner`

### `static`修饰符

#### 应用范围

`static` 修饰符只能用来修饰

- 类中定义的
  - 成员变量
  - 成员方法
  - 代码块以及
  - 内部类（内部类有专门章节进行讲解）

##### `static` 修饰成员变量

- `static` 修饰的成员变量称之为类变量。属于该类所有成员共享。

##### `static` 修饰成员方法

- `static` 修饰的成员方法称之为类方法。属于该类所有成员共享。

##### `static` 修饰代码块

- `static` 修饰的代码块称为静态代码块，在 `JVM` 第一次记载该类时执行。
- 因此，静态代码块只能够被执行一次，通常用于一些系统设置场景。



## chapter12 继承

### 子类

- 子类从其父类继承所有成员（字段，方法和嵌套类）。
- 构造方法不是成员，因此它们不会被子类继承，但是可以从子类中调用父类的构造方法。

### 继承

#### 继承范围

- 不论子类在什么包中，子类会继承父类中所有的`public`和`protected`成员（包括字段和方法）。
- 如果子类和父类在同一个包中，子类也会继承父类中受包保护的（默认的）成员。
- 子类不会继承父类中定义的`private`成员。尽管如此，如果父类有提供`public`或`protected`访问该字段的方法，这些方法也能在子类中被使用。

#### 方法的使用

- 如果一个对象赋值给其父类的引用，此时想要调用该对象的特有的方法，必须要进行强制类型转换

#### 构造方法

- 如果父类中定义了带参构造，并且没有定义无参构造，那么必须在子类的构造方法中显示的调用父类的带参构造
  - 否则会报错
  - 因为java规定：如果子类的构造方法没有明确调用父类的构造方法，Java编译器会自动插入一个父类无参构造的调用。
  - 使用super调用父类的构造方法时，必须为这个构造方法的第一条语句

### 重写

- 重写方法时访问修饰符的级别不能降低。

- 如果你的方法重写了父类的方法之一
  - 则可以通过使用关键字super来调用父类中被重写的方法。
  - 你也可以使用super来引用隐藏字段（尽管不建议使用隐藏字段）。

- 子类中的静态方法与父类中的静态方法具有相同的签名不属于方法重写。

  - 因为静态方法称之为类方法，跟对象无关，调用时只看对象的数据类型。

  - 实例：

    ```java
    StaticFather f = new StaticChild();
    f.show();
    StaticFather.show();
    StaticChild.show();
    ```

    此时`f.show();`的结果与`StaticFather.show();`一致。

### `final`修饰符

#### 应用范围

`final` 修饰符应该使用在类、变量以及方法上

##### `final` 修饰类

最终类，不可以被继承

##### `final` 修饰变量

对象构建时就完成初始化，常量

##### `final` 修饰方法

最终方法，不可以被重写



## chapter14 多态

### 编译时多态

体现在方法重载

### 运行时多态

体现在方法重写

#### 虚拟方法调用

#### `instanceof` 运算符

##### 语法

```java
对象名 instanceof 类名; 
```

- 主要应用在类型的强制转换上面
- 对转换的目标类型进行检测，如果是，则进行强制转换。这样可以保证程序的正常运行。

### `Object` 类常用方法

#### `getClass()`

##### 定义

```java
public final Class getClass()
```

##### 示例

```java
TV tv = new TV();
Class clazz = tv.getClass();//获取类的定义信息
String name = clazz.getSimpleName();//获取类名
String className = clazz.getName(); //获取类的全限定名

Class superClass = clazz.getSuperclass(); //获取父类的定义信息
String superName = superClass.getSimpleName();//获取父类的名称
String superClassName = superClass.getName(); //获取父类的全限定名

Class[] interfaceClasses = clazz.getInterfaces();
Class interfaceClass = interfaceClasses[0];
String interfaceName = interfaceClass.getSimpleName();//获取接口的名称
String interfaceClassName = interfaceClass.getName(); //获取接口的全限定名
```

#### `hashCode()`

##### 定义

```java
public int hashCode()
```

#### `equals(Object obj)`

##### 定义

```java
public boolean equals(Object obj)
```

##### 注意

- 重写`equals(Object obj)`时也要重写`hashCode()`

##### 重写示例

```java
package com.cyx.polymorphism.hashcode;
public class Student {
    private String name;
    private int age;
    public Student(String name, int age) {
        this.name = name;
        this.age = age;
    }
    
    //1. 比较内存地址
    //2. 检测是否是同一类型
    //3. 检测属性是否相同
    @Override
    public boolean equals(Object o) {
        if(this == o) return true;
        //比较类的定义是否一致
        if(this.getClass() != o.getClass()) return false;
        //类的定义一致，那么对象o就可以被强制转换为Student
        Student other = (Student) o;
        return this.name.equals(other.name) && this.age == other.age;
    }
    
    //hashCode()方法被重写之后，返回的值就不在是对象的内存地址
    @Override
    public int hashCode() {
        return name.hashCode() + age;
    }
}
```

#### `toString()`

##### 定义

```java
public String toString()
```

#### `finalize()`

##### 定义

```java
protected void finalize() throws Throwable
```

##### 不一定执行

- finalize() 方法的调用依赖于 JVM 的垃圾回收机制，而 System.gc() 只是建议 JVM 进行垃圾回收，并不保证立即执行。
- 因此，finalize() 可能不会在程序退出前被调用，导致你看不到日志输出。



## chapter15 异常

### 异常体系

#### 继承关系

- `Throwable`：所有异常的父类。常用方法：

  ```java
  public Throwable();//构造方法
  public Throwable(String message);//构造方法
  public String getMessage();//获取异常发生的原因
  public void printStackTrace(); //打印异常在栈中的轨迹信息
  ```

  

  - `Error`
  - `Exception`
    - `RuntimeException`
    - `Checked Exception`

### 异常处理

#### 五个关键字

`throw` 、`throws`、`try`、`catch`、`finally`

### 自定义异常

#### 实例

```java
/**
 * 用户名不存在异常
 *
 * 异常命名规范：场景描述+Exception
 */
public class UsernameNotFoundException extends Exception{
    public UsernameNotFoundException(){}
    public UsernameNotFoundException(String msg){
        super(msg);
    }
}
```

### 异常使用注意

- 运行时异常可以不处理。 
- 如果父类抛出了多个异常,子类覆盖父类方法时,只能抛出相同的异常或者是该异常的子集。(与协变返回类型原理一致) 
- 父类方法没有抛出异常，子类覆盖父类该方法时也不可抛出检查异常。此时子类产生该异常，只能捕获处理，不能声明抛出



## chapter16 字符串

### `String`

#### `String`类特性

- 无需引用直接使用（因为位于`java.lang`包中）
- `final`修饰，最终类
- 对象不可再被更改

#### 常用构造方法

```java
public String(String original);
public String(char value[]);
public String(char value[], int offset, int count);
public String(byte bytes[]);
public String(byte bytes[], int offset, int length);
public String(byte bytes[], Charset charset);//指定字符集
```

##### 构建UTF-8字符集

```java
Charset charset = Charset.forName("UTF-8");
```

#### 常用方法（特别常用：★）

##### 返回`int`类型

###### ★获取长度

```java
public int length();
```

###### 子串位置查找

```java
// 返回子串第一次出现的起始索引
public int indexOf(String str);

// 返回子串最后一次出现的起始索引
public int lastIndexOf(String str);
```



##### 返回`boolean`类型

###### ★字符串比较

```java
// 比较两个字符串是否相同（区分大小写）
public boolean equals(Object anObject);

// 忽略大小写比较两个字符串是否相同
public boolean equalsIgnoreCase(String anotherString); 
```

###### 字符位置查找

```java
// 查找字符位置（返回索引，从0开始）

// 返回字符第一次出现的索引，未找到返回-1
public int indexOf(int ch);

// 返回字符最后一次出现的索引，未找到返回-1
public int lastIndexOf(int ch);
```

###### 字符串匹配正则表达式

```java
//检测字符串是否匹配给定的正则表达式
public boolean matches(String regex);
```



##### 返回`String`或`String[]`类型

###### 字符串大小写转换

```java
public String toLowerCase(); // 将字符串转换为小写
public String toUpperCase(); // 将字符串转换为大写
```

###### ★字符串截取方法

```java
// 从指定位置截取到字符串末尾
public String substring(int beginIndex);

// 截取指定区间字符串（左闭右开）
public String substring(int beginIndex, int endIndex);
```

###### 字符串替换

```java
// 字符替换
public String replace(char oldChar, char newChar);
// 字符串替换
public String replace(CharSequence target, CharSequence replacement);
// 正则替换
public String replaceAll(String regex, String replacement);
```

###### ★字符串拼接

```java
public String concat(String str);//将字符串追加到末尾
```

###### 去除字符串两端的空白字符

```java
public String trim();
```

###### ★字符串分割

```java
//将字符串按照匹配的正则表达式分割
public String[] split(String regex);
```



##### 返回`char`或`char[]`或`byte[]`类型

###### ★获取指定位置字符
```java
// 获取特定索引的字符
public char charAt(int index);
```

###### 获取字符数组

```java
public char[] toCharArray();
```

###### 获取字节数组

```java
// 获取字节数组
public byte[] getBytes();
// 获取指定编码下的字节数组
public byte[] getBytes(Charset charset);
```



##### 检查字符串常量池

```java
public native String intern();
```

###### 示例

```java
/*将字符串s3放入字符串常量池，放入时会先检测常量池中是否存在s3字符串，如果字符串常量池中存在字符串s3，那么s5直接使用常量池中的s3字符串地址即可。如果不存在，则在常量池中创建字符串s3*/
String s5 = s3.intern();
```



### `StringBuilder`和`StringBuffer`

#### 特性

- 无需引用直接使用（因为位于`java.lang`包中）
- `final`修饰，最终类
- 对象可以实现字符序列的追加，不会产生新的对象，只是将这个字符序列保存在字符数组中

#### 常用构造方法

```java
public StringBuilder(); //构建一个StringBuilder对象，默认容量为16

public StringBuilder(int capacity);//构建一个StringBuilder对象并指定初始化容量

public StringBuilder(String str); //构建一个StringBuilder对象，并将指定的字符串存储在其中
```

#### 常用方法

##### 返回`StringBuilder`类型

###### ★追加

```java
//将一个字符串添加到StringBuilder存储区
public StringBuilder append(String str);

//将StringBuffer存储的内容添加StringBuilder存储区
public StringBuilder append(StringBuffer sb);
```

###### 删除指定区间存储的内容

```java
//将StringBuilder存储区指定的开始位置到指定的结束位置之间的内容删除掉
public StringBuilder delete(int start, int end);
```

###### 删除存储区指定下标位置存储的字符

```java
public StringBuilder deleteCharAt(int index);
```

###### 在StringBuilder存储区指定偏移位置处插入指定的字符串

```java
public StringBuilder insert(int offset, String str);
```

###### 将存储区的内容倒序

```java
public StringBuilder reverse();
```

##### 返回`int`类型

###### 获取指定字符串在存储区中的位置

```java
//获取指定字符串在存储区中第一次出现的位置
public int indexOf(String str); 

//获取指定字符串在存储区中最后一次出现的位置
public int lastIndexOf(String str);
```

### 对比

- 少量字符串：
  - `String`、`StringBuilder`和`StringBuffer`都是用来处理字符串的。在处理少量字符串的时候，它们之间的处理效率几乎没有任何区别。
- 处理大量字符串：
  - `String`类的对象不可再更改，因此在处理字符串时会产生新的对象，对于内存的消耗来说较大，导致效率低下。
  - `StringBuilder`和`StringBuffer`使用的是对字符串的字符数组内容进行拷贝，不会产生新的对象，因此效率较高。
- 多线程：
  - `StringBuffer`为了保证在多线程情况下字符数组中内容的正确使用，在每一个成员方法上面加了锁，有锁就会增加消耗，因此`StringBuffer`在处理效率上要略低于`StringBuilder`。