# 一、 java基础

## 1. CMD人机交互

windows中使用命令行：CMD

如何打开CMD以及CMD的常用命令

### 1.1 打开CMD

打开就完事了！

win+E：打开我的电脑

### 1.2 CMD常用的命令：

```
-   盘符名称 + 冒号  ：  盘符切换
-   dir              ：  查看当前路径下的内容（也会展示隐藏的东西）
-   cd 目录(文件夹)  ：  进入单级目录
-   cd ..            ：  回退到上一级目录
```

![image-20240105233429886](../../images/image-20240105233429886.png)

```
- cd 目录1\目录2\...    :     进入多级目录
- cd \                  :     回退到盘符目录
- cls                   :     清屏
- exit                  :     退出命令行
/* 注意斜杠的方向 */
```

### 1.3 练习：

1.   利用cmd打开自己电脑上的QQ：这种方式太麻烦了

```
C:\Users\20866>D:

D:\>cd D:\SoftwareInstall\TencentQQ\Bin

D:\SoftwareInstall\TencentQQ\Bin>qq.exe
```

2.   在任意的目录下面都能打开qq：将QQ的路径记录在电脑的环境变量。（系统变量的path里面）

## 2. 代码

```java
char[] chs = new char[52];
for (int i = 0; i < chs.length; i++) {
    if (i <= 25) {
        // 小写字母
        chs[i] = (char) (97 + i);
    } else {
        // 大写字母
        chs[i] = (char) (65 + i - 26);
    }

}

for (int i = 0; i < chs.length; i++) {
    System.out.print(chs[i] + " ");
}

// a b c d e f g h i j k l m n o p q r s t u v w x y z A B C D E F G H I J K L M N O P Q R S T U V W X Y Z
```











