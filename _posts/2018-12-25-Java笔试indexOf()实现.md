---
layout:     post
title:      Java 关于链表的基本算法
subtitle:   链表
date:       2018-12-23
author:     柏梓涵
header-img: img/post-bg-java.jpg
catalog: true
tags:
    - Java
---

### indexOf源码解析

```java
public int indexOf(String str) {
    return indexOf(str, 0);
}
 
public int indexOf(String str, int fromIndex) {
    return indexOf(value, 0, value.length,str.value, 0, str.value.length, fromIndex);
}

static int indexOf(char[] source, int sourceOffset, int sourceCount, char[] target, int targetOffset, int targetCount, int fromIndex) {
    //1、当开始查找位置 大于等于 源字符串长度时,如果[查找字符串]为空,则:
    //返回字符串的长度,否则返回-1.
    if (fromIndex >= sourceCount) { 
        return (targetCount == 0 ? sourceCount : -1);
    }
    //2、如果fromIndex 小于 0,则从 0开始查找。
    if (fromIndex < 0) { 
        fromIndex = 0;
    }
    //3、如果[查找字符串]为空,则返回fromIndex
    if (targetCount == 0) { 
        return fromIndex;
    }
    //4、开始查找,从[查找字符串]中得到第一个字符,标记为first
    char first = target[targetOffset];
    //4.1、计算[源字符串最大长度]
    int max = sourceOffset + (sourceCount - targetCount);
    //4.2、遍历查找
    for (int i = sourceOffset + fromIndex; i <= max; i++) { 
        //4.2.1、从[源字符串]中,查找到第一个匹配到[目标字符串]first的位置 
        //for循环中,增加while循环 
        /* Look for first character. */ 
        if (source[i] != first) { 
            while (++i <= max && source[i] != first); 
        } 
        //4.2.2、如果在[源字符串]中,找到首个[目标字符串], 
        //则匹配是否等于[目标字符串] 
        /* Found first character, now look at the rest of v2 */ 
        if (i <= max) { 
            //4.2.2.1、得到下一个要匹配的位置,标记为j 
            int j = i + 1; 
            //4.2.2.2、得到其余[目标字符串]的长度,标记为end 
            int end = j + targetCount - 1; 
            //4.2.2.3、遍历,其余[目标字符串],从k开始, 
            //如果j不越界(小于end,表示:其余[目标字符串]的范围), 
            //同时[源字符串]==[目标字符串],则 //自增,继续查找匹配。j++、k++ 
            for (int k = targetOffset + 1; j < end && source[j] == target[k]; j++, k++); 
            //4.2.2.4、如果j与end相等,则表示: 
            //源字符串中匹配到目标字符串,匹配结束,返回i。 
            if (j == end) { 
                /* Found whole string. */ 
                return i - sourceOffset; 
            } 
        }
    }
    //其余情况,返回-1.return -1; 
    return -1;
} 
```

### 实现

>给定一个 haystack 字符串和一个 needle 字符串，在 haystack 字符串中找出 needle 字符串出现的第一个位置 (从0开始)。如果不存在，则返回  -1。

```java
public int strStr(String haystack, String needle) {
        if(needle.length() == 0) { //当noodle为空应该返回0
            return 0;
        } else if(needle.length() > haystack.length()) { //当needle长度大于haystack，返回-1
            return -1;
        } else {
            char first = needle.charAt(0);
            int max = haystack.length() - needle.length();
            for(int i = 0; i <= max; i++) {
                if(haystack.charAt(i) != first) {
                    while(++i <= max && haystack.charAt(i) != first);
                }
                if(i <= max) {
                    int j = i + 1;
                    int end = j + needle.length() - 1;
                    for(int k = 1; j < end && haystack.charAt(j) == needle.charAt(k); j++, k++);
                    if(j == end) {
                        return i;
                    }
                }
            }
            return -1;
        }
    }
    public int strStr2(String haystack, String needle) {
        if(needle.equals("")||haystack.equals(needle)){
            return 0;
        }
        int index=-1;
        if(haystack.contains(needle)){
            String[] str=haystack.split(needle); 
            if(str.length>=1){
                index=str[0].length();
            }else {
                index=0;
            }
        }else{
                index=-1;
            }
        return index;
    }
```