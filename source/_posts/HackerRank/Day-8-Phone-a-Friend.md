---
title: Day 8 Phone a Friend
date: 2019-10-08 14:56:17
tags: hackerrank
keywords: 解题记录
description:
---

**Task**
Given `n` names and phone numbers, assemble a phone book that maps friends' names to their respective phone numbers. You will then be given an unknown number of names to query your phone book for. For each `name` queried, print the associated entry from your phone book on a new line in the form `name=phoneNumber`; if an entry for `name` is not found, print `Not found` instead.

**Note:** Your phone book should be a Dictionary/Map/HashMap data structure.



<!--more-->





```java
package com.luopandeng;

import java.util.HashMap;
import java.util.Map;
import java.util.Scanner;

/**
 * @Author: LPD0155
 * @Date: 2019/10/8:14:12
 */


public class DicAndMap {
    public static void main(String []args){
        Scanner in = new Scanner(System.in);
        int n = in.nextInt();
        Map<String, Integer> aMap = new HashMap<String, Integer>(n);
        for(int i = 0; i < n; i++){
            String name = in.next();
            int phone = in.nextInt();
            // Write code here
            aMap.put(name, phone);
        }
        while(in.hasNext()){
            String s = in.next();
//             Write code here
            if (aMap.get(s)==null){
                System.out.println("Not found.");
            }else{
                System.out.println(s+"="+aMap.get(s));
            }
        }
        in.close();
    }
}

```

