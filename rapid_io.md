# acm模式
之前一直是在leetcode上做题，核心代码模块和现在的oj平台不一样，正好要准备校内的acm比赛，就此记录一下这二者的区别



### 为什么 cout 和 cin 比 scanf 和 printf 要慢？

首先在c++中时可以使用scanf和printf的，用习惯了c++的输入输出方式，这里有必要回顾一下前者的具体写法： 

* printf函数： 
  ~~~c++
  printf("%d", num); // %s %d %c %f
  ~~~ 
* scanf函数:
  ~~~c++
  printf("%d", &num); //参数是读取数据的地址
  ~~~ 

下面来解释二者速度上的区别：   
* 标准流对象cin/cout为了普适性，**继承体系很复杂**，所以在对象的构造等方面会影响效率，因此总体效率比较低。
* cin和cout会**从缓存区读取和写入数据**，所以速度较慢

如何加速cin/cout?   


~~~c++
    //在main函数头部加上一下代码
    ios::sync_with_stdio(0);
    cin.tie(nullptr);
    cout.tie(nullptr);
~~~

### 输出保留小数位数

保留数值的形式有两个参数，一个是数的总位数（整数 + 小数），另一个是保留的小数位数，二者要结合使用才能达到想到的效果：

c++的输出
~~~c++
    //c++
    #include<iomanip> // 包含头文件

    int num = 1243.234;
    cout << setprecision(5) << num; // 输出5位数字 1243.2
    cout << fixed << setprecision(3) << num; // 输出小数点后5位1243.234

~~~   

c语言的输出
~~~c
    // c语言
    %n.xf // 输出总位数为n， 小数位数为x

~~~