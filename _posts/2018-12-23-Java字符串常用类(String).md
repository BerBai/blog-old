---
layout:     post
title:      Java 字符串常用类
subtitle:   String 类
date:       2018-12-23
author:     涂诣
header-img: img/post-bg-java.jpg
catalog: true
tags:
    - Java
---

## 字符串查找
String 提供了两种查找字符串的方法，即 **indexOf** 与 **lastIndexOf** 方法。

### 1、indexOf（String s） 
该方法用于返回参数字符串s在指定字符串中首次出现的索引位置，当调用字符串的indexOf()方法时，会从当前字符串的开始位置搜索s的位置；如果没有检索到字符串s，该方法返回-1

```java
String str ="We are students";
int size = str.indexOf("a"); // 变量size的值是3
```

### 2、lastIndexOf(String str)

该方法用于返回字符串最后一次出现的索引位置。当调用字符串的lastIndexOf()方法时，会从当前字符串的开始位置检索参数字符串str，并将最后一次出现str的索引位置返回。如果没有检索到字符串str，该方法返回-1.

如果lastIndexOf方法中的参数是空字符串"" ，，则返回的结果与length方法的返回结果相同。

## 获取指定索引位置的字符
使用charAt()方法可将指定索引处的字符返回。

```java
String str = "hello word";
char mychar =  str.charAt(4);  // mychar的结果是o
```

## 获取子字符串
通过String类的substring()方法可对字符串进行截取。这些方法的共同点就是都利用字符串的下标进行截取，且应明确字符串下标是从0开始的。在字符串中空格占用一个索引位置。

### 1、substring(int beginIndex)

该方法返回的是从指定的索引位置开始截取知道该字符串结尾的子串。

```java
String str = "Hello word";
String substr = str.substring(3); //获取字符串，此时substr值为lo word
```

### 2、substring(int beginIndex,  int endIndex)

beginIndex : 开始截取子字符串的索引位置

endIndex：子字符串在整个字符串中的结束位置

```java
String str = "Hello word";
String substr = str.substring(0,3); //substr的值为hel
```

## 去除空格、标点等
trim() 方法返回字符串的副本，忽略前导空格和尾部空格。

```java
public static void main(String[] args) {
        //string去除空格
        String str="  hello   world  ";
        System.out.println(str);
 
        String str1=str.trim();//去除首尾空格
        System.out.println(str1);
 
        String str2=str.replace(" ","");//去掉所有空格,包括首尾,中间
        System.out.println(str2);
 
        String str3=str.replaceAll(" +","");//去掉所有空格,包括首尾,中间
        System.out.println(str3);
 
        String str4=str.replaceAll("\\s*",""); //可以替换大部分空白字符， 不限于空格 . 说明:\s 可以匹配空格、制表符、换页符等空白字符的其中任意一个
        System.out.println(str4);
 
        //string去除标点符号
        //正则表达式去除标点
        String stri="ss&*(,.~1如果@&(^-自己!!知道`什`么#是$苦%……Z，&那*()么一-=定——+告诉::;\"'/?.,><[]{}\\||别人什么是甜。";
        System.out.println(stri);
 
        String stri1=stri.replaceAll("\\p{Punct}","");//不能完全清除标点
        System.out.println(stri1);
 
        String stri2=stri.replaceAll("\\pP","");//完全清除标点
        System.out.println(stri2);
 
        String stri3=stri.replaceAll("\\p{P}","");//同上,一样的功能
        System.out.println(stri3);
 
        String stri4=stri.replaceAll("[\\pP\\p{Punct}]","");//清除所有符号,只留下字母 数字  汉字  共3类.
        System.out.println(stri4);
    }
}
```

```
//**效果如下**
hello   world  
hello   world
helloworld
helloworld
helloworld
ss&*(,.~1如果@&(^-自己!!知道`什`么#是$苦%……Z，&那*()么一-=定——+告诉::;"'/?.,><[]{}\||别人什么是甜。
ss1如果自己知道什么是苦……Z，那么一定——告诉别人什么是甜。
ss~1如果^自己知道`什`么是$苦Z那么一=定+告诉><||别人什么是甜
ss~1如果^自己知道`什`么是$苦Z那么一=定+告诉><||别人什么是甜
ss1如果自己知道什么是苦Z那么一定告诉别人什么是甜
```

## 字符串替换
replace(w) 方法可实现将指定的字符或字符串替换成新的字符或字符串

oldChar：要替换的字符或字符串

newChar：用于替换原来字符串的内容

如果要替换的字符oldChar在字符串中重复出现多次，replace()方法会将所有oldChar全部替换成newChar。需要注意的是，要替换的字符oldChar的大小写要与原字符串中字符的大小写保持一致。

```java
String str= "address";
String newstr = str.replace("a", "A");// newstr的值为Address
```

## 判断字符串的开始与结尾
startsWith()方法与endsWith()方法分别用于判断字符串是否以指定的内容开始或结束。这两个方法的返回值都为boolean类型。

### 1、startsWith(String prefix) 

该方法用于判断当前字符串对象的前缀是否是参数指定的字符串。

### 2、endsWith(String suffix) 
该方法用于判断当前字符串是否以给定的子字符串结束

## 判断字符串是否相等
    
### 1、equals(String otherstr)

如果两个字符串具有相同的字符和长度，则使用equals()方法比较时，返回true。同时equals()方法比较时区分大小写。

### 2、equalsIgnoreCase(String otherstr)

equalsIgnoreCase()方法与equals()类型，不过在比较时**忽略了大小写**。

## 按字典顺序比较两个字符串

compareTo()方法为按字典顺序比较两个字符串，该比较基于字符串中各个字符的Unicode值，按字典顺序将此String对象表示的字符序列与参数字符串所表示的字符序列进行比较。如果按字典顺序此String对象位于参数字符串之前，则比较结果为一个负整数；如果按字典顺序此String对象位于参数字符串之后，则比较结果为一个正整数；如果这两个字符串相等，则结果为0.

```java
str.compareTo(String otherstr);
```

## 字母大小写转换
字符串的toLowerCase()方法可将字符串中的所有字符从大写字母改写为小写字母，而tuUpperCase()方法可将字符串中的小写字母改写为大写字母。

```java
str.toLowerCase();
str.toUpperCase();
```
## 字符串分割
使用split()方法可以使字符串按指定的分隔字符或字符串对内容进行分割，并将分割后的结果存放在字符数组中。

```java
1 str.split(String sign);
```
sign为分割字符串的分割符，也可以使用正则表达式。

没有统一的对字符串进行分割的符号，如果想定义多个分割符，可使用符号“<kbd>|</kbd>”。例如，“,<kbd>|</kbd>=”表示分割符分别为“,”和“=”。

```java 
str.split(String sign, in limit);
```
该方法可根据给定的分割符对字符串进行拆分，并限定拆分的次数。

### 欢迎关注我的微信公众号

![微信公众号：柏战不殆](http://upload-images.jianshu.io/upload_images/3990834-c91d28f8be4121e4.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
