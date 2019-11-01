---
title: Days 9 Recursion
date: 2019-10-08 16:09:37
tags: hackerrank
keywords:
description:
---

利用递归算法求阶乘。这个破系统不知道怎么回事，我都提交了，却显示我明天才能看题目。

**Task**
Write a *factorial* function that takes a positive integer,  N as a parameter and prints the result of  N (N factorial).

**Note:** If you fail to use recursion or fail to name your recursive function *factorial* or *Factorial*, you will get a score of 0.



<!--more-->



```java
package com.luopandeng;

import java.io.BufferedWriter;
import java.io.FileWriter;
import java.io.IOException;
import java.util.Scanner;

/**
 * @Author: LPD0155
 * @Date: 2019/10/8:15:16
 */


public class Recursion {

    // Complete the factorial function below.
    static int factorial(int n) {
        if (n <= 1) {
            return 1;
        } else {
            return n*factorial(n-1);

        }
    }

    private static final Scanner scanner = new Scanner(System.in);

    public static void main(String[] args) throws IOException {
        Scanner scanner = new Scanner(System.in);
        int n = scanner.nextInt();
        scanner.skip("(\r\n|[\n\r\u2028\u2029\u0085])?");
        int result = factorial(n);
        System.out.println(result);
        scanner.close();
    }

}

```

