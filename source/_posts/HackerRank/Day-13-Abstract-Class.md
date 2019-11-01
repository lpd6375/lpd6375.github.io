---
title: Day 13 Abstract Class
date: 2019-10-13 09:25:30
tags: hackerrank
keywords:
description:
---

 **Objective**
Today, we're taking what we learned yesterday about [*Inheritance*](https://docs.oracle.com/javase/tutorial/java/IandI/subclasses.html) and extending it to [*Abstract Classes*](https://docs.oracle.com/javase/tutorial/java/IandI/abstract.html). Because this is a very specific Object-Oriented concept, submissions are limited to the few languages that use this construct. Check out the [Tutorial](https://www.hackerrank.com/challenges/30-abstract-classes/tutorial) tab for learning materials and an instructional video! 



<!--more-->



![day13.1.png](/images/day13.1.png)

![day13.2.png](/images/day13.2.png)



Here is my solution:

```

abstract class Book {
    String title;
    String author;
    
    Book(String title, String author) {
        this.title = title;
        this.author = author;
    }
    
    abstract void display();
}

// Declare your class here. Do not use the 'public' access modifier.
    // Declare the price instance variable
    
    /**   
    *   Class Constructor
    *   
    *   @param title The book's title.
    *   @param author The book's author.
    *   @param price The book's price.
    **/
    // Write your constructor here
    
    /**   
    *   Method Name: display
    *   
    *   Print the title, author, and price in the specified format.
    **/
    // Write your method here
    
// End class

public class Solution {
   
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        String title = scanner.nextLine();
        String author = scanner.nextLine();
        int price = scanner.nextInt();
        scanner.close();

        Book book = new MyBook(title, author, price);
        book.display();
    }
}
```

