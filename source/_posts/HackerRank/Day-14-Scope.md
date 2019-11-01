---
title: Day 14 Scope
date: 2019-10-14 10:51:29
tags: hackerrank
keywords:
description:
---

Today's challenge is so solve problem that you need to calculate maximum absolute sum of given a array every two.



<!--more-->



![day14.1](/images/day14.1.png)

![day14.2](/images/day14.2.png)



Here is my solution:

```java
package com.luopandeng.hackerrank;

import java.util.Collections;
import java.util.HashSet;
import java.util.Scanner;

/**
 * @Author: LPD0155
 * @Date: 2019/10/14:9:58
 */


class Difference {
    private int[] elements;
    public int maximumDifference;

    public Difference(int[] a) {
        this.elements = a;
    }

    public void computeDifference() {
        HashSet<Integer> integers = new HashSet<>();
        for (int i = 0; i < elements.length; i++) {
            for (int j = i; j < elements.length; j++) {
                integers.add(Math.abs(elements[i] - elements[j]));
            }
        }
        maximumDifference = Collections.max(integers);

    }

    // Add your code here

} // End of Difference class


public class Day14Scope {

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        int[] a = new int[n];
        for (int i = 0; i < n; i++) {
            a[i] = sc.nextInt();
        }
        sc.close();

        Difference difference = new Difference(a);

        difference.computeDifference();

        System.out.print(difference.maximumDifference);
    }


}

```





## Solution From Others:

```java
public Difference(int[] elements){
        this.elements = elements;
    }

    public void computeDifference(){
        Arrays.sort(elements);
        this.maximumDifference = Math.abs(elements[elements.length - 1] - elements[0]);
    }

```

