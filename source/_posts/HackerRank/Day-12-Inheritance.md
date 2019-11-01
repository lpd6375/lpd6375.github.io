---
title: Day 12 Inheritance
date: 2019-10-12 10:50:24
tags: hackerrank
keywords:
description:
---

today's challenge is inheritance. given a class you need to complete some methods that calculate the average score of a student and return a mark which is given in the initial script. And here is my solution below.



<!--more-->



![1](/images/day12.1.png)

![2](/images/day12.2.png)

```java
package com.luopandeng.hackerrank;

import java.util.Scanner;

/**
 * @Author: LPD0155
 * @Date: 2019/10/12:10:29
 */


class Inheritance {
    class Person {
        protected String firstName;
        protected String lastName;
        protected int idNumber;

        // Constructor
        Person(String firstName, String lastName, int identification){
            this.firstName = firstName;
            this.lastName = lastName;
            this.idNumber = identification;
        }

        // Print person data
        public void printPerson(){
            System.out.println(
                    "Name: " + lastName + ", " + firstName
                            + 	"\nID: " + idNumber);
        }

    }

    class Student extends Person{
        private String firstName;
        private String lastName;
        private int id;
        private int[] testScores;

        public Student(String firstName, String lastName, int identification) {
            super(firstName, lastName, identification);
        }

        public Student(String firstName, String lastName, int identification,  int[] testScores) {
            super(firstName, lastName, identification);
            this.testScores = testScores;
        }

        public String calculate() {
            int sum = 0;
            for (int i = 0; i < testScores.length; i++) {
                sum+=testScores[i];
            }
            int average = sum/testScores.length;
            if (average>=90){
                return "O";
            }else if (average>=80&&average<90){
                return "E";
            }else if (average>=70&&average<80){
                return "A";
            }else if (average>=55&&average<70){
                return "P";
            }else if (average>=40&&average<55){
                return "D";
            }
            return "T";
        }
    }

    class Solution {
        public void main(String[] args) {
            Scanner scan = new Scanner(System.in);
            String firstName = scan.next();
            String lastName = scan.next();
            int id = scan.nextInt();
            int numScores = scan.nextInt();
            int[] testScores = new int[numScores];
            for(int i = 0; i < numScores; i++){
                testScores[i] = scan.nextInt();
            }
            scan.close();

            Student s = new Student(firstName, lastName, id, testScores);
            s.printPerson();
            System.out.println("Grade: " + s.calculate() );
        }
    }
}

```





### solution from others

```java
class Student extends Person{
    private int[] testScores;
    
    Student(String firstName, String lastName, int identification, int[] scores){
		super(firstName, lastName, identification);
		this.testScores = scores;
	}
	
	public char calculate(){
		int average = 0;
		for(int i = 0; i < testScores.length; i++){
			average += testScores[i];
		}
		average = average / testScores.length;
		
		if(average >= 90){
			return 'O'; // Outstanding
		}
		else if(average >= 80){
			return 'E'; // Exceeds Expectations
		}
		else if(average >= 70){
			return 'A'; // Acceptable
		}
		else if(average >= 55){
			return 'P'; // Dreadful
		}
		else if(average >= 40){
			return 'D'; // Dreadful
		}
		else{
			return 'T'; // Troll
		}
	}
}
```

