---
title: Max Contiguous Subarray Sum (Kadane's Algorithm)
description: Cubic time to Linear time using Kadanes Algorithm.
date: 2020-08-03
---

Today we are looking at a very easy and convenient coding question to introduce you to the essence of <ins class="sub-ins-2">Dynamic</ins> <ins class="sub-ins-2">Programming</ins> and how can one implement dynamic programming to <ins class="sub-ins-2">optimise complexities.

We are going to approach the problem step-by-step and we will identify solutions as bad as a <ins class="sub-ins-2">cubic</ins> time or <ins class="sub-ins-2">quadratic</ins> time solution and optimise them to give us a solution in <ins class="sub-ins-2">linear</ins> time.

## Problem Statement:

Given an integer array 'nums', find the contiguous subarray **(containing at least one number)** which has the largest sum and return its 'sum'.

_Example:_

```java
Input: [-2,1,-3,4,-1,2,1,-5,4],
Output: 6

Explanation: [4,-1,2,1] has the largest sum = 6.
```

> **_Follow up:_** If you have figured out the O(n) solution, try coding another solution using the divide and conquer approach, which is more subtle.

---

## Approach-1

#### <ins class="sub-ins">CUBIC TIME - O(n^3)</ins>

```java
/*
      The outer 2 'for' loops will look through
      all possible windows in the array.

      We fix 'left' value and move 'right' value
      from that 'left' fixed value.

      Once we hit the rightmost end we now move the 'left' value by one
      and yet again move 'right' from the 'left'.
    */
    for (int left = 0; left < n; left++) {
      for (int right = left; right < n; right++) {
        // Let's investigate this window
        int windowSum = 0;

        // this loop takes care of all the items
        // within the left and the right bound
        for (int k = left; k <= right; k++) {
          windowSum += nums[k];
        }

        // Find the max
        maximumSubArraySum = Math.max(maximumSubArraySum, windowSum);
      }
    }

    return maximumSubArraySum;
  }
}
```

Here in Approach-1 we see, for every <ins class="sub-ins-2">window</ins> we do the same <ins class="sub-ins-2">repitive</ins> checks which is not optimal. Let us look at Approach-2 for a better efficiency.

## Approach-2

#### <ins class="sub-ins">QUADRATIC TIME - O(n^2)</ins>

```java
class Solution {
  public int maxContiguousSubarraySum(int[] nums) {
    int n = nums.length;
    int maximumSubArraySum = Integer.MIN_VALUE;

    for (int left = 0; left < n; left++) {
      int runningWindowSum = 0;

      for (int right = left; right < n; right++) {
        runningWindowSum += nums[right];

        // Does this window has the best sum we have seen so far?
        maximumSubArraySum = Math.max(maximumSubArraySum, runningWindowSum);
      }
    }

    return maximumSubArraySum;
  }
}
```

Here in Approach-2, we do <ins class="sub-ins-2">repititive</ins> checks as well. Well, how can we avoid this repitive checks that makes our algorithm perform slower. The answer for this is <ins class="sub-ins-2">Dynamic</ins> <ins class="sub-ins-2">Programming</ins>.

- The <ins class="sub-ins-2">intuition</ins> behind Dynamic Programming is that we can reuse <ins class="sub-ins-2">overlapping</ins> <ins class="sub-ins-2">subproblems</ins> and solving these subproblems can help us solve the bigger problem.
- Dynamic Programming is mainly an <ins class="sub-ins-2">optimization</ins> over plain recursion. Wherever we see a recursive solution that has<ins class="sub-ins-2"> repeated</ins> calls for same inputs, we can optimize it using Dynamic Programming.
- The idea is to simply store the <ins class="sub-ins-2">results</ins> of <ins class="sub-ins-2">subproblems</ins>, so that we do not have to <ins class="sub-ins-2">re-compute</ins> them when needed later.

Let us implement our solution using Dynamic Programming on our next approach.

## Approach-3

#### <ins class="sub-ins">LINEAR TIME - O(n)</ins>

> Heavy comments for you to understand what goes through each step.

```java
class Solution {
  public int maxContiguousSubarraySum(int[] nums) {
    /*
      The best maximum seen so far is the first
      element.

      The the best max ending at the first element
      is...the first element itself.
    */
    int maxSoFar = nums[0];
    int maxEndingHere = nums[0];

    /*
      We will loop through all the items in the array from index
      1 onward.
    */
    for (int i = 1; i < nums.length; i++) {
      /*
        We are inspecting the item at index i.

        We want to answer the question:
        "What is the Max Contiguous Subarray Sum we can achieve ending at index i?"

        We have 2 choices:

        maxEndingHere + nums[i] (extend the previous subarray best whatever it was)
          1.) Let the item we are sitting at contribute to this best max we achieved
          ending at index i - 1.

        nums[i] (start and end at this index)
          2.) Just take the item we are sitting at's value.

        The max of these 2 choices will be the best answer to the Max Contiguous
        Subarray Sum we can achieve for subarrays ending at index i.

        Example:

        index     0  1   2  3   4  5  6   7  8
        Input: [ -2, 1, -3, 4, -1, 2, 1, -5, 4 ]
                 -2, 1, -2, 4,  3, 5, 6,  1, 5    'maxEndingHere' at each point

        The best subarrays we would take if we took them:
          ending at index 0: [ -2 ]           (snippet from index 0 to index 0)
          ending at index 1: [ 1 ]            (snippet from index 1 to index 1) [we just took the item at index 1]
          ending at index 2: [ 1, -3 ]        (snippet from index 1 to index 2)
          ending at index 3: [ 4 ]            (snippet from index 3 to index 3) [we just took the item at index 3]
          ending at index 4: [ 4, -1 ]        (snippet from index 3 to index 4)
          ending at index 5: [ 4, -1, 2 ]     (snippet from index 3 to index 5)
          ending at index 6: [ 4, -1, 2, 1 ]  (snippet from index 3 to index 6)
          ending at index 7: [ 4, -1, 2, 1, -5 ]    (snippet from index 3 to index 7)
          ending at index 8: [ 4, -1, 2, 1, -5, 4 ] (snippet from index 3 to index 8)

        Notice how we are changing the end bound by 1 everytime.
      */
      maxEndingHere = Math.max(maxEndingHere + nums[i], nums[i]);

      // Did we beat the 'maxSoFar' with the 'maxEndingHere'?
      maxSoFar = Math.max(maxSoFar, maxEndingHere);
    }

    return maxSoFar;
  }
}
```

---

And there we go, we have solved the problem to find max contiguous subarray sum using Dynamic Programming. We have seen how we can <ins class="sub-ins-2">optimise</ins> a <ins class="sub-ins-2">cubic</ins> time solution to something as good as a <ins class="sub-ins-2">linear</ins> time. So, next time you encounter a recursive problem that needs to perform <ins class="sub-ins-2">repititive</ins> tasks, don't hesitate to use Dynamic Programming.

Happy Coding.
