---
title: 'Day 7: Arrays'
date: 2019-10-07 15:54:16
tags: hackerrank
keywords: 
description: the seventh
---

task:

Given an array, A , of  N integers, print A's elements in *reverse* order as a single line of space-separated numbers.

给定一个定长的数组，翻转这个数组。



<!--more-->



My solution:

```java
package com.luopandeng;

import java.util.Scanner;

/**
 * @Author: LPD0155
 * @Date: 2019:2019/10/7:14:14
 */


public class ReverseArray {

    private static final Scanner scanner = new Scanner(System.in);

    public static void main(String[] args) {
        int n = scanner.nextInt();
        scanner.skip("(\r\n|[\n\r\u2028\u2029\u0085])?");
        if (n >= 1 & n <= 1000) {
            int[] arr = new int[n];
            String[] arrItems = scanner.nextLine().split(" ");
            scanner.skip("(\r\n|[\n\r\u2028\u2029\u0085])?");
            for (int j = 0; j < arrItems.length; j++) {
                if (Integer.parseInt(arrItems[j]) < 1 || Integer.parseInt(arrItems[j]) > 10000) {
                    System.out.println("You just input a wrong number");
                }
            }
            for (int i = 0; i < n; i++) {
                int arrItem = Integer.parseInt(arrItems[i]);
                arr[i] = arrItem;
            }
            //all code goes here below
            int midT = 0;
            for (int i = 0; i < arr.length / 2; i++) {
                midT = arr[i];
                arr[i] = arr[arr.length - 1 - i];
                arr[arr.length - i - 1] = midT;
            }
            for (int i = 0; i < arr.length; i++) {
                System.out.print(arr[i] + " ");
            }
        } else {
            System.out.println("You just input a wrong number");
        }
        scanner.close();
    }
}

```

其他实现方法：

```java
//Collections.reverse()
public void invertUsingCollectionsReverse(Object[] array) {
    List<Object> list = Arrays.asList(array);
    Collections.reverse(list);
}
//使用Stream API实现:
Object[] invertUsingStreams(Object[] array) {
    return IntStream.rangeClosed(1, array.length)
      .mapToObj(i -> array[array.length - i])
      .toArray();
}

```

