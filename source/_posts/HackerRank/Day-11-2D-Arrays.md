---
title: Day 11 2D Arrays
date: 2019-10-11 09:48:19
tags: hackerrank
keywords:
description:
---

**Context**
Given a 6 * 6 *2D Array*, A:

```
1 1 1 0 0 0
0 1 0 0 0 0
1 1 1 0 0 0
0 0 0 0 0 0
0 0 0 0 0 0
0 0 0 0 0 0
```

We define an hourglass in  A to be a subset of values with indices falling in this pattern in A's graphical representation:

```
a b c
  d
e f g
```

There are  16 hourglasses in A, and an *hourglass sum* is the sum of an hourglass' values.

**Task**
Calculate the hourglass sum for every hourglass in A, then print the *maximum* hourglass sum.



<!--more-->



```java
package com.luopandeng.hackerrank;

import java.util.*;

/**
 * @Author: LPD0155
 * @Date: 2019/10/11:10:03
 */


public class Day10 {

    private static final Scanner scanner = new Scanner(System.in);

    public static void main(String[] args) {
        int[][] arr = new int[6][6];
        for (int i = 0; i < 6; i++) {
            String[] arrRowItems = scanner.nextLine().split(" ");
            scanner.skip("(\r\n|[\n\r\u2028\u2029\u0085])?");
            for (int j = 0; j < 6; j++) {
                int arrItem = Integer.parseInt(arrRowItems[j]);
                arr[i][j] = arrItem;
            }
        }
        HashSet<Integer> result = new HashSet<>();
        for (int i = 0; i < arr.length-2; i++) {
            for (int j = 0; j < arr[i].length-2; j++) {
                //顶
                int top = arr[i][j] + arr[i][j+1] + arr[i][j+2];
//                System.out.println(top);
                int mid = arr[i + 1][j + 1];
//                System.out.println(mid);
                int bottom = arr[i+2][j] + arr[i+2][j+1] + arr[i+2][j+2];
                result.add(top+mid+bottom);
//                System.out.println(bottom+top+mid);
            }
        }
        System.out.println(Collections.max(result));
        scanner.close();
    }
}

```



My solution is not good. Perhaps there are some smart way to solve it.



Below is a another solution from others.

```java
import java.io.*;
import java.util.*;
import java.text.*;
import java.math.*;
import java.util.regex.*;

public class Solution {
    private static final int _MAX = 6; // size of matrix
    private static final int _OFFSET = 2; // hourglass width
    private static int matrix[][] = new int[_MAX][_MAX];
    private static int maxHourglass = -63; // initialize to lowest possible sum (-9 x 7)
    
    /** Given a starting index for an hourglass, sets maxHourglass
    *   @param i row 
    *   @param j column 
    **/
    private static void hourglass(int i, int j){
        int tmp = 0; // current hourglass sum
        for(int k = j; k <= j + _OFFSET; k++){
            tmp += matrix[i][k]; // top 3 elements
            tmp += matrix[i + _OFFSET][k]; // bottom 3 elements
        }
        tmp += matrix[i + 1][j + 1]; // middle element
        
        if(maxHourglass < tmp){
            maxHourglass = tmp;
        }
    }

    public static void main(String[] args) {
        // read inputs
        Scanner scan = new Scanner(System.in); 
        for(int i=0; i < _MAX; i++){
            for(int j=0; j < _MAX; j++){
                matrix[i][j] = scan.nextInt();
            }
        }
        scan.close();
        
        // find maximum hourglass
        for(int i=0; i < _MAX - _OFFSET; i++){
            for(int j=0; j < _MAX - _OFFSET; j++){
                hourglass(i, j);
            }
        }
        
        // print maximum hourglass
        System.out.println(maxHourglass);
    }
}
```

