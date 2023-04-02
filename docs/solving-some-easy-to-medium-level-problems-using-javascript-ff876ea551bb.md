# 使用 JavaScript 解决一些简单到中等水平的问题

> 原文：<https://javascript.plainenglish.io/solving-some-easy-to-medium-level-problems-using-javascript-ff876ea551bb?source=collection_archive---------8----------------------->

## 用 JavaScript 解决一些容易到中级问题的算法。

![](img/997d59bdc9ccae90438aee2234046630.png)

嗨伙计们！问题解决是软件开发的核心。从仔细分析一个问题到实现高效的解决方案，这是一件有趣而又具有挑战性的事情。在直接开始编码之前，花些时间思考问题并消除任何疑虑总是一个好主意。

所以，我们滚动求解。

1.  编写一个算法，该算法采用一个数组并将所有的零移动到末尾，保留其他元素的顺序。

```
// input: [false,1,0,1,2,0,1,3,"a"]
// output: [false,1,1,2,1,3,"a",0,0]var moveZeros = function (arr) {
  return [
    ...(arr.filter(n => n !== 0)),
    ...(arr.filter(n => n === 0))
  ];
}
```

2.找出整数数组中所有和等于给定数字的对。

```
// input: array=[2,3,12,3,5,0,8,23,-1,2]; sum=5
// output:  [2, 3],[2, 3],[3, 2],[3, 2], 5, 0]function findPairsWithSum(arr, S) {
 const sum = [];
  for(let i = 0; i< arr.length; i++) {
    for(let j = i+1;  j < arr.length; j++) {
      if(S == arr[i] + arr[j]) sum.push([arr[i],arr[j]])
    }
  }
 return sum
}
```

3.可能的最长连续数字序列的长度。

```
// input: [4, 6, 9, 1, 2, 8, 5, 3, -1];
// output: 6 * ; 1, 2, 3, 4, 5, 6*const getLongestConseqSeq = (arr) => {
    const len=arr.length;
    let max = 0, count =0;

    arr.sort((a, b) => a-b);
    let newArr = [];
    newArr.push(arr[0]); for (let i=1; i<len; i++) {
        if(arr[i] != arr[i-1]) newArr.push(arr[i]);
     } for(let i=0; i<newArr.length; i++) {
        if(i >0 && newArr[i] == newArr[i-1]+1) count++;
        else count =1; max = Math.max(max, count);
    }
    return max;
}
```

4.反转单向链表。

```
// input: {"data":1,"next":{"data":2,"next":{"data":3,"next":{"data":4,"next":{"data":5,"next":{"data":5,"next":{"data":6}}}}}}}// output: {"data":6,"next":{"data":5,"next":{"data":5,"next":{"data":4,"next":{"data":3,"next":{"data":2,"next":{"data":1,"next":null}}}}}}}const reverseLinkedList = (list) => {
    let reversed = null;
    while(list) {
        const temp = list;
        list = list.next;
        temp.next = reversed;
        reversed = temp;
    }
    return reversed;
}
```

5.找出一个字符串的所有排列。

```
// input: wow
// output: ['wow', 'wwo', 'oww']const permuteStr = (str = '') => {
    if(!str) return;
    if(str.length < 2) return str;
    const permutations = []; for (let i=0;i<str.length; i++) {
       let char = str[i];
       if(str.indexOf(char) !== i) continue;
       const restStr = str.slice(0,i) + str.slice(i + 1, str.length);
       for(let permute of permuteStr(restStr)) {
            permutations.push(char+permute)
        }
    }
    return permutations;
}
```

6.删除单链表中从末尾开始的第 N 个*节点。*

```
// input: head = {"data":1,"next":{"data":2,"next":{"data":3,"next":{"data":4,"next":{"data":5,"next":{"data":5,"next":{"data":6}}}}}}}; key = 2// output: {"data":1,"next":{"data":2,"next":{"data":3,"next":{"data":5,"next":{"data":6}}}}}function deleteNode(head, key) {
    var first = head;
    var second = head; for (i = 0; i < key; i++) {
       if (second.next == null) {
          if (i == key - 1) head = head.next;
          return;
       }
       second = second.next;
     }
     while (second.next != null) {
          first = first.next;
          second = second.next;
       }

     first.next = first.next.next;
     return head;
}
```

7.找出给定数字的所有质因数。

```
// input: 100
// output: [5,2]const findPrimes = num => {
    const isPrime = num => {
        for(let i=2; i<= Math.sqrt(num); i++) {
            if(num % i === 0) return false;
        }
        return true;
    }
    let factors = [];
    for(let i=2; i<= num; i++) {
        while(isPrime(i) && num % i === 0) {
            if(factors.indexOf(i) == -1) factors.push(i);
            num /= i;
        }
    }
    return factors;
}
```

8.给定一个整数数组，求相邻子数组的最大和。

```
// input: [-2,1,-3,4,-1,2,1,-5,4]
// output: 6const maxSumOfSubArr = arr => {
  let a1 = 0
  let a2 = arr[0]
  arr.forEach((i, a) => {
    a1 = Math.max(i, a1 + i)
    a2 = Math.max(a2, a1)
  })
  return a2
}
```

9.从字符串中查找第一个不重复的字符。

```
// input: aabcbd
// output: cconst findFirstNonRepeated = str => {
    let first;
    str.split('').some((char, index, obj) => {
        if(obj.indexOf(char) === obj.lastIndexOf(char)) {
            first = char;
            return true;
        }
        return false;
    });
    return first;
}
```

10.给定一个数组，反转由连续 k 个元素组成的每个子数组。

```
// input: k = 3; arr = [1,2,3,4,5]
// output: [3,2,1,5,4]const reverseArrGroup = (arr, k) => {
    const len = arr.length;
    for(let i=0; i<len; i+=k) {
        let left = i;
        let right = Math.min(i+k-1, len-1); let temp;
        while(left<right) {
            temp = arr[left];
            arr[left] = arr[right];
            arr[right] = temp;
            left += 1;
            right -= 1;
        }
    }
    return arr;
}
```

这就是这篇文章的全部内容。感谢阅读！

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *，加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。***