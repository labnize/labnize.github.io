title: js全排列算法
date: 2017-06-08 14:43:44
tags:
---

#### In this kata you have to create all permutations of an input string and remove duplicates, if present. This means, you have to shuffle all letters from the input in all possible orders.

##### Examples:

```
permutations('a'); // ['a']
permutations('ab'); // ['ab', 'ba']
permutations('aabb'); // ['aabb', 'abab', 'abba', 'baab', 'baba', 'bbaa']

```

​       

##### 对于这种问题，都是采用插空的方法。所以基本思路也就这样了，每次选一个字符，在剩余字符串中进行插空

> 对于这种问题，都是采用插空的方法。所以基本思路也就这样了，每次选一个字符，在剩余字符串中进行插空

​          

##### 实现过程

```
function permutations(string) {
  return (string.length == 1) ? [string] : string.split('').map(
     (e, i) => permutations(string.slice(0,i) + string.slice(i+1)).map((e2) => e+e2)
  ).reduce((r,e) => r.concat(e)).sort().filter((e,i,a) => (i==0) || a[i-1] != e);
}
```

​          

##### 运行结果

```
Test Results:
 permutations
 examples from description
Test Passed: Value == '[\'a\']'
Test Passed: Value == '[\'ab\', \'ba\']'
Test Passed: Value == '[\'aabb\', \'abab\', \'abba\', \'baab\', \'baba\', \'bbaa\']'
Completed in 4ms
Completed in 8ms
You have passed all of the tests! :)
```

