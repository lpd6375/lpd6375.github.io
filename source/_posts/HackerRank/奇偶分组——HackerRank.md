---
title: 奇偶分组——HackerRank
date: 2019-10-07 12:59:55
tags: 算法 hackerrank
---

要求：给出一个字符串，把字符串中的字母按奇偶分成两组打印出来。



<!--more-->



我的解：

```java
package com.luopandeng;

import java.io.BufferedInputStream;
import java.util.ArrayList;
import java.util.List;
import java.util.Scanner;

public class EvenSplit {

    public static void main(String[] args) {
        Scanner sc = new Scanner(new BufferedInputStream(System.in));
        int T = sc.nextInt();
        List<List<String>> outter = new ArrayList<>();
        for (int i = 0; i < T; i++) {
            /*
            *这里是个坑，起初这个inner 是在循环外的。单个输入的时候能输出正确答案
            *但是输入一个以上的串时出现的情况是，outter这个列表里出现相同的值，且都为最后输入的那个
            *为什么会出现这种情况呢？这就不得不提到两概念了，值传递和引用传递。
            */
            List<String> innner = new ArrayList<>();
            String s = sc.next();
            char[] chars = s.toCharArray();
            StringBuilder evenChar = new StringBuilder();
            StringBuilder oddChar = new StringBuilder();
            for (int j = 0; j < chars.length; j++) {
                if (j % 2 != 0) {
                    oddChar.append(chars[j]);
                } else {
                    evenChar.append(chars[j]);
                }
            }
            innner.add(evenChar.toString());
            innner.add(oddChar.toString());
            outter.add(innner);
        }
        System.out.println(outter);
        for (int k = 0; k < outter.size(); k++) {
            System.out.println(outter.get(k).get(0) + " " + outter.get(k).get(1));
        }
        sc.close();
    }

}
```

## 值传递和引用传递

先来看在外面和在里面不同的输出结果。

|                          |                            |
| ------------------------ | -------------------------- |
| ![外面](/images/out.png) | ![里面](/images/inner.png) |

重点看红框里的部分。从hello拆出来的应该是在列表内的第一个列表内，从world拆出来的应该是在第二个列表里。

**（1）基本数据类型传值，对形参的修改不会影响实参；**
**（2）引用类型传引用，形参和实参指向同一个内存地址（同一个对象），所以对参数的修改会影响到实际的对象；**
**（3）String, Integer, Double等immutable的类型特殊处理，可以理解为传值，最后的操作不会修改实参对象。**

参考链接：[理解Java中的引用传递和值传递](https://www.cnblogs.com/binyue/p/3862276.html)

由此我们可以知道，当`inner` 在外面时 `outter` 每次`add`的都是 `inner` 对象的地址，一旦 `inner`的值发生变化 ，则`outter`也会发生变化，就算是已经加进去的也会发生改变；当`inner`在里面时，每一次循环都会重新建立一个`inner`对象，`outter`的`add`接收的都是新的对象，因此能得到正确答案。

另外，这道题目遇到的另一个问题是：`Scanner`接收输入的问题。有机会再总结。。。