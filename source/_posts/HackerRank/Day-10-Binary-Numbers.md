---
title: Day 10 Binary Numbers
date: 2019-10-10 12:03:48
tags: hackerrank
keywords: 
description: 
---

输入一个正整数，转为二进制将二进制中连续的1的个数的最大值求出来。

**Task**
Given a base-10 integer,N , convert it to binary (base-2). Then find and print the base-10 integer denoting the maximum number of consecutive 1's in N's binary representation.



<!--more-->



```java
package com.luopandeng;

import java.util.Collections;
import java.util.HashSet;
import java.util.Scanner;

/**
 * @Author: LPD0155
 * @Date: 2019/10/10:11:43
 */


public class BinaryNumbers {

    private static final Scanner scanner = new Scanner(System.in);

    public static void main(String[] args) {
        int n = scanner.nextInt();
        scanner.skip("(\r\n|[\n\r\u2028\u2029\u0085])?");
        String s = Integer.toBinaryString(n);
        String[] split = s.split("0");
        HashSet<Integer> set = new HashSet<>();
        for (int i = 0; i < split.length; i++) {
            if (split[i]!=""&&!split[i].equals("")) {
                set.add(Integer.valueOf(split[i].length()));
            }
        }
        Integer max = Collections.max(set);
        System.out.println(max);
        scanner.close();
    }
}

```

