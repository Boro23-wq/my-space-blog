---
title: Asteroid Collision ☄️
description: 2020 most frequently asked 'Lyft' programming problem.
date: 2020-08-15
---

#### <ins class="sub-medium">Leetcode Medium</ins>

![asteroid-collision](https://hips.hearstapps.com/pop.h-cdn.co/assets/15/45/1446833427-asteroid-index03.gif)

## Problem Statement :

We are given an array <ins class="sub-ins-2">asteroids</ins> of integers representing asteroids in a row.

For each asteroid, the absolute value represents its size, and the sign represents its direction ( <ins class="sub-ins-2">+ve</ins> meaning <ins class="sub-ins-2">right</ins>, <ins class="sub-ins-2">-ve</ins> meaning <ins class="sub-ins-2">left</ins> ). Each asteroid moves at the same speed.

Find out the state of the asteroids after all collisions. If two asteroids meet, the smaller one will explode. If both are the same size, both will explode. Two asteroids moving in the same direction will never meet.

---

### **Example 1:**

```java
Input: asteroids = [5, 10, -5]
Output: [5, 10]
```

`Explanation: The 10 and -5 collide resulting in 10. The 5 and 10 never collide.`

### **Example 2:**

```java
Input: asteroids = [8, -8]
Output: []
```

`Explanation: The 8 and -8 collide exploding each other.`

### **Example 3:**

```java
Input: asteroids = [10, 2, -5]
Output: [10]
```

`Explanation: The 2 and -5 collide resulting in -5. The 10 and -5 collide resulting in 10.`

### **Example 4:**

```java
Input: asteroids = [-2, -1, 1, 2]
Output: [-2, -1, 1, 2]
```

`Explanation: The -2 and -1 are moving left, while the 1 and 2 are moving right. Asteroids moving the same direction never meet, so no asteroids will meet each other.`

**_Note:_**

- The length of asteroids will be at most 10000.
- Each asteroid will be a non-zero integer in the range [-1000, 1000]..

---

## Approach using Stack - [Accepted]

### Intuition

A row of asteroids is stable if no further collisions will occur. After adding a new asteroid to the right, some more collisions may happen before it becomes stable again, and all of those collisions (if they happen) must occur right to left. This is the perfect situation for using a stack.

---

### Algorithm

The first asteroid is always going to the stack since there are not enough asteroid already (in the stack) for collision.

For the second asteroid, if the asteroid is moving right (+ve), and the previous asteroid already in the stack is (+ve) or (-ve), then no collisions happen. Since the (-ve) asteroid will always move left, further apart. Also for the (+ve) asteroid since they both move towards the same direction at same speed, there won't be any collision.

For two asteroids to collide the left asteroid must be moving right and the right asteroid must be moving left. ()

- If <ins class="sub-ins-2">abs(new)</ins> < <ins class="sub-ins-2">abs(top)</ins>, then the new asteroid will blow up.
- If <ins class="sub-ins-2">abs(new)</ins> == <ins class="sub-ins-2">abs(top)</ins>, then both asteroids will blow up
- If <ins class="sub-ins-2">abs(new)</ins> > <ins class="sub-ins-2">abs(top)</ins>, then the top asteroid will blow up (and possibly more asteroids will, so we should continue checking.)

---

## Java Code :

#### <ins class="sub-ins">Time - O(n)</ins> | <ins class="sub-ins">Space - O(n)</ins>

```java
class Solution {
    public int[] asteroidCollision(int[] asteroids) {

        Stack<Integer> stack = new Stack<>();

        for (int i = 0; i < asteroids.length; i++){
            int currentAsteroid = asteroids[i];

            // handles positive number
            if (currentAsteroid > 0){
                stack.push(currentAsteroid);
            }

            // handles negative number
            while (!stack.isEmpty() && stack.peek() > 0 && -currentAsteroid > stack.peek()){
                stack.pop();
            }

            if (stack.isEmpty() || stack.peek() < 0) stack.push(currentAsteroid);
            else if (stack.peek() == -currentAsteroid) stack.pop();
        }

        int[] result = new int[stack.size()];

        for(int i = result.length - 1; i >= 0; i--) {
            result[i] = stack.pop();
        }
        return result;
    }
}
```

---

## Algorithm Steps :

- <ins class="sub-ins-2">Step-1</ins> : in the first iteration if asteroid is +ve add it to the stack.
- <ins class="sub-ins-2">Step-2</ins> : while if stack is not empty & top of the stack is a positive number & current asteroid >= top of the stack, pop from the stack.
- <ins class="sub-ins-2">Step-3</ins> : if top of the stack is negative, push the asteroid to the stack.
- <ins class="sub-ins-2">Step-4</ins> : if the current asteroid and the top of the stack is same then pop from the stack.
