---
title: Palindrome Check (Rearrange Palindrome)
description: Check for palindromes in a string.
date: 2020-04-04
---

## Problem Statement:

Given a string, determine if there is a way to <ins class="sub-ins-2">arrange</ins> the string such that the string is a <ins class="sub-ins-2">palindrome</ins>. If such arrangements exists, return the palindrome (there may be many arrangements - return just one). Otherwise return false if no such palindrome exists.

**Example-1:**

```javascript
Input: racecar
Output: racecar
```

> Since 'racecar' is a palindrome.

**Example-2:**

```javascript
Input: racecara
Output: false
```

> Since 'racecara' can't be arranged to form a palindrome.

Let us dive into the solution code to understand how can we solve this problem.

---

## Solution:

#### <ins class="sub-ins">Time - O(n)</ins> | <ins class="sub-ins">Space - O(n)</ins>

#### <ins class="sub-ins-2">Step 1:</ins>

> Let us consider input as **'racecar'** for this example.

```javascript
let set = [...s].reduce((acc, curr) => {
  acc[curr] = acc[curr] ? (acc[curr] += 1) : 1
  return acc
}, {})
```

Here, in Step 1, the number of occurences of each character is stored in the set. The output will look something like:

> set --> { r : 2, a : 2, c : 2, e : 1}

---

#### <ins class="sub-ins-2">Step 2:</ins>

In Step 2, we use two variables <ins class="sub-ins-2">odd_char</ins> and <ins class="sub-ins-2">palindrome</ins> to keep track of the string.

```javascript
let odd_char = ""
let palindrome = ""
```

---

#### <ins class="sub-ins-2">Step 3:</ins>

```javascript
for (let c in set) {
  if (set[c] % 2 === 0) {
    palindrome += c.repeat(Math.floor(set[c] / 2))
  } else if (odd_char === "") {
    odd_char += c
    palindrome += c.repeat(Math.floor(set[c] / 2))
  } else {
    return false
  }
}
```

In Step 3:

- We check for all the keys (i.e. the characters in the set), if the occurences are <ins class="sub-ins-2">even</ins> (which we can get from the 'value' of the key-value pair) we add it to the <ins class="sub-ins-2">palindrome</ins> variable (occurences / 2) times.

- (occurences / 2) times since we only want to add <ins class="sub-ins-2">half</ins> of the string characters so we can <ins class="sub-ins-2">mirror</ins> the second half to <ins class="sub-ins-2">reconstruct</ins> a palindrome.

- While if its <ins class="sub-ins-2">odd</ins>, we add it to the <ins class="sub-ins-2">odd_char</ins> variable and also add it to the <ins class="sub-ins-2">palindrome</ins> string (occurences / 2) times.

**Note**: For a string to be a <ins class="sub-ins-2">palindrome</ins>, the string should contain <ins class="sub-ins-2">even</ins> number of <ins class="sub-ins-2">occurences</ins> of the same character except one, which can be placed in between the string to form a palindrome.

- If there is a second character that has <ins class="sub-ins-2">odd</ins> <ins class="sub-ins-2">occurrences</ins>, it cannot be added to the <ins class="sub-ins-2">odd_char</ins> variable since we can't form palindromes with strings having <ins class="sub-ins-2">two</ins> or <ins class="sub-ins-2">more</ins> characters occuring in odd numbers.

---

#### <ins class="sub-ins-2">Step 4:</ins>

```javascript
return palindrome + odd_char + palindrome.split("").reverse().join("")
```

In Step 4, we return <ins class="sub-ins-2">palindrome</ins> + <ins class="sub-ins-2">odd_char</ins> + <ins class="sub-ins-2">reverseOf(palindrome)</ins> to form the palindrome string. If we don't find any string we would return **false**.

---

### Complete Code:

```javascript
var findPalindrome = function (s) {
  let set = [...s].reduce((acc, curr) => {
    acc[curr] = acc[curr] ? (acc[curr] += 1) : 1
    return acc
  }, {})

  let odd_char = ""
  let palindrome = ""

  for (let c in set) {
    // if even count add it to palindrome
    if (set[c] % 2 === 0) {
      palindrome += c.repeat(Math.floor(set[c] / 2))
      //if odd add to the odd_char and also to the palindrome,
      //and add the extra letter to the palindrome
    } else if (odd_char === "") {
      odd_char += c
      palindrome += c.repeat(Math.floor(set[c] / 2))
    } else {
      return false
    }
  }
  return palindrome + odd_char + palindrome.split("").reverse().join("")
}

findPalindrome("nolemonnomelon") // nnoolemameloonn
// findPalindrome("racecar") // racecar
// findPalindrome("mygym") //mygym
// findPalindrome("nogymn") // false
// findPalindrome("racecara") // false
```
