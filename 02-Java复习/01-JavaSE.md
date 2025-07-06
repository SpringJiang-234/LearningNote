## chapter2

### Scanner输入

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



## chapter4

### 随机数

```java
// 获取 [0,1) 随机数
double r = Math.random();
```

