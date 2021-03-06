语法基础要点
==========

> [书中代码和练习题目参考](http://www.learntosolveit.com/cprogramming/)

## 类型

* int 和 float 类型的取值范围取决于具体的机器，int通常16位，float通常32位

| 类型 | 大小 |
|-----|-----|
| char | 字符  一个字节大小|
|short | 短整形 |
|long | 长整形 |
|double | 双精度浮点型|
|int| 一般整形 |


## 语法等


printf 常用的几个例子

* %d 整数打印
* %6d 整数打印，至少6个字符宽度
* %f 浮点数打印
* %6.1 浮点数打印，至少6个字符宽度，小数点后面保留2位
* %o 表示八进制数
* %x 表示16进制数
* %c 表示字符
* %s 表示字符串
* %% 表示百分号

define

* define 定义常量，一般用大写字母，指令的末尾**没有分号**


条件语句

```
if(表达式)
	do some
else if(表达式)
	do some
else
	do some
```

循环语句

```
while(){

}

for(;;){

}
```


逻辑运算

* `&&` 与，比`或`优先级高
* `||` 或
* `!`  非



## API

* putchar(c) 单个字符输出函数,向终端输出一个字符,在 stdio.h 中定义
* c = getchar() 从输入设备中输入一个字符, 回车键结束，在 stdio.h 中定义
* `EOF` end of file, 文件结束符 定义在 stdio.h中


## getchar how test?

```bash
liuzhizhi@lzz-rmbp|tcpl # ./a.out <<< "HELLO"
6
```

