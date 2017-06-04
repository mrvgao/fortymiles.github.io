---
layout: post
title: "Computing Complexity 01"
permalink: /blog/computing-complexity-01/
author: "Gao Minquan"
date: 2017-03-16 11:27
category: Theoretical Computing
---

### Computing Complexity 01

### 1. Introduction of computing complexity

(Alex's communication centers problem)

### 2. Analyse Algorithm

#### 2.1 What could effect the running time of a program? 

+ input size
+ input content
+ type of computer we are using
+ amount of memory the computer has
+ how the algorithm is implemented
+ the programming language used.

#### 2.2 Simplification methods for analys algroithm.

+ Analyse without implementing
    + RAM model
+ Consider worst possible input. 
    + worst-cost running time
+ Ignore "unnecessary" details.
    + Big $O$ notation.
   
#### 2.3 RAM model. 

**Random Access Machine**

`simpler computer`

What are essential components of a computer model? 

[$\star$] memory         
[X] Graphic Card           
[X] Mouse         
[X] Moninter          
[X] File System             
[X] Operating System          
[X] CD-ROM           
[$\star$] Input/Output        
[$\star$] Programming Capability


Input & Program --> RAM  <----> Memory

1. "Simple" operations take 1 timestep.
2. Loops count as often as they run.
3. Memory access is free.

4. *We have as much memory as we need.*
5. *A unit of memory cannnot hold an arbitary large number.*


Quiz: 

    a = 1
    b = 2 * a
    
    # timesteps on ram? 
    
    s = 5
    while s > 0:        ## 6
        s = s - 1       ## 5
        
    # timesteps on ram? 
   
    
    String s[0], s[1], .. s[n-1]
    count = 0
    for c in s:
        if c == 'a':
            count += 1
            
    
    
#### 2.3 What Type of Analysis

##### Best-Case
##### Average-Case
##### Worst Case


    for index in len(string):
        if string[index] == 'a':
            if string[index+1] == 'b':
                count += 1
                 
    # aaaaaaaaaaaa => worst case
    # abababababab => worst case
    # acacacacacac => middle case
    # bbbbbbbbbbbb => best case
    

#### 2.4 Big-O notation

1. There're some numbers $n^{\prime}$, c, such that $ c \cdot g(n^{\prime}) \geq f(n^{\prime}) $
2. For all $ n^{\prime \prime} \gt n^{\prime} $, we have $ c \cdot g(n^{\prime \prime}) \geq f(n^{\prime \prime})$

==> $ f(n) \in O(g(n)) $

**Big O means that g(n) is a function that grows at least as fast as f(n) **



