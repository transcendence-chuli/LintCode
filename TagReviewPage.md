 
 
 
## Merge Sort (1)
**0. [MergeSort.java](https://github.com/awangdev/LintCode/blob/master/Java/MergeSort.java)**      Level: Medium
      

#### Merge Sort
- Divide and conquer, recursively
- 先从中间分段, merge sort 左边 (dfs), merge sort 右边
- 最后merge起来
- merge的时候因为是做int[], 所以没办法必须要O(n) space
- Time O(nlogn), Space O(n)



---




 
 
 
## String (30)
**0. [Judge Route Circle.java](https://github.com/awangdev/LintCode/blob/master/Java/Judge%20Route%20Circle.java)**      Level: Easy
      

简单的character checking. 各个方向, 加加减减.



---

**1. [First Unique Character in a String.java](https://github.com/awangdev/LintCode/blob/master/Java/First%20Unique%20Character%20in%20a%20String.java)**      Level: Easy
      

方法1: 按照题意, 找到第一个 first index == last index的字母.

方法2: 用hashmap存字母的index, 有些重复字母的index就会是个list. 找到单一index, 结合成list, sort, return list.get(0)



---

**2. [Reverse Vowels of a String.java](https://github.com/awangdev/LintCode/blob/master/Java/Reverse%20Vowels%20of%20a%20String.java)**      Level: Easy
      

vowels: 元音字母. 要求reverse所有元音字母.

##### 方法1: two pointer.
- 前后两个指针, 在while loop里面跑.
- 注意 i<j, 一旦相遇, 就break.
- 找到合适的, 就做swap.
- StringBuffer可以 sb.setCharAt()记得用.
- O(n)
##### 方法2:
拿出所有vowels, 反过来放进去. O(n)



---

**3. [Scramble String.java](https://github.com/awangdev/LintCode/blob/master/Java/Scramble%20String.java)**      Level: Hard
      

- 给两个string S, T. 检验他们是不是scramble string.
- scramble string 定义: string可以被分拆成binary tree的形式, 也就是切割成substring;
- 旋转了不是leaf的node之后, 形成新的substring, 这就是原来string的 scramble.


#### Interval DP 区间型
- 降维打击, 分割, 按照长度来dp.
- dp[i][j][k]: 数组S从index i 开始, T从index j 开始, 长度为k的子串, 是否为scramble string

##### Break down
- 一切两半以后, 看两种情况: , 或者不rotate这两半. 对于这些substring, 各自验证他们是否scramble.
- 不rotate分割的两半: S[part1] 对应  T[part1] && S[part2] 对应  T[part2]. 
- rotate分割的两半: S[part1] 对应  T[part2] && S[part2] 对应  T[part1]. 

##### Initialization
- len == 1的时候, 其实无法旋转, 也就是看S,T的相对应的index是否字符相等.
- initialization非常非常重要. 很神奇, 这个initailization 打好了DP的基础, 后面一蹴而就, 用数学表达式就算出了结果.
- input s1, s2 在整个题目的主要内容里面, 几乎没有用到, 只是用在initialization时候.
- More details, 看解答



---

**4. [Interleaving String.java](https://github.com/awangdev/LintCode/blob/master/Java/Interleaving%20String.java)**      Level: Hard
      

双序列DP, 从最后点考虑.
拆分问题的末尾, 考虑和s1, s2 subsequence之间的关联.

求存在性, boolean




---

**5. [Letter Combinations of a Phone Number.java](https://github.com/awangdev/LintCode/blob/master/Java/Letter%20Combinations%20of%20a%20Phone%20Number.java)**      Level: Medium
      

方法1: Iterative with BFS using queue.

方法2: Recursively adding chars per digit



---

**6. [Edit Distance.java](https://github.com/awangdev/LintCode/blob/master/Java/Edit%20Distance.java)**      Level: Hard
      

两个字符串, A要变成B, 可以 insert/delete/replace, 找最小变化operation count

#### Double Sequence
- 考虑两个字符串变换的最后点: 需要insert/delete/replace? 分析每种情况, 然后列出表达式.
- 先calculate最坏的情况, 3种operation count + 1; 然后在比较match的情况.
- 注意, 在i或者j为0的时候, 变成另外一个数字的steps只能是全变.
- 第一步, 空间时间都是O(MN)
- 滚动数组优化, 空间O(N)

#### Search



---

**7. [Distinct Subsequences.java](https://github.com/awangdev/LintCode/blob/master/Java/Distinct%20Subsequences.java)**      Level: Hard
      

Double Sequence DP:
0. DP size (n+1): 找前nth的结果, 那么dp array就需要开n+1, 因为结尾要return dp[n][m]
1. 在for loop 里面initialize dp[0][j] dp[i][0]
2. Rolling array 优化成O(N): 如果dp[i][j]在for loop里面, 就很好替换 curr/prev



---

**8. [Regular Expression Matching.java](https://github.com/awangdev/LintCode/blob/master/Java/Regular%20Expression%20Matching.java)**      Level: Review
      



---

**9. [Wildcard Matching.java](https://github.com/awangdev/LintCode/blob/master/Java/Wildcard%20Matching.java)**      Level: Hard
      

Double sequence DP. 与regular expression 很像.

注意1: 分析字符 ?, * 所代表的真正意义, 然后写出表达式.
注意2: 搞清楚initialization 的时候 dp[i][0] 应该always false.当p为empty string, 无论如何都match不了 (除非s="" as well)
    同时 dp[0][j]不一定是false. 比如s="",p="*" 就是一个matching.



---

**10. [Add Binary.java](https://github.com/awangdev/LintCode/blob/master/Java/Add%20Binary.java)**      Level: Easy
      

方法一:土办法没技术，把binary换成数字，加起来，再换成binary。如果input很大，那么很可能int,long都hold不住。不保险。

方法二:一般方法，string化为charArray,然后逐位加起，最后记得处理多余的一个carry on
注意: 需要从末尾加起来, 所以要用一个diff来帮助  shortArray[i-diff] 指向 shortArray的相对应index.



---

**11. [Longest Substring Without Repeating Characters.java](https://github.com/awangdev/LintCode/blob/master/Java/Longest%20Substring%20Without%20Repeating%20Characters.java)**      Level: Medium
      

方法1:
Two Pointers
双指针: 从start开始遍历, 但是第一步是while loop来推进end; 直到推不动end, 然后start++
巧妙点: 因为end是外围variable, 在start的loop上, end不会重置;[star ~ end] 中间不需要重复计算.
最终可以O(n);

Previous verison of two pointers:
用两个pointer, head和i.
注意：head很可能被退回到很早的地方，比如abbbbbba,当遇到第二个a，head竟然变成了 head = 0+1 = 1.      
当然这是不对的，所以head要确保一直增长，不回溯

方法2:
   HashMap<Char, Integer>: <character, last occurance index>
   一旦有重复, rest map.
   没有重复时候, 不断map.put(), 然后求max值

问题: 每次reset map之后就开始从新从一个最早的index计算, 最坏情况是O(n^2):
'abcdef....xyza'




---

**12. [Minimum Window Substring.java](https://github.com/awangdev/LintCode/blob/master/Java/Minimum%20Window%20Substring.java)**      Level: Hard
      

基本思想: 用个char[]存string的frequency. 然后2pointer, end走到底, 不断validate.
符合的就process as result candidate.

HashMap的做法比char[]写起来要复杂一点, 但是更generic



---

**13. [Longest Substring with At Most K Distinct Characters.java](https://github.com/awangdev/LintCode/blob/master/Java/Longest%20Substring%20with%20At%20Most%20K%20Distinct%20Characters.java)**      Level: Medium
      

大清洗 O(nk)   
map.size一旦>k，要把longest string最开头（marked by pointer:start）的那个char抹掉    
一旦某一个char要被清除，所以在这个char 的1st and last appearance之间的char都要被清洗from map




---

**14. [Palindrome Pairs.java](https://github.com/awangdev/LintCode/blob/master/Java/Palindrome%20Pairs.java)**      Level: Hard
      

Obvious的做法是全部试一遍, 判断, 变成 O(n^2) * O(m) = O(mn^2). O(m): isPalindrome() time.

当然不行了, 那就看是O(nlogN), 还是O(n)?

#### 方法1: Hash Table + Palindrome的性质. 复合型.
O(mn)

##### 思路
- 每一个word, 都可以拆分成 front + mid + end. 如果这个word + 其他word可以组成palindrome,那就是说
- 砍掉 (mid+end), front.reverse() 应该存在 words[] 里面.
- 砍掉 (front+mid), end.reverse() 应该存在 words[] 里面.
- 我们用HashMap存所有的<word, index>, 然后reverse, 找配对就好.

##### Corner case
- 如果有 empty string "", 那么它跟任何一个palindrome word, 都可以配对, 并且根据位置前后变换, 凑成2份 distinct indexes.
- 这样就有了那个 `if (reverseEnd.equals("")) {...}` 的logic.
- 注意: 虽然在处理砍头/砍尾的两个 for loop里面都在根据 empty string 重复记录, 
  但因为 "" 自己本身不能作为起点, 所以overall只会在被其他palindrome配对时记录一次.


#### 方法2: Trie
还要做一下那.



---

**15. [Change to Anagram.java](https://github.com/awangdev/LintCode/blob/master/Java/Change%20to%20Anagram.java)**      Level: Easy
      

HackerRank里面的random 题目: 给一个string, 一切成两半, 看两半要变化多少个字符, 能变成anagram.

- 切两半成两个String A,B. 分别在int count[26]里面++, --.
- 记录 26个小写字母的频率. 如果全部抵消, 就是anagram.
- 注意: 最后count出来要除以2：字母不同，会在不同的字母位上加减count,那么就是刚好重复计算了一遍。所以除以二

- Note: HackerRank里要注意自己写: Scanner, import java.util, non-static method ...etc.



---

**16. [Compare Version Numbers.java](https://github.com/awangdev/LintCode/blob/master/Java/Compare%20Version%20Numbers.java)**      Level: Medium
      

给两串version number,  由数字和'.' 组成. 比较先后顺序. 

If version1 > version2 return 1, if version1 < version2 return -1, otherwise return 0.

#### divide and conquer 
- 用 str.split("\\.") 分割string
- Convert成integer, 逐个击破

#### 注意
- '1.0' 和 '0' 是相等的
- 如果可以假设version integer都是valid, 直接Integer.parseInt()就可以了
- 不然的话, 可以compare string



---

**17. [Compare Strings.java](https://github.com/awangdev/LintCode/blob/master/Java/Compare%20Strings.java)**      Level: Easy
      

看StringA是不是包括所有 StringB的字符.

#### Basic Implementation
- 比较一下大小, null.
- 然后用int[]来count chars from A, count[x]++. 再对照chars in B, count[x]--
- 如果 count[c] < 0, 就 false.
- O(n)



---

**18. [Count and Say.java](https://github.com/awangdev/LintCode/blob/master/Java/Count%20and%20Say.java)**      Level: Easy
      

介绍一种count数字的方法, 然后每一行读出上一行的结果, 一行一行推算. 问nth行是啥样?

#### Basic Implementation
- 主要是题意很难理解, 非常misleading, 等到看明白题目, 其实没有什么算法要求.
- Count duplicates and print



---

**19. [One Edit Distance.java](https://github.com/awangdev/LintCode/blob/master/Java/One%20Edit%20Distance.java)**      Level: Medium
      

如果S, T只用一个operation就能变成相等, return true.

#### Edit: 删除，增加，和替换
- 换完之后，理论上换成的String 就应该全等
- for loop, 一旦找到不一样的char, 就判断那三种可能性
- insert/delete 对于2个string来说, 效果是类似的
- O(n)



---

**20. [Decode Ways.java](https://github.com/awangdev/LintCode/blob/master/Java/Decode%20Ways.java)**      Level: Medium
      

给出一串数字, 要翻译(decode)成英文字母. [1 ~ 26] 对应相对的英文字母. 求有多少种方法可以decode.

#### Partition DP
- 确定末尾的2种状态: single letter or combos. 然后计算出单个letter的情况, 和双数的情况
- 定义dp[i] = 前i个digits最多有多少种decode的方法. new dp[n + 1].
- 加法原理: 把不同的情况, single-digit, double-digit 的情况加起来
- note: calculate number from characters, need to - '0' to get the correct integer mapping.
- 注意: check value != '0', 因为'0' 不在条件之中(A-Z)




---

**21. [Group Anagrams.java](https://github.com/awangdev/LintCode/blob/master/Java/Group%20Anagrams.java)**      Level: Medium
      

给一串string, return list of list, 把anagram 放在一起.

#### Hash Table, key 是 character frequency
- 存anagram
- 用 character frequency 来做unique key
- 用固定长度的char[26] arr 存每个字母的frequency; 然后再 new string(arr).   
- 因为每个位子上的frequency的变化，就能构建一个unique的string
- O(nk), k = max word length


#### Hash Table, key 是 sorted string
- 和check anagram 想法一样：转化并sort char array，用来作为key。
- 把所有anagram 存在一起。注意结尾Collections.sort().
- O(NKlog(K)), N = string[] length, k = longest word length    




---

**22. [Flip Game.java](https://github.com/awangdev/LintCode/blob/master/Java/Flip%20Game.java)**      Level: Easy
      

#### String
- 可以用 sb.replace(i, j, "replacement string")
- 简单按 window=2 来扫描
- 原来只需要从'++'转到'--'的情况
- O(n)



---

**23. [Implement strStr().java](https://github.com/awangdev/LintCode/blob/master/Java/Implement%20strStr().java)**      Level: Easy
      

给两个string A, B, 找一个 B 在 A 种的起始位置.

#### Two Pointer
- 找到B在A中的起始位置, 然后看一下从这个点开始的substring是否等于B就可以了
- 还挺多坑的, 这些可以帮助优化:
- 1. 当B是“”的时候，也就是能在A的其实位置找到B....index = 0.
- 2. edge condition: 如果 haystack.length() < needle.length() 的话, 必须错, return -1
- 3. 如果在某个index, A后面剩下的长度, 比B的长度短, 也是误解, return -1



---

**24. [Integer to English Words.java](https://github.com/awangdev/LintCode/blob/master/Java/Integer%20to%20English%20Words.java)**      Level: Hard
      

给一个小于 Integer.MAX_VALUE (2^31 - 1) 的数字, 转换成英语. (不需要加 'and')

#### String
- 基本implementation
- 分类讨论: thounsand, million, billion.  3个数字一格.
- 用array枚举 token
- 运用 % 和 / 来找到每个分段的英语翻译
- 3-digit 的部分, 可以用一个helper funtion来找到结果, 每段的处理方法都是一样的

#### 注意
- StringBuffer 更有效率
- 注意加 " " 的时候, 如果多余, 要trim()
- 注意, 小于20的数字, 有自己的特殊写法, 需要额外handle
- 这道题目就是要细致耐心, 算法并不难, 就是想要写的efficient并且正确, 需要很小心




---

**25. [Length of Last Word.java](https://github.com/awangdev/LintCode/blob/master/Java/Length%20of%20Last%20Word.java)**      Level: Easy
      

给一个String, 里面有lower case character 和 ' '. 找最后一个单个word的长度

#### basics
- 从末尾找' ', 找到了计算长度
- 记得要s.trim(), 把首尾的space去掉



---

**26. [Longest Common Substring.java](https://github.com/awangdev/LintCode/blob/master/Java/Longest%20Common%20Substring.java)**      Level: Medium
      

#### Double Sequence DP
- 两个string, 找最值: longest common string length
- 序列型, 并且是双序列, 找两个序列 (两维的某种性质)
- dp[i][j]: 对于 A 的前i个字母, 对于 B 的前j个字母, 找最长公共substring的长度
- dp = new int[m + 1][n + 1]
- dp[i][j] = dp[i - 1][j - 1] + 1; only if A.charAt(i - 1) == B.charAt(j - 1)
- 注意track max, 最后return
- space O(n^2), time(n^2)

##### Rolling array
- 空间优化, [i] 只有和 [i - 1] 相关, 空间优化成 O(n)

#### String
- 找所有A的substring, 然后B.contains()
- track max substring length
- O(n^2) time



---

**27. [Longest Words.java](https://github.com/awangdev/LintCode/blob/master/Java/Longest%20Words.java)**      Level: Easy
      

给一串String, 找到最长的长度, 把最长的String全都return

#### HashMap
- <Integer,List<String>>
- 存最长值, 最后map.get(max) 



---

**28. [Valid Palindrome.java](https://github.com/awangdev/LintCode/blob/master/Java/Valid%20Palindrome.java)**      Level: Easy
      

验证string是不是 palindrome. 只考虑 alphanumeric, 其他字符可以忽略

#### Check Palindrome
- 前后两个指针, 往中间移动, 查看是否字母重合

#### 过滤 alphanumeric
- 可以用 ASCII code 来手动过滤, 只要 '0' ~ '9', 'a' ~ 'z', 'A' - 'Z' 之间的
- 也可以用 regular expression: match 所有这些字母, 是 [a-zA-Z0-9]
- 那凡是不是这些字母的 match, 就是取反: "[^a-zA-Z0-9]". 测试: https://regex101.com/



---

**29. [Rotate String.java](https://github.com/awangdev/LintCode/blob/master/Java/Rotate%20String.java)**      Level: Easy
      

给两个String, 看A rotate之后 能不能变成B

#### LeetCode
- Basics
- StringBuffer.deleteCharAt(xx), StringBuffer.append(xx)
- O(n)


#### LintCode
- Different problem: 给一个char[], 要rotate offset times.
- *三步rotate*
- 有个坑：offset可能很长，那么要%length，才能得到真正需要rotate的部分。
- Note: rotate 一个 full length之后，是string 不变



---




 
 
 
## Math (20)
**0. [Power of Three.java](https://github.com/awangdev/LintCode/blob/master/Java/Power%20of%20Three.java)**      Level: Easy
      

方法1:
Power of 3:  3 ^ x == n ?
意思是 n / 3 一直除, 最后是可以等于1的, 那么就有了 n/=3, check n%3, 最后看结果是不是整除到1的做法. 用while loop.

方法2:
如果n是power of 3, 那么 3 ^ x的这个 x一定是个比n小的数字. 那么可以在 0 ~ n 之间做binary serach, 但是就比较慢.

方法3:
巧妙的想法.最大的3^x integer是 3^19. 那么找到这个数, 一定可以被n整除. 一步到位.



---

**1. [Plus One.java](https://github.com/awangdev/LintCode/blob/master/Java/Plus%20One.java)**      Level: Easy
      

简单的实现, 加1, 进位. 唯一取巧的地方, 最后如果要多一位, 一定是10000...这个模式, 可以走捷径, 直接来个+1size的array, 然后第一位=1.
注意,转换成long也不合理,用太多memory.


---

**2. [Power of Two.java](https://github.com/awangdev/LintCode/blob/master/Java/Power%20of%20Two.java)**      Level: Easy
      

跟powerOfThree一样: 可以loop, check mod; 也可以用binary search找合适的数字.



---

**3. [Encode and Decode TinyURL.java](https://github.com/awangdev/LintCode/blob/master/Java/Encode%20and%20Decode%20TinyURL.java)**      Level: Medium
      

其实想到了切入点, 是个可难可简单的题目. 这里的encode就是想办法把url存起来, 然后给个 key.
那么具体怎么做这个key, 简单就可以用一个map, 然后counting. 复杂一点就可以做random letter/number组成key.



---

**4. [Perfect Squares.java](https://github.com/awangdev/LintCode/blob/master/Java/Perfect%20Squares.java)**      Level: Medium
      

给一个数字n, 找到这个数字 最少能用多少个 平方数组成. 

平方数比如: 1, 4, 9, 16 ... etc

#### Partition DP
- 遇到最值, 想到DP.
- 看到分割字眼, 想到分割型 DP. 
- 思考, 如果 j * j = 9, 那么 j = 3 就是最少的一步; 但是如果是10呢? 就会分割成1 + 9 = 1 + j * j 
- 考虑最后的数字: 要是12割个1出来, 剩下11怎么考虑? 割个4出来,剩下8怎么考虑?
- partion的方式: 在考虑dp[i - x]的时候,  x 不是1, 而是 x = j*j.
- 就变成了dp = Min{dp[i - j^2] + 1}

#### 时间复杂度
- 乍一看是O(n*sqrt(n)). 实际也是. 但如何推导?
- 考虑上限: 把小的数字变成大的 推导上限; 考虑下限: 把数字整合归小, 找到下限.
- 考虑sqrt(1) + sqrt(2) + ....sqrt(n):找这个的upper bound and lower bound.
- 最后发现它的两边是 A*n*sqrt(n) <= actual time complexity <= B*n*sqrt(n)
- 那么就是O(n*sqrt(n))啦

#### Previous Notes
- 一开始没clue.看了一下提示
- １.　第一步想到了，从数学角度，可能是从最大的perfect square number开始算起。
- ２.　然后想法到了dp， 假设最后一步用了最大的maxSqrNum, 那么就在剩下的 dp[i - maxSqrNum^2] +１　不就好了？
- ３.　做了，发现有个问题．．．最后一步选不选maxSqrNum?  比如12就是个例子。
- 然后就根据提示，想到BFS。顺的。 把1～maxSqrNum 都试一试。找个最小的。
- 看我把12拆分的那个example. 那很形象的就是BFS了。
- 面试时候，如果拆分到这个阶段不确定，那跟面试官陶瓷一下，说不定也就提示BFS了。



---

**5. [Valid Perfect Square.java](https://github.com/awangdev/LintCode/blob/master/Java/Valid%20Perfect%20Square.java)**      Level: Review
      

Binary找sqrt. 基本 mid+1, mid-1 template.
注意: define index as long. 



---

**6. [Pow(x,n).java](https://github.com/awangdev/LintCode/blob/master/Java/Pow(x,n).java)**      Level: Medium
      

傻做就O(n), 要更好就考虑O(logN).
减少重复计算, 一切两半.

注意:
- n/2的奇数偶数
- n的正负
- n == 0的情况, x == 0, x == 1 的情况.


---

**7. [Add Binary.java](https://github.com/awangdev/LintCode/blob/master/Java/Add%20Binary.java)**      Level: Easy
      

方法一:土办法没技术，把binary换成数字，加起来，再换成binary。如果input很大，那么很可能int,long都hold不住。不保险。

方法二:一般方法，string化为charArray,然后逐位加起，最后记得处理多余的一个carry on
注意: 需要从末尾加起来, 所以要用一个diff来帮助  shortArray[i-diff] 指向 shortArray的相对应index.



---

**8. [Add Digits.java](https://github.com/awangdev/LintCode/blob/master/Java/Add%20Digits.java)**      Level: Easy
      

方法1: 普通做法就是按照题意, double-while loop把数字加起来. 第一层循环是O(n), 然后第二层循环就少很多数位, overall O(n)

方法2: 找数学规律, 每过9个数字, 取mod就会开始重复, 所以给所有数字取mod 就可以间接找到答案. O(1)



---

**9. [Add Two Numbers.java](https://github.com/awangdev/LintCode/blob/master/Java/Add%20Two%20Numbers.java)**      Level: Medium
      

LinkedList都已经反转好了，直接做.
遍历两个l1,l2把carry-on处理好，每次生成一个新node，最后检查carry-on.

跟Add Binary的理解方式一模一样.

注意:
Linked List 没有天然size.
用DummyNode(-1).next来hold住结果.




---

**10. [Reverse Integer.java](https://github.com/awangdev/LintCode/blob/master/Java/Reverse%20Integer.java)**      Level: Easy
      

#### 方法1
每次加上x%10，然后x不断减小～0
注意处理MAX_VALUE, MIN_VALUE
符号不重要, 直接处理, 也会保留.

#### 方法2
转换成String 然后 reverse
Space O(n), time O(n)



---

**11. [Sqrt(x).java](https://github.com/awangdev/LintCode/blob/master/Java/Sqrt(x).java)**      Level: Easy
      

#### s- qrt(int x)
- 理解题意, 从[0, x]找一个可以m*m=x的值.
- 注意, 如果找不到, 最后问考官该return一个什么值：按道理，因为return int, 会取整，那么return一个平方最close to x就可以.
- 注意 mid 用 long, 因为很可能超过最大int.

#### sqrt(double x)
- 二分float number, 应该用精度来定义结尾.
- 还是二分, 但是判断条件变成: while ( end - start > eps)
- eps = 1e-12,也就是精度到1e-12



---

**12. [Continuous Subarray Sum.java](https://github.com/awangdev/LintCode/blob/master/Java/Continuous%20Subarray%20Sum.java)**      Level: Medium
      

给一个非负数的数列和数字k(可正负, 可为0). 找到连续子序列(长度超过2), 使得这个subarray的sum 是 k的倍数. 问: 是否可能?

#### DP
- O(n^2)
- 需要记录在0 ~ i点(包括nums[i], 以nums[i]结尾)的sum, 坐标型动态规划.
- dp[i] = dp[i - 1] + nums[i];
- 最后移动, 作比较

#### 直接算结果
- 从sum = 每次[i ~ j]的所有情况
- 验证



---

**13. [Count Primes.java](https://github.com/awangdev/LintCode/blob/master/Java/Count%20Primes.java)**      Level: Easy
      

计数: 所有小于n的prime number.

#### prime number定义
- >=2的没有除自己和1以外公约数的数。   
- 还有另外一个定义方法: 这个n,有没有小于n的一个i, 而达到： i * i + # of i = n. 如果有，那就不是 prime   

#### Steps
- 一个boolean长条，存isPrime[]。 然后从i=2， 全部变true.
- hash key: the number itself
- 然后利用这个因子的性质，非prime满足条件： self*self, self * self + self ... etc.     
- 所以就check每一个j, j+i, j+i+i, 然后把所有non-prime全部mark成false.     
- 最后，数一遍还剩下的true个数就好了   



---

**14. [Excel Sheet Column Number.java](https://github.com/awangdev/LintCode/blob/master/Java/Excel%20Sheet%20Column%20Number.java)**      Level: Easy
      

#### Math
- 26位的运算, 根据10位运算去思考
- 'A' - 'A' = 0. 所以 char - 'A' + 1 = 题目里的对应数位
- 或者: 26位运算和10位一样:num += 每位的digit * Math.pow(26, 数位号)




---

**15. [Excel Sheet Column Title.java](https://github.com/awangdev/LintCode/blob/master/Java/Excel%20Sheet%20Column%20Title.java)**      Level: Easy
      

#### 基本换算
- 26位
- 从末尾开始, mod %26 可以拿到 末尾数字 remain = n % 26
- 特殊: remain = 0 的时候, 也就是说n是26的倍数, 末尾应该是 'Z'
- 记录'Z'了之后, n--




---

**16. [Integer to English Words.java](https://github.com/awangdev/LintCode/blob/master/Java/Integer%20to%20English%20Words.java)**      Level: Hard
      

给一个小于 Integer.MAX_VALUE (2^31 - 1) 的数字, 转换成英语. (不需要加 'and')

#### String
- 基本implementation
- 分类讨论: thounsand, million, billion.  3个数字一格.
- 用array枚举 token
- 运用 % 和 / 来找到每个分段的英语翻译
- 3-digit 的部分, 可以用一个helper funtion来找到结果, 每段的处理方法都是一样的

#### 注意
- StringBuffer 更有效率
- 注意加 " " 的时候, 如果多余, 要trim()
- 注意, 小于20的数字, 有自己的特殊写法, 需要额外handle
- 这道题目就是要细致耐心, 算法并不难, 就是想要写的efficient并且正确, 需要很小心




---

**17. [Fibonacci.java](https://github.com/awangdev/LintCode/blob/master/Java/Fibonacci.java)**      Level: Easy
      

#### Memoization
- fib[n] = fibonacci(n - 1) + fibonacci(n - 2);

#### DP array.
- 滚动数组, 简化DP

#### recursively calculate
- recursively calculate fib(n - 1) + fib(n - 2). 公式没问题, 但是时间太长, timeout.




---

**18. [Missing Number.java](https://github.com/awangdev/LintCode/blob/master/Java/Missing%20Number.java)**      Level: Easy
      

给一串unique数字, 数字取自 [0 ~ n], 无序, 找第一个skipped的数字.

#### Swap 
- 跟First Missing Positive 非常像, 只有一行代码的区别.
- swap 所有的数字, 到自己的correct position
- 最后一个for loop找到错位的index, 也就是缺的数字.

#### Bit Manipulation
- XOR will only retain bits that are different 1 ^ 0 = 1, but 0^0, 1^1 == 0
- Use that feature, 把所有value都和index XOR了
- 剩下的多余的数字, 其实是那个index无法被XOR消掉, 也就是那个缺的number value.
- 注意: 题目告诉数字是 [0 ~ n], 然而缺一个数字, 那么在[0 ~ n - 1] 里面, 最大的数字(不管缺没缺), 一定是 n = nums.length.

#### HastSet
- 全存, 找missing
- O(n) space, 不合题意

#### sorting
- sort, 找1st missing
- O(n log n) 太慢, 不合题意



---

**19. [Basic Calculator.java](https://github.com/awangdev/LintCode/blob/master/Java/Basic%20Calculator.java)**      Level: Hard
      

给一个expression String, 要evaluate这个expression的值.

Expression string 里面包括 +, -, 整数, 开合括号, 还有space.

#### Expression Tree
- Expression Tree是一个 weight-based的 min-tree 
- 基于 运算符号 + 数字的 tree: 数字永远在leaf, 然后符号是tree node,  括号不出现在tree里面
- 用 monotonuous stack 来构建这个tree

##### Thinking points
- Understand Expression Tree
- Use stack to build the expression tree + understand the weight system
- Use post-order traversal to evaluate the tree
- 注意, input里面的数字不会是single digit, 所以需要一个buffer存number string
- 整个题目的做法, 可以参照 `Expression Evaluation`



---




 
 
 
## DP (63)
**0. [Coin Change.java](https://github.com/awangdev/LintCode/blob/master/Java/Coin%20Change.java)**      Level: Medium
      

给一串不同数额的coins, 和total amount to spent. 求 最少 用多少个coin可以组合到这个amount. 每种coins个数不限量.

#### DP
- 找对方程dp[x], 积累到amount x最少用多少个coin: #coin是value, index是 [0~x].
- 子问题的关系是: 如果用了一个coin, 那么就应该是f[x - coinValue]那个位置的#coins + 1

##### initialization
- 处理边界, 一开始0index的时候, 用value0. 
- 中间利用Integer.MAX_VALUE来作比较, initialize dp[x]
- 注意, 一旦 Integer.MAX_VALUE + 1 就会变成负数. 这种情况会在coin=0的时候发生.

##### Optimization
- 方法1: 直接用Integer.MAX_VALUE
- 方法2: 用-1, 稍微简洁一点, 每次比较dp[i]和 dp[i - coin] + 1, 然后save. 不必要做多次min比较.

#### Memoization
- dp[i] 依然表示: min # of coints to make amount i
- initialize dp[i] = Integer.MAX_VALUE
- 先选最后一步(遍历coins),  然后dfs做同样的操作
- 记录dp[amount] 如果已经给过value, 不要重复计算, 直接return.
- 但是这道题没必要强行做memoization, 普通DP的状态和方程相对来说很好找到



---

**1. [Maximum Product Subarray.java](https://github.com/awangdev/LintCode/blob/master/Java/Maximum%20Product%20Subarray.java)**      Level: Medium
      

从一组数列(正负都有)里面找一串连续的子序列, 而达到乘积product最大值.

#### DP
- 求最值, 想到DP. Time/Space O (n)
- 两个特别处: 
- 1. 正负数情况, 需要用两个DP array. 
- 2. continuous prodct 这个条件决定了在Math.min, Math.max的时候, 
- 是跟nums[x]当下值比较的, 如果当下值更适合, 会舍去之前的continous product, 然后重新开始.
- 这也就注定了需要一个global variable 来hold result.

#### Space optimization, rolling array
- maxProduct && minProduct 里面的 index i, 都只能 i - 1相关, 所以可以省去redundant operatoins
- Time: O(n), space: O(1)



---

**2. [k Sum.java](https://github.com/awangdev/LintCode/blob/master/Java/k%20Sum.java)**      Level: Hard
      

DP. 公式如何想到, 还需要重新理解.

dp[i][j][m]: # of possibilities such that from j elements, pick m elements and sum up to i. 
i: [0~target]

dp[i][j][m] = dp[i][j-1][m] + dp[i - A[j - 1]][j-1][m-1]
            (i not included)   (i included)



---

**3. [Longest Increasing Subsequence.java](https://github.com/awangdev/LintCode/blob/master/Java/Longest%20Increasing%20Subsequence.java)**      Level: Medium
      

无序数组, 找最长的上升(不需要连续)数组 的长度. 先做O(n^2), 然后可否O(nLogN)?

#### DP, double for loop, O(n^2)
- 考虑nums[i]结尾的时候, 在[0, i) 里count有多少小于nums[i]
- 对于所有 i in [0, n), 最常的increasing序列有多少length?
- max需要在全局维护: nums是无序的, nums[i]也可能是一个很小的值, 所以末尾dp[i]并不是全局的max, 而只是对于nums[i]的max.
- 正因此, 每个nums[i]都要和每个nums[j] 作比较, j < i.
- dp[i] = Maht.max(dp[i], dp[j] + 1); j = [0 , i - 1]
- 时间复杂度  O(n^2)


#### O(nLogN)
- 维持一个list of increasing sequence
- 这个list其实是一个base-line, 记录着最低的increasing sequence.
- 当我们go through all nums的时候, 如果刚好都是上升, 直接append
- 如果不上升, 应该去list里面, 找到最小的那个刚好大于new num的数字, 把它换成num
- 这样就完成了baseline. 举个例子, 比如替换的刚好是在list最后一个element, 等于就是把peak下降了, 那么后面其他的数字就可能继续上升.
- '维护baseline就是一个递增的数列' 的证明, 还没有仔细想.



---

**4. [Unique Binary Search Tree.java](https://github.com/awangdev/LintCode/blob/master/Java/Unique%20Binary%20Search%20Tree.java)**      Level: Medium
      

Not quite clear.
根据左右分割而总结出了原理, 每次分割, 左右两边都会有一定数量的permutation, 总体上的情况数量当然是相乘.
然后每一个不同的分割点都加一遍:
f(n) = f(0)*f(n-1) + f(1)*f(n-2) + ... + f(n-2)*f(1) + f(n-1)*f(0)

然后把数学公式转换成DP的方程, 有点玄学的意思啊! 不好想.



---

**5. [Unique Paths II.java](https://github.com/awangdev/LintCode/blob/master/Java/Unique%20Paths%20II.java)**      Level: Medium
      

跟unique path的grid一样, 目标走到右下角, 但是grid里面可能有obstacle, 不能跨越. 求unique path 的count.

#### 坐标DP
- dp[i][j]: # of paths to reach grid[i][j]
- dp[i][j] = dp[i - 1][j] + dp[i][j - 1];
- 考虑最终结尾需要的状态:如何组成,写出公式.
- 公式中注意处理能跳掉的block, marked as 1. '到不了', 即为 0 path in dp[i][j].



---

**6. [Bomb Enemy.java](https://github.com/awangdev/LintCode/blob/master/Java/Bomb%20Enemy.java)**      Level: Medium
      

2D grid, 每个格子里面可能是 'W' wall, 'E' enemy, 或者是 '0' empty.

一个bomb可以往4个方向炸. 求在grid上面, 最大能炸掉多少个敌人.

#### Corrdinate DP
- Space, Time: O(MN)
- dp[i][j] 就是(i, j)上最多能炸掉的enemy数量
- dp[i][j] 需要从4个方向加起来, 也就是4个方向都要走一遍, 所以分割成 UP/Down/Left/Right 4个 int[][]
- 最后一步的时候求max
- 分方向考虑的方法很容易想到,但是四个方向移动的代码比较繁琐.
- 往上炸: 要从顶向下考虑
- 往下炸: 要从下向上考虑
- 熟练写2D array index 的变换.

似乎还有一个更简洁的方法, 用col count array: http://www.cnblogs.com/grandyang/p/5599289.html



---

**7. [Perfect Squares.java](https://github.com/awangdev/LintCode/blob/master/Java/Perfect%20Squares.java)**      Level: Medium
      

给一个数字n, 找到这个数字 最少能用多少个 平方数组成. 

平方数比如: 1, 4, 9, 16 ... etc

#### Partition DP
- 遇到最值, 想到DP.
- 看到分割字眼, 想到分割型 DP. 
- 思考, 如果 j * j = 9, 那么 j = 3 就是最少的一步; 但是如果是10呢? 就会分割成1 + 9 = 1 + j * j 
- 考虑最后的数字: 要是12割个1出来, 剩下11怎么考虑? 割个4出来,剩下8怎么考虑?
- partion的方式: 在考虑dp[i - x]的时候,  x 不是1, 而是 x = j*j.
- 就变成了dp = Min{dp[i - j^2] + 1}

#### 时间复杂度
- 乍一看是O(n*sqrt(n)). 实际也是. 但如何推导?
- 考虑上限: 把小的数字变成大的 推导上限; 考虑下限: 把数字整合归小, 找到下限.
- 考虑sqrt(1) + sqrt(2) + ....sqrt(n):找这个的upper bound and lower bound.
- 最后发现它的两边是 A*n*sqrt(n) <= actual time complexity <= B*n*sqrt(n)
- 那么就是O(n*sqrt(n))啦

#### Previous Notes
- 一开始没clue.看了一下提示
- １.　第一步想到了，从数学角度，可能是从最大的perfect square number开始算起。
- ２.　然后想法到了dp， 假设最后一步用了最大的maxSqrNum, 那么就在剩下的 dp[i - maxSqrNum^2] +１　不就好了？
- ３.　做了，发现有个问题．．．最后一步选不选maxSqrNum?  比如12就是个例子。
- 然后就根据提示，想到BFS。顺的。 把1～maxSqrNum 都试一试。找个最小的。
- 看我把12拆分的那个example. 那很形象的就是BFS了。
- 面试时候，如果拆分到这个阶段不确定，那跟面试官陶瓷一下，说不定也就提示BFS了。



---

**8. [Backpack VI.java](https://github.com/awangdev/LintCode/blob/master/Java/Backpack%20VI.java)**      Level: Medium
      

给一个数组nums, 全正数, 无重复数字; 找: # of 拼出m的方法.

nums 里的数字, 可以重复使用. 不同的order可以算作不同的拼法.

#### Backpack DP
- dp[i] 表示: # of ways to fill weight i
- 1维: dp[w]: fill weigth w 有多少种方法. 前面有多少种可能性, 就sum多少个:
- dp[w] = sum{dp[w - nums[i]]}, i = 0~n

##### 分析
- 拼背包时, 可以有重复item, 所以考虑'最后被放入的哪个unique item' 就没有意义了.
- 背包问题, 永远和weight分不开关系.
- 这里很像coin chagne: 考虑最后被放入的东西的value/weigth, 而不考虑是哪个.






---

**9. [Copy Books.java](https://github.com/awangdev/LintCode/blob/master/Java/Copy%20Books.java)**      Level: Hard
      

给一串书pages[i], k个人, pages[i] 代表每本书的页数. k个人从不同的点同时开始抄书. 

问, 最快什么时候可以抄完?

#### Partition DP
- 第一步, 理解题目要求的问题: 前k个人copy完n本书, 找到最少的用时; 也可以翻译成, n本书, 让k个人来copy, 也就是分割成k段.
- 最后需要求出 dp[n][k]. 开: int[n+1][k+1]. 
- 在[0 ~ n - 1]本书里, 最后一个人可以选择copy 1 本, 2 本....n本, 每一种切割的方法的结果都不一样
- 木桶原理, 因为K个人同时开始, 最坏的情况决定结果
- dp[n][k] = Math.min(Math.max(dp[j][k - 1], sum[j+1, n-1]), loop over i, k, j)
- Time: O(kn^2), space O(nk)

##### Init
- Init: dp[0][0] = 0, 0个人0本书
- Integer.MAX_VALUE的运用:
- 当 i = 1, k = 1, 表达式: dp[i][k] = Math.min(dp[i][k], Math.max(dp[j][k - 1], sum));
- 唯一可行的情况就只有一种: i=0, k=0, 刚好 0 个人 copy 0 本书, dp[0][0] = 0.
- 其他情况, i = 1, k = 0, 0 个人读 1本书, 不可能发生: 所以用Integer.MAX_VALUE来冲破 Math.max, 维持荒谬值.
- 当 i=0, k=0 的情况被讨论时候, 上面的方程式才会按照实际情况计算出 dp[i][k]
- 这道题的init是非常重要而tricky的

##### 计算顺序
- k个人, 需要一个for loop; 
- k个人, 从copy1本书开始, 2, 3, ... n-1,所以 i=[1, n], 需要第二个for loop
- 在每一个i上, 切割的方式可以有[0 ~ i] 中, 我们要计算每一种的worst time

##### 滚动数组
- [k] 只有和 [k - 1] 相关
- Space: O(n)

#### Binary Search
- 根据: 每个人花的多少时间(time)来做binary search: 每个人花多久时间, 可以在K个人之内, 用最少的时间完成?
- time variable的范围不是index, 也不是page大小. 而是[minPage, pageSum]
- validation 的时候注意3种情况: 人够用 k>=0, 人不够所以结尾减成k<0, 还有一种是time(每个人最多花的时间)小于当下的页面, return -1
- O(nLogM). n = pages.length; m = sum of pages.




---

**10. [Longest Palindromic Subsequence.java](https://github.com/awangdev/LintCode/blob/master/Java/Longest%20Palindromic%20Subsequence.java)**      Level: Medium
      

#### Interval DP
- 用[i][j]表示区间的首尾
- 考虑3个情况: 砍头, 砍尾, 砍头并砍尾 (考虑首尾关系)
- Iteration一定是以i ~ j 之间的len来看的. 
- len = j - i + 1; 那么反推, 如果len已知, j = len + i -1;
- 注意考虑len == 1, len == 2是的特殊情况.

#### Memoization
- 同样的方式model dp[i][j]: range [i, j] 之间的  max palindromic length
- 三种情况: 
- 1. 首尾match 继而 dfs[i+1, j-1]
- 2. 首尾不match,dfs[i+1,j] 
- 3. 首尾不match,dfs[i,j-1] 
- 注意: init dp[i][j]=-1, dfs的时候查dp[i][j] 是否算过



---

**11. [Scramble String.java](https://github.com/awangdev/LintCode/blob/master/Java/Scramble%20String.java)**      Level: Hard
      

- 给两个string S, T. 检验他们是不是scramble string.
- scramble string 定义: string可以被分拆成binary tree的形式, 也就是切割成substring;
- 旋转了不是leaf的node之后, 形成新的substring, 这就是原来string的 scramble.


#### Interval DP 区间型
- 降维打击, 分割, 按照长度来dp.
- dp[i][j][k]: 数组S从index i 开始, T从index j 开始, 长度为k的子串, 是否为scramble string

##### Break down
- 一切两半以后, 看两种情况: , 或者不rotate这两半. 对于这些substring, 各自验证他们是否scramble.
- 不rotate分割的两半: S[part1] 对应  T[part1] && S[part2] 对应  T[part2]. 
- rotate分割的两半: S[part1] 对应  T[part2] && S[part2] 对应  T[part1]. 

##### Initialization
- len == 1的时候, 其实无法旋转, 也就是看S,T的相对应的index是否字符相等.
- initialization非常非常重要. 很神奇, 这个initailization 打好了DP的基础, 后面一蹴而就, 用数学表达式就算出了结果.
- input s1, s2 在整个题目的主要内容里面, 几乎没有用到, 只是用在initialization时候.
- More details, 看解答



---

**12. [Best Time to Buy and Sell Stock with Cooldown.java](https://github.com/awangdev/LintCode/blob/master/Java/Best%20Time%20to%20Buy%20and%20Sell%20Stock%20with%20Cooldown.java)**      Level: Medium
      

Sequence DP
跟StockIII很像. 分析好HaveStock && NoStock的状态, 然后看最后一步.



---

**13. [Longest Common Subsequence.java](https://github.com/awangdev/LintCode/blob/master/Java/Longest%20Common%20Subsequence.java)**      Level: Medium
      

给两个string, A, B. 找这两个string里面的LCS: 最长公共字符长度 (不需要是continuous substring)

#### Double Sequence DP
- 设定dp长度为(n+1), 因为dp[i]要用来表示前i个(ith)时候的状态, 所以长度需要时i+1才可以在i位置, hold住i.
- 双序列: 两个sequence之间的关系, 都是从末尾字符看起, 分析2种情况:
- 1. A最后字符不在common sequence 或者 B最后字符不在common sequence.
- 2. A/B最后字符都在common sequence. 总体count + 1.



---

**14. [Interleaving String.java](https://github.com/awangdev/LintCode/blob/master/Java/Interleaving%20String.java)**      Level: Hard
      

双序列DP, 从最后点考虑.
拆分问题的末尾, 考虑和s1, s2 subsequence之间的关联.

求存在性, boolean




---

**15. [Edit Distance.java](https://github.com/awangdev/LintCode/blob/master/Java/Edit%20Distance.java)**      Level: Hard
      

两个字符串, A要变成B, 可以 insert/delete/replace, 找最小变化operation count

#### Double Sequence
- 考虑两个字符串变换的最后点: 需要insert/delete/replace? 分析每种情况, 然后列出表达式.
- 先calculate最坏的情况, 3种operation count + 1; 然后在比较match的情况.
- 注意, 在i或者j为0的时候, 变成另外一个数字的steps只能是全变.
- 第一步, 空间时间都是O(MN)
- 滚动数组优化, 空间O(N)

#### Search



---

**16. [Distinct Subsequences.java](https://github.com/awangdev/LintCode/blob/master/Java/Distinct%20Subsequences.java)**      Level: Hard
      

Double Sequence DP:
0. DP size (n+1): 找前nth的结果, 那么dp array就需要开n+1, 因为结尾要return dp[n][m]
1. 在for loop 里面initialize dp[0][j] dp[i][0]
2. Rolling array 优化成O(N): 如果dp[i][j]在for loop里面, 就很好替换 curr/prev



---

**17. [Regular Expression Matching.java](https://github.com/awangdev/LintCode/blob/master/Java/Regular%20Expression%20Matching.java)**      Level: Review
      



---

**18. [Wildcard Matching.java](https://github.com/awangdev/LintCode/blob/master/Java/Wildcard%20Matching.java)**      Level: Hard
      

Double sequence DP. 与regular expression 很像.

注意1: 分析字符 ?, * 所代表的真正意义, 然后写出表达式.
注意2: 搞清楚initialization 的时候 dp[i][0] 应该always false.当p为empty string, 无论如何都match不了 (除非s="" as well)
    同时 dp[0][j]不一定是false. 比如s="",p="*" 就是一个matching.



---

**19. [Ones and Zeroes.java](https://github.com/awangdev/LintCode/blob/master/Java/Ones%20and%20Zeroes.java)**      Level: Hard
      

还是Double Sequence, 但是考虑第三种状态: 给的string array的用量.
所以开了3维数组.

如果用滚动数组优化空间, 需要把要滚动的那个for loop放在最外面, 而不是最里面.
当然, 这个第三位define在 dp[][][]的哪个位置, 问题都不大.

另外, 注意在外面calcualte zeros and ones, 节约时间复杂度.



---

**20. [Word Break II.java](https://github.com/awangdev/LintCode/blob/master/Java/Word%20Break%20II.java)**      Level: Review
      

两个DP一起用.解决了timeout的问题     
1. isWord[i][j], subString(i,j)是否存在dict中？

2. 用isWord加快 isValid[i]: [i ～ end]是否可以从dict中找到合理的解？      
	从末尾开始查看i：因为我们需要测试isWord[i][j]时候，j>i, 而我们观察的是[i,j]这区间；       
	j>i的部分同样需要考虑，我们还需要知道isValid[0～j+1]。 所以isValid[x]这次是表示[x, end]是否valid的DP。     
	i 从 末尾到0, 可能是因为考虑到isWord[i][j]都是在[0~n]之内，所以倒过来数，坐标比较容易搞清楚。     
	(回头看Word Break I， 也有坐标反转的做法)

3. dfs 利用 isValid 和isWord做普通的DFS。

Note:
在Word Break里面用了set.contains(...), 在isValid里面，i 从0开始。 但是，contains()本身是O(n).     
在这道题里面应该是因为word dictionary太大，加上nest for, 变成O(n^3)所以timeout.

istead,用一个isWord[i][j]，就O(1)判断了i~j是不是存在dictionary里面。



---

**21. [Unique Path.java](https://github.com/awangdev/LintCode/blob/master/Java/Unique%20Path.java)**      Level: Medium
      

2D array, 算走到最右下角，有多少种方式.

##### DP
- 计数DP.注意方程式前两位置加在一起: 前两种情况没有overlap, 也不会缺情况.
- 注意initialization, 归1.
- 需要initialize的原因是,也是一个reminder: 在方程中会出现-1index
- Of course, row i = 0, or col j = 0, there is only 1 way to access
- time O(mn), space O(mn)

##### 滚动数组
- [i] 只跟 [i - 1] 有关系, 用 curr/prev 建立滚动数组.
- space O(n) 优化空间




---

**22. [Maximal Rectangle.java](https://github.com/awangdev/LintCode/blob/master/Java/Maximal%20Rectangle.java)**      Level: Hard
      

#### 方法1: monotonous stack
分解开来, 其实是'Largest Rectangle in Histogram', 只不过这里要自己model heights.
一个2D array里面的rectangle, 最终也是用height * width做出来的.
巧妙在于, 把每一行当做底边, 算出这个底边, 到顶部的height: 
- 如果底边上的一个value==0, 那么算作没有height(以这个底边做rectangle, value==0的位置是空中楼阁, 不能用)
- 如果底边上的value==1, 那么就把上面的height加下来, 做成histogram

如果看具体实例, 有些row似乎是白算的, 但是没有办法, 这是一个搜索的过程, 最终会比较出最优解.

#### 方法2: DP
Coordinate DP?



---

**23. [Maximal Square.java](https://github.com/awangdev/LintCode/blob/master/Java/Maximal%20Square.java)**      Level: Medium
      

只能往右边,下面走, 找面积最大的 square. 也就是找到变最长的 square.

#### DP
- 正方形, 需要每条边都是一样长度.
- 以右下角为考虑点, 必须满足条件: left/up/diagonal的点都是1
- 并且, 如果三个点分别都衍生向三个方向, 那么最长的 square 边就是他们之中的最短边 (受最短边限制)
- dp[i][j]: max square length when reached at (i, j), from the 3 possible directions
- dp[i][j] = Math.min(Math.min(dp[i - 1][j], dp[i][j - 1]), dp[i - 1][j - 1]) + 1;
- Space, time O(mn)

##### init
每个点都可能是边长1, 如果 matrix[i][j] == '1'

##### 滚动数组
[i] 和 [i - 1] 之间的关系, 想到滚动数组优化 space, O(n) sapce.



---

**24. [Longest Increasing Path in a Matrix.java](https://github.com/awangdev/LintCode/blob/master/Java/Longest%20Increasing%20Path%20in%20a%20Matrix.java)**      Level: Hard
      

m x n 的matrix, 找最长增序的序列长度. 这里默认连续的序列.

- 接成圈是不行的, 所以visit过得 (x,y)就不能再去了.
- 斜角方向不能走, 只能走上下左右
- 无法按照坐标DP来做, 因为计算顺序4个方向都可以走.
- 最终要visit所有node, 所以用DFS搜索比较合适.

#### DFS, Memoization
- DFS太多重复计算; memoization (dp[][], visited[][]) 省去了重复计算
- initialize dp[x][y] = 1, (x,y) 自己也算path里的一格
- dfs(matrix, x, y): 每次检查(x,y)的4个neighbor (nx, ny), 如果他们到(x,y)是递增, 那么就考虑和比较:
- Maht.max(dp[x][y], dp[nx][ny] + 1); where dp[n][ny] = dfs(matrix, nx, ny)
- top level: O(mn), 尝试从每一个 (x,y) 出发
- O(m * n * k), where k is the longest path

#### Topological sort
还没有做



---

**25. [Coins in a Line.java](https://github.com/awangdev/LintCode/blob/master/Java/Coins%20in%20a%20Line.java)**      Level: Medium
      

拿棋子游戏, 每个人可以拿1个或者2个, 拿走最后一个子儿的输. 问: 根据给的棋子输, 是否能确定先手的输赢?

Game Theory: 如果我要赢, 后手得到的局面一定要'有输的可能'.

#### DP, Game Theory
- 要赢, 必须保证对手拿到棋盘时, 在所有他可走的情况中, '有可能败', 那就足够.
- 设计dp[i]:表示我面对i个coins的局面时是否能赢, 取决于我拿掉1个,或者2个时, 对手是不是会可能输?
- dp[i] = !dp[i - 1] || !dp[i-2]
- 时间: O(n), 空间O(n)
- 博弈问题, 常从'我的第一步'角度分析, 因为此时局面最简单.

#### Rolling Array
空间优化O(1). Rolling array, %2



---

**26. [Coins in a Line II.java](https://github.com/awangdev/LintCode/blob/master/Java/Coins%20in%20a%20Line%20II.java)**      Level: Medium
      

给一串coins, 用values[]表示; 每个coin有自己的value. 先手/后手博弈,
每次只能 按照从左到右的顺序, 拿1个或者2个棋子, 最后看谁拿的总值最大.

MiniMax的思考方法很神奇, 最后写出来的表达式很简单

#### DP, Game Theory 自考过程比较长
- 跟Coins in a line I 不一样: 每个coin的value不同.
- 用到MiniMax的思想, 这里其实是MaxiMin. Reference: http://www.cnblogs.com/grandyang/p/5864323.html
- Goal: 使得player拿到的coins value 最大化.
- 设定dp[i]: 从index i 到 index n的最大值. 所以dp[0]就是我们先手在[0 ~ n]的最大取值 
- 于此同时, 你的对手playerB也想最大化, 而你的选择又不得不被对手的选择所牵制.
- 用MaxiMin的思想, 我们假设一个当下的状态, 假想对手playerB会做什么反应(从对手角度, 如何让我输)
- 在劣势中(对手让我输的目标下)找到最大的coins value sum


##### 推算表达式
- Reference里面详细介绍了表达式如何推到出来, 简而言之:
- 如果我选了i, 那么对手就只能选(i+1), (i+2) 两个位置, 而我在对方掌控时的局面就是min(dp[i+2], dp[i+3])
- 如果我选了i和(i+1), 那么对手就只能选(i+2), (i+3) 两个位置, 而我在对方掌控时的局面就是min(dp[i+3], dp[i+4])
- 大家都是可选1个或者2个coins
- 目标是maximize上面两个最坏情况中的最好结果

##### 简化表达式
- 更加简化一点: 如果我是先手, dp[i]代表我的最大值.
- 取决于我拿了[i], 还是[i] + [i+1], 对手可能是dp[i + 1], 或者是dp[i+2]
- 其实dp[i] = Math.max(sum - dp[i + 1], sum - dp[i + 2]);
- 这里的sum[i] = [i ~ n] 的sum, 减去dp[i+1], 剩下就是dp[i]的值没错了

##### Initialization
- 这个做法是从最后往前推的, 注意initialize dp末尾的值.
- dp = new int[n + 1]; dp[n] = 0; // [n ~ n]啥也不选的时候, 为0.
- sum = new int[n + 1]; sum[n] = 0; // 啥也不选的时候, 自然等于0
- 然后记得initialize (n-1), (n-2)

##### 时间/空间
Time O(n)
Space O(n): dp[], sum[]



---

**27. [Climbing Stairs.java](https://github.com/awangdev/LintCode/blob/master/Java/Climbing%20Stairs.java)**      Level: Easy
      

#### Recursive + Memoization
- 递归很好写, 但是重复计算, timeout. time: O(2^n)
- O(2^n): each n can spawn 2 dfs child, at next level, it will keep spawn. Total 2^n nodes will spawn.
- 用全局变量int[] memo 帮助减少重复计算
- O(n) time, space

#### DP
- 最后一步被前两种走法决定: dp[i] = dp[i - 1] + dp[i - 2]
- 基础sequence DP, int[] dp = int[n + 1];
- DP[]存的是以 1-based index的状态
- 需要知道dp[n] 的状态, 但是最大坐标是[n-1], 所以int[n+1]
- dp[0]往往是有特殊状态的
- O(n) space, time

#### 序列DP, 滚动数组
- [i] only associates with [i-2], [i-1].
- %2
- O(1) space



---

**28. [Coins in a Line III.java](https://github.com/awangdev/LintCode/blob/master/Java/Coins%20in%20a%20Line%20III.java)**      Level: Hard
      

还是2个人拿n个coin, coin可以有不同的value. 

只不过这次选手可以从任意的一头拿, 而不限制从一头拿. 算先手会不会赢?

#### Memoization + Search
- 跟Coins in a Line II 一样, MaxiMin的思想: 找到我的劣势中的最大值
- dp[i][j] 代表在[i,j]区间上 选手最多能取的value 总和
- 同样, sum[i][j]表示[i] 到 [j]间的value总和
- 对手的最差情况, 也就是先手的最好情况:
- dp[i][j] = sum[i][j] - Math.min(dp[i][j - 1], dp[i + 1][j]);
- 这里需要search, 画出tree可以看明白是如何根据取前后而分段的.

#### 博弈 + 区间DP
- 因为是看区间[i,j]的情况, 所以可以想到是区间 DP
- 这个方法需要复习, 跟数学表达式的推断相关联: S(x) = - S(y) + m. 参考下面的公式推导.
- dp[i][j]表示 从index(i) 到 index(j), 先手可以拿到的最大值与对手的数字差. 也就是S(x).
- 其中一个S(x) = dp[i][j] = a[i] - dp[i + 1][j]
- m 取在开头, m 取在末尾的两种情况:
- dp[i][j] = max{a[i] - dp[i + 1][j], a[j] - dp[i][j - 1]}
- len = 1, 积分就是values[i]
- 最后判断 dp[0][n] >= 0, 最大数字和之差大于0, 就赢.
- 时间/空间 O(n^2)

##### 公式推导
- S(x) = X - Y, 找最大数字和之差, 这里X和Y是选手X的总分, 选手Y的总分. 
- 对于选手X而言: 如果S(x)最大值大于0, 就是赢了; 如果最大值都小于0, 就一定是输了. 
- 选手Y: S(y)来表示 对于Y,  最大数字和之差. S(y) = Y - X
- 根据S(x) 来看, 如果从 数字和X里面, 拿出一个数字 m, 也就是 X = m + Xwithout(m)
- S(x) = m + Xwithout(m) - Y = m + (Xwithout(m) - Y). 
- 如果我们从全局里面索性去掉m, 那么 S(y'') = Y - Xwithout(m)
- 那么推算下来: S(x) = m + (Xwithout(m) - Y) = m - (Y - Xwithout(m)) = m - S(y'')
- 在这个问题里面, 我们model X 和 Y的时候, 其实都是 dp[i][j], 而区别在于先手/后手.
- 将公式套用, 某一个S(x) = a[i] - dp[i + 1][j],  也就是m=a[i], 而 S(y'') = dp[i + 1][j]

##### 注意
- 如果考虑计算先手[i, j]之间的最大值, 然后可能还需要两个数组, 最后用于比较先手和opponent的得分大小 => 那么就要多开维.
- 我们这里考虑的数字差, 刚好让人不需要计算先手的得分总值, 非常巧妙.
- Trick: 利用差值公式, 推导有点难想到.

##### 区间型动态规划
- 找出[i, j]区间内的性质: dp[i][j]下标表示区间范围 [i, j]
- 子问题: 砍头, 砍尾, 砍头砍尾
- loop应该基于区间的length
- template: 考虑len = 1, len = 2; 设定i的时候一定是 i <= n - len; 设定j的时候, j = len + i - 1;




---

**29. [Burst Balloons.java](https://github.com/awangdev/LintCode/blob/master/Java/Burst%20Balloons.java)**      Level: Hard
      

一排球, 每个球有value, 每次扎破一个, 就会积分: 左*中间*右 的值. 求, 怎么扎, 最大值?

TODO: Need more thoughts on why using dp[n + 2][n + 2] for memoization, but dp[n][n] for interval DP.

#### Interval DP
- 因为数组规律会变, 所以很难找'第一个burst的球'. 反之, 想哪一个是最后burst?
- 最后burst的那个变成一堵墙: 分开两边, 分开考虑, 加法原理; 最后再把中间的加上.
- dp[i][j] represent max value on range [i, j)
- Need to calculate dp[i][j] incrementally, starting from range size == 3 ---> n
- Use k to divide the range [i, j) and conquer each side.

##### Interval DP 三把斧:
- 中间劈开
- 砍断首或尾
- Range区间作为iteration的根本

##### Print the calculation process
- use pi[i][j] and print recursively.
- Print k, using pi[i][j]: max value taken at k

#### Memoization
- 其实会做之后挺好想的一个DP
- dp[i][j] =  balloons i~j 之间的 max. 
- 然后找哪个点开始burst? 设为x。
- For loop 所有的点作为x， 去burst。
- 每次burst都切成了三份：左边可以recusive 求左边剩下的部分的最大值 + 中间3项相乘 + 右边递归下去求最大值。
- Note: 这个是Memoization, 而不纯是DP
- 因为recursive了，其实还是搜索，但是memorize了求过的值，节省了Processing




---

**30. [Nim Game.java](https://github.com/awangdev/LintCode/blob/master/Java/Nim%20Game.java)**      Level: Easy
      

#### Brainteaser
- 著名Nim游戏
- 写一些，发现n=4,5,6,7,8...etc之后的情况有规律性: 谁先手拿到4就输了.
- 最终很简单n%4!=0就可以了,  time, space O(1)

#### DP
- 正规地找规律做, 就跟 coins in a line 一样, 按照先手后手来做
- 可以rolling array 优化空间
- Time O(n), 当然啦, 这个题目这样会timeout, 可以使用brainteaser的做法写出结果.



---

**31. [K Edit Distance.java](https://github.com/awangdev/LintCode/blob/master/Java/K%20Edit%20Distance.java)**      Level: Hard
      

给一串String, target string, int k. 找string array里面所有的candidate: 变化K次, 能变成target.

#### Trie
TODO

#### Double Sequence DP
- Edit Distance的follow up.
- 其实就是改一下 minEditDistance的function, 带入K作比较罢了.
- 写起来跟Edit Distance 的主要逻辑是一模一样的.
- 但是LintCode 86% test case 时候timeout. 
- Time O(mnh), where h = words.length, 如果 n ~ m, Time 就几乎是 O(n^2), 太慢.



---

**32. [Jump Game.java](https://github.com/awangdev/LintCode/blob/master/Java/Jump%20Game.java)**      Level: Medium
      

给出步数，看能不能jump to end.

#### DP
- DP[i]: 在i点记录，i点之前的步数是否可以走到i点？ True of false.
- 其实j in [0~i)中间只需要一个能到达i 就好了
- Function: DP[i] = DP[j] && (A[j] >= i - j), for all j in [0 ~ i)
- Return: DP[dp.length - 1];
- It timesout, O(n^2)

#### Greedy
- Keep track of farest can go
- 一旦 farest >= nums.length - 1, 也就是到了头, 就可以停止, return true.
- 一旦 farest <= i, 也就是说, 在i点上, 已经走过了步数, 不能再往前跳, 于是 return false



---

**33. [Coin Change 2.java](https://github.com/awangdev/LintCode/blob/master/Java/Coin%20Change%202.java)**      Level: Medium
      

给串数字, target amount, 求总共多少种方式可以reach the amount.

#### DP
- O(MN): M, total target amount; N: size of coins
- 状态: dp[i]: sum of ways that coins can add up to i.
- Function: dp[j] += dp[j - coins[i]];
- Init: dp[0] = 1 for ease of calculation; other dp[i] = 0 by default
- note: 避免重复count, 所以 j = coins[i] as start
- 注意 coins 可能需要放在for loop 外面, 而主导换coin的流程. 
- 类似于: 网格dp, unique path 里面的2种走法: 从上到下, 从左到右



---

**34. [Paint House.java](https://github.com/awangdev/LintCode/blob/master/Java/Paint%20House.java)**      Level: Easy
      

要paint n个房子, 还有 nx3的cost[][]. 求最少用多少cost paint 所有房子.

#### Sequence DP
- 求知道dp[n]的min cost, 但是不知道最后一个房子选什么颜色
- 那么就遍历最后一个房子(i - 1)的颜色
- 选中最后一个房子的颜色同时, 来选择 (i - 2)的颜色, 来找出最低的cost
- 考虑DP最后一个位置的情况. 发现给出了一些特殊条件, 需要附带在DP[i]上,
- 那么就定义二维数组

#### Rolling Array
- 观察发现 index[i] 只跟 [i-1] 相关, 所以2位就足够, %2


---

**35. [Decode Ways.java](https://github.com/awangdev/LintCode/blob/master/Java/Decode%20Ways.java)**      Level: Medium
      

给出一串数字, 要翻译(decode)成英文字母. [1 ~ 26] 对应相对的英文字母. 求有多少种方法可以decode.

#### Partition DP
- 确定末尾的2种状态: single letter or combos. 然后计算出单个letter的情况, 和双数的情况
- 定义dp[i] = 前i个digits最多有多少种decode的方法. new dp[n + 1].
- 加法原理: 把不同的情况, single-digit, double-digit 的情况加起来
- note: calculate number from characters, need to - '0' to get the correct integer mapping.
- 注意: check value != '0', 因为'0' 不在条件之中(A-Z)




---

**36. [Longest Continuous Increasing Subsequence.java](https://github.com/awangdev/LintCode/blob/master/Java/Longest%20Continuous%20Increasing%20Subsequence.java)**      Level: Easy
      

找连续的持续上升子序列的长度.

#### Coordinate DP
- 1D coordinate, dp 的角标, 就是代表 index i 的状态
- 求最值, dp[i] = 在index i位置的最长子序列
- 如果 nums[i] > nums[i - 1], dp[i] = dp[i - 1] + 1
- 如果没有持续上升, 那么dp[i] = 1, 重头来过
- maintain max

#### Basic
- 用一个数存current count,  maintain max



---

**37. [Minimum Path Sum.java](https://github.com/awangdev/LintCode/blob/master/Java/Minimum%20Path%20Sum.java)**      Level: Medium
      

#### DP
- Time, Space O(MN)
- 往右下角走, 计算最短的 path sum. 典型的坐标型.
- 注意: init 第一行的时候, 要accumulate dp[0][j - 1] + grid[i][j], 而不是单纯assign grid[i][j]

#### Rolling Array
- Time O(MN), Space O(1)
- 需要在同一个for loop里面完成initialization, 和使用dp[i][j]
- 原因: dp[i % 2][j] 在被计算出来的时候, 是几乎马上在下一轮是要被用的; 被覆盖前不备用,就白算
- 如果按照第一种方法, 在开始initialize dp, 看起来固然简单, 但是不方便空间优化



---

**38. [Counting Bits.java](https://github.com/awangdev/LintCode/blob/master/Java/Counting%20Bits.java)**      Level: Medium
      

给一个数组, 算里面有多少bit 1. 

#### Bitwise DP
- 对于每一个数字, 其实很简单就能算出来: 每次 >>1, 然后 & 1 就可以count 1s. Time: 一个数字可以 >>1 O(logN) 次
- 现在要对[0 ~ num] 都计算, 也就是N个数字, 时间复杂度: O(nLogN).
- 用DP来优化, 查找过的number的1s count, 存下来在 dp[number]里面.
- 计算你顺序从 0 -> num, count过的数字就可以重复利用.
- Bit题目 用num的数值本身表示DP的状态.
- 这里, dp[i] 并不是和 dp[i-1]有逻辑关系; 而是dp[i] 和dp[i>>1], 从binary representation看出有直接关系.



---

**39. [Continuous Subarray Sum.java](https://github.com/awangdev/LintCode/blob/master/Java/Continuous%20Subarray%20Sum.java)**      Level: Medium
      

给一个非负数的数列和数字k(可正负, 可为0). 找到连续子序列(长度超过2), 使得这个subarray的sum 是 k的倍数. 问: 是否可能?

#### DP
- O(n^2)
- 需要记录在0 ~ i点(包括nums[i], 以nums[i]结尾)的sum, 坐标型动态规划.
- dp[i] = dp[i - 1] + nums[i];
- 最后移动, 作比较

#### 直接算结果
- 从sum = 每次[i ~ j]的所有情况
- 验证



---

**40. [House Robber.java](https://github.com/awangdev/LintCode/blob/master/Java/House%20Robber.java)**      Level: Easy
      

搜刮房子, 相邻的不能碰. 每个房子里有value, 求max.

#### Sequence DP
- 看最后结尾状态的前一个或前两个的情况，再综合考虑当下的
- 思考的适合搞清楚当下的和之前的情况的关系
- Sequence DP, new dp[n + 1];

#### Rolling Array
- [i]'只和前两个位子 [i-1], [i - 2]'相关
- 用%2来标记 [i], [i - 1], [i - 2]三个位置.
- 其他滚动时惯用curr/prev来表示坐标, 这里%2虽然抽象, 但是更加实用.




---

**41. [House Robber II.java](https://github.com/awangdev/LintCode/blob/master/Java/House%20Robber%20II.java)**      Level: Medium
      

和House Robber I 类似, 搜刮房子, 相邻不能动. 特点是: 现在nums排成了圈, 首尾相连.

#### Sequence DP
- 根据dp[i-1]是否被rob来讨论dp[i]: dp[i] = Math.max(dp[i-1], dp[i - 2] + nums[i - 1]);
- 特别的是，末尾的last house 和 first house相连. 这里就需要分别讨论两种情况: 第一个房子被搜刮, 或者第一个房子没被搜刮
- be careful with edge case nums = [0], only with 1 element.

#### 两个状态
- 是否搜刮了第一个房子, 分出两个branch, 可以看做两种状态.
- 可以考虑用两个DP array; 也可以加一dp维度, 补充这个状态.
- 连个维度表示的是2种状态(1st house being robbed or not); 这两种状态是平行世界的两种状态, 互不相关.

#### Rolling array
与House Robber I一样, 可以用%2 来操作rolling array



---

**42. [House Robber III.java](https://github.com/awangdev/LintCode/blob/master/Java/House%20Robber%20III.java)**      Level: Medium
      

Houses被arrange成了binary tree, 规则还是一样, 连续相连的房子不能同时抄.

求Binary Tree neighbor max 能抄多少.

#### DFS
- 判断当下的node是否被采用，用一个boolean来表示. 
- 如果curr node被采用，那么下面的child一定不能被采用.
- 如果curr node不被采用，那么下面的children有可能被采用，但也可能略过，所以这里用Math.max() 比较一下两种可能有的dfs结果。
- dfs重复计算:每个root都有4种dive in的可能性, 假设level高度是h, 那么时间O(4^(h)), where h = logN, 也就是O(n^2)

#### DP, DFS
- 并不是单纯的DP, 是在发现DFS很费劲后, 想能不能代替一些重复计算?
- 基本思想是dfs解法一致: 取root找最大值, 或者不取root找最大值
- 在root上DFS, 不在dfs进入前分叉; 每一个level按照状态来存相应的值: dp[0] root not picked, dp[1] root picked.
- Optimization: DP里面, 一口气找leftDP[]会dfs到最底层, 然后自下向上做计算
- 这个过程里面, 因为没有在外面给dfs()分叉, 计算就不会重叠, 再也不用回去visit most-left-leaf了, 算过一遍就完事.
- 然而, 普通没有dp的dfs, 在算完visited的情况下的dfs, 还要重新dfs一遍!visited的情况.
- Space O(h), time O(n), 或者说是O(2^h), where h = log(n)

#### DP 特点
- 不为状态而分叉dfs
- 把不同状态model成dp
- 每一个dfs都return一个based on status的 dp array.
- 等于一次性dfs计算到底, 然后back track, 计算顶部的每一层.
- DP 并不一定要是以n为base的. 也可以是局部的去memorize状态->value.



---

**43. [Paint House II.java](https://github.com/awangdev/LintCode/blob/master/Java/Paint%20House%20II.java)**      Level: Hard
      

一排n个房子, 每个房子可涂成k种颜色, 涂每个房子的价钱不一样, 用costs[][]表示. 

costs[0][1]表示涂了index是0的房子, 用了color 1.

规则: 相邻的两个房子不能使同一种颜色

求: 最少的cost 

#### DP
- 先考虑单纯地用dp[i]表示涂前 i 个房子的最小cost
- 但是 dp[i] 和 dp[i-1] 两个index选什么颜色会互相影响, 难讨论, 于是加状态: 序列DP被加了状态变成2D. 
- 考虑最后位, 而前一位i-1又被i位的颜色限制, 于是在考虑 min dp[i] 时候, 又多了一层iteration.
- 做dp[i][j]: # cost for 前 i 个房子, 所以要先pick (i-1) 房子的cost, 然后在找出 (i-2)房子的cost
- K种颜色 => O(NK^2)
- 如果不优化, 跟Paint House I 几乎是一模一样的代码


#### 注意
- 序列型dp[i]表示'前i-1个'的结果. 所以dp最好设定为 int[n + 1] size. 
- 然而, 颜色在这里是状态, 所以保留在 j: [ 0~k)
- [[8]] 这样的edge case. 跑不进for loop, 所以特殊handle.

#### Optimization
- O(NK)
- 如果已知每次都要从cost里面选两个不同的最小cost,那么先把最小两个挑出来, 就不必有第三个for loop 找 min
- 每次在数列里面找: 除去自己之外的最小值, 利用最小值/次小值的思想
- 维持2个最值: 最小值/次小值. 
- 计算的时候, 如果除掉的不是最小值的index, 就给出最小值; 如果除掉的是最小值的index, 就给出次小值.
- Every loop: 1. calculate the two min vlaues for each i; 2. calcualte dp[i][j]
- 如何想到优化: 把表达式写出来, 然后看哪里可以优化



---

**44. [Best Time to Buy and Sell Stock I.java](https://github.com/awangdev/LintCode/blob/master/Java/Best%20Time%20to%20Buy%20and%20Sell%20Stock%20I.java)**      Level: Easy
      

给个array of stock prices, 限制能交易(买/买)一轮, 问如何找到最大profit.

#### 理解意思是关键
- 每天都就交易价格，n天只让买卖一次，那就找个最低价买进，找个最高价卖出
- 记录每天最小值Min是多少. O(n)
- 每天都算和当下的Min买卖，profit最大多少.

#### DP
- Find min value for first i items, new dp[n + 1].
- 然后用当天的price做减法算max profit.
- Time, Space: O(n)
- 更进一步, 用一个min来表示min[i], 因为计算中只需要当下的min.

#### Rolling array
- index i only depend on [i - 2]
- Space O(n)

#### Brutle Failed
- 每天都试着买进，然后之后的每一天尝试卖出. double for loop, O(n^2). timeout.
- 其中很多都是没必要的计算：[7, 1, 5, 3, 6, 4]。 if we know buyin with 1 is cheapest, we don't need to buyin at 5, 3, 6, 4 later on; we'll only sell on higher prices.



---

**45. [Best Time to Buy and Sell Stock II.java](https://github.com/awangdev/LintCode/blob/master/Java/Best%20Time%20to%20Buy%20and%20Sell%20Stock%20II.java)**      Level: Easy
      

和Stock I 的区别：可以买卖多次，求总和的最大盈利.

#### 几种其他不同的思路:
- Greedy, 每次有相邻的diff符合profit条件, 就卖了, 最后把所有的diff加在一起. 计算delta, 其实简单粗暴, 也还不错.
- 如下, 从低谷找peek, sell.
- DP. (old dp solution BuyOn[], SellOn[])
- DFS计算所有(timeout).Improvement on DFS -> DP -> calculate sellOn[i] and buyOn[i], and then return buyOn[i]. 有点难想, 但是代码简单, 也是O(n)

#### Greedy
- 画图, 因为可以无限买卖, 所以只要有上升, 就卖
- 所有卖掉的, 平移加起来, 其实就是overall best profit
- O(n)

#### 找涨幅最大的区间，买卖：
- 找到低谷，买进:peek = start + 1 时候，就是每次往前走一步;若没有上涨趋势，继续往低谷前进。
- 涨到峰顶，卖出:一旦有上涨趋势，进一个while loop，涨到底, 再加个profit.
- profit += prices[peek - 1] - prices[start]; 挺特别的。
- 当没有上涨趋势时候，peek-1也就是start, 所以这里刚好profit += 0.

#### DP
- 想知道前i天的最大profit, 那么用sequence DP
- 当天的是否能卖, 取决于昨天是否买进, 也就是昨天买了或者卖了的状态: 加状态, 2D DP
- 如果今天是卖的状态, 那么昨天: 要么买进了, 今天 +price 卖出; 要么昨天刚卖, 今天不可能再卖, profit等同.
- 如果今天是买的状态, 那么昨天: 要么卖掉了, 今天 -price 买入; 要么昨天刚卖, 今天不可能再买, profit等同.

#### Rolling Array
- [i] 和 [i - 1] 相关联, roll




---

**46. [Best Time to Buy and Sell Stock III .java](https://github.com/awangdev/LintCode/blob/master/Java/Best%20Time%20to%20Buy%20and%20Sell%20Stock%20III%20.java)**      Level: Hard
      

比stock II 多了一个限制：只有2次卖出机会.

#### DP加状态
- 只卖2次, 把买卖分割成5个状态模块.
- 在状态index 0, 2, 4: 没有持有股票. 1. 一直在此状态, max profit不变; 2. 刚卖掉, dp[i][前状态] + profit
- 在状态index 1, 3: 持有股票. 1. 一直在此状态, daily profit. 2. 刚刚买进, 状态改变, 但是没有profit yet: dp[i][前状态]

##### Partial profit
- 把每天的partial profit (diff)加在一起, 最终的overall profit是一样的. 唯一更好的是, 不需要记录中间买入的时间点.
- 什么时候会积累profit呢? 
- 1. 原本就持有股票的, 如果毫无动作, 那么状态不变, 积累profit diff. 
- 2. 卖出了股票, 状态改变, 积累profit diff.
- 注意: 只有在状态index: 0, 2, 4, 也就是卖掉股票的时候, 猜可以积累profit

##### Rolling Array
- [i] 只有和 [i-1] 打交道, reduce space
- O(1) space, O(n) time

#### 找峰头
- 找峰头；然后往下再找一个峰头。
- 怎么样在才能Optimize两次巅峰呢？从两边同时开始找Max！（棒棒的想法）
- leftProfit是从左往右，每个i点上的最大Profit。
- rightProfit是从i点开始到结尾，每个点上的最大profit.
- 那么在i点上，就是leftProfit，和右边rightProfit的分割点。在i点，leftProfit+rightProfit相加，找最大值。
- 三个O(n),还是O(n)



---

**47. [Best Time to Buy and Sell Stock IV.java](https://github.com/awangdev/LintCode/blob/master/Java/Best%20Time%20to%20Buy%20and%20Sell%20Stock%20IV.java)**      Level: Hard
      

有int[] price of stock, 最多做 k transactions.  求最大profit.

#### DP
- 根据StockIII, 不难发现StockIV就是把状态划分为2k+1份. 那么同样的代码, 移植.

##### 注意1: 
- 如果k很大, k>n/2, 那么长度为n的数组里面, 最多也只能n/2个transaction
- 那么题目简化为stockII, 给n数组, 无限次transaction.
- 注意, status的数量是 2k+1
- Time O(NK), Space O(2k+1) to store the status

##### 注意2: 
- 最后状态是'没有stock'的都该考虑, 做一个 for 循环比较max. 
- 当然, 来一个profit variable, 不断比较, 也是可以的.

#### 方法2
- (previous notes, 熟练第一种方法的思考就可以)
- 记得要理解：为什么 i-1天的卖了又买，可以和第 i 天的卖合成一次交易？    
- 因为每天交易的price是定的。所以卖了又买，等于没卖！这就是可以合并的原因。要对价格敏感啊少年。
- Inspired from here: http://liangjiabin.com/blog/2015/04/leetcode-best-time-to-buy-and-sell-stock.html

##### 局部最优解 vs. 全局最优解：     
- local[i][j] = max(global[i – 1][j – 1] + diff, local[i – 1][j] + diff)    
- global[i][j] = max(global[i – 1][j], local[i][j])     
- local[i][j]: 第i天，当天一定进行第j次交易的profit     
- global[i][j]: 第i天，总共进行了j次交易的profit.

- local[i][j]和global[i][j]的区别是：local[i][j]意味着在第i天一定有交易（卖出）发生。    
- 当第i天的价格高于第i-1天（即diff > 0）时，那么可以把这次交易（第i-1天买入第i天卖出）跟第i-1天的交易（卖出）合并为一次交易，即local[i][j]=local[i-1][j]+diff；    
- 当第i天的价格不高于第i-1天（即diff<=0）时，那么local[i][j]=global[i-1][j-1]+diff，而由于diff<=0，所以可写成local[i][j]=global[i-1][j-1]。    
- (Note:在我下面这个solution里面没有省去 +diff）   

- global[i][j]就是我们所求的前i天最多进行k次交易的最大收益，可分为两种情况：    
- 如果第i天没有交易（卖出），那么global[i][j]=global[i-1][j]；     
- 如果第i天有交易（卖出），那么global[i][j]=local[i][j]。    





---

**48. [Russian Doll Envelopes.java](https://github.com/awangdev/LintCode/blob/master/Java/Russian%20Doll%20Envelopes.java)**      Level: Hard
      

俄罗斯套娃, 这里用envelope来表现. 给一串array, 每一个[x, y] 是envelope 长宽. [[5,4],[6,4],[6,7],[2,3]]. 

看用这些套娃, 可以最多套几个.

#### DP: 1D Coordinate
- envelopes没有顺序, 先排序 (主要根据第一个index排序)
- 然后观察: 排序过后, 就变成了1D的坐标动态规划.
- max number 取决于上一个成功Russian doll的 max value + 1
- 上一个index不知道, 所以遍历找上一个index. 
- 当下index i 的状态, 取决于前面index j 的状态, 所以遍历两个index.
- O(n^2)的DP, n = envelopes.length;

#### DP: 2D Coordinate
- 这个方法是自己想出来的, 但是时间复杂度太大, timeout
- 把envelop标记在2D grid上面, 然后像走机器人一样, 求到最右下角的最大 count max.
- count 当下能存在多少Russian doll
- 两种情况: 当下coordinate 没有target, 当下coordinate有target
- 当下coordinate 没有target: 如同机器人走法, Math.max(dp[i - 1][j], dp[i][j - 1])
- 当下coordinate 有target: dp[i - 1][j - 1] + dp[i][j]
- timeout: O(n^2), n = largest coordinate.




---

**49. [Jump Game II.java](https://github.com/awangdev/LintCode/blob/master/Java/Jump%20Game%20II.java)**      Level: Hard
      

给一串数字 是可以跳的距离. goal: 跳到最后的index 所可能用的最少次数.

#### DP 
- DP[i]: 在i点记录，走到i点上的最少jump次数
- dp[i] = Math.min(dp[i], dp[j] + 1);
- condition (j + nums[j] >= i)
- 注意使用 dp[i] = Integer.MAX_VALUE做起始值, 来找min

#### Previous Notes
- Greedy, 图解 http://www.cnblogs.com/lichen782/p/leetcode_Jump_Game_II.html
- 维护一个range, 是最远我们能走的. 
- index/i 是一步一步往前, 每次当 i <= range, 做一个while loop， 在其中找最远能到的地方 maxRange
- 然后更新 range = maxRange
- 其中step也是跟index是一样, 一步一步走.
- 最后check的condition是，我们最远你能走的range >= nums.length - 1, 说明以最少的Step就到达了重点。Good.



---

**50. [Backpack.java](https://github.com/awangdev/LintCode/blob/master/Java/Backpack.java)**      Level: Medium
      

给i本书, 每本书有自己的重量 int[] A, 背包有自己的大小M, 看最多能放多少重量的书?

#### Backpack DP 1
- 简单直白的思考 dp[i][m]: 前i本书, 背包大小为M的时候, 最多能装多种的书?
- **注意**: 背包问题, 重量weight一定要是一维.
- dp[i][j] = Math.max(dp[i][j], dp[i - 1][j - A[i - 1]] + A[i - 1]);
- 每一步都track 最大值
- 最后return dp[n][m]
- 时间空间  O(mn)
- Rolling array, 空间O(m)

#### Backpack DP 2
- true/false求解, 稍微曲线救国: 重点是, 最后, 按照weight从大到小遍历, 第一个遇到true的, index就是最大值.  
- 考虑: 用i个item (可跳过地取), 是否能装到weight w?
- 需要从'可能性'的角度考虑, 不要搞成单一的最大值问题.
- 1. 背包可装的物品大小和总承重有关.
- 2. 不要去找dp[i]前i个物品的最大总重, 找的不是这个. 
    dp[i]及时找到可放的最大sum, 但是i+1可能有更好的值, 把dp[i+1]变得更大更合适.

##### 做法
- boolean[][] dp[i][j]表示: 有前i个item, 用他们可否组成size为j的背包? true/false.
- (反过来考虑了，不是想是否超过size j, 而是考虑是否能拼出exact size == j)
- **注意**: 虽然dp里面一直存在i的位置, 实际上考虑的是在i位置的时候, 看前i-1个item.

##### 多项式规律
- 1. picked A[i-1]: 就是A[i-1]被用过, weight j 应该减去A[i-1]. 那么dp[i][j]就取决于dp[i-1][j-A[i-1]]的结果.
- 2. did not pick A[i-1]: 那就是说, 没用过A[i-1], 那么dp[i][j]就取决于上一行d[i-1][j]
- dp[i][j] = dp[i - 1][j] || dp[i - 1][j - A[i - 1]]

##### 结尾
- 跑一遍dp 最下面一个row. 从末尾开始找, 最末尾的一个j (能让dp[i][j] == true)的, 就是最多能装的大小 :)   
- 时间，空间都是：O(mn)




---

**51. [Backpack II.java](https://github.com/awangdev/LintCode/blob/master/Java/Backpack%20II.java)**      Level: Medium
      

给i本书, 每本书有自己的重量 int[] A, 每本书有value int[] V

背包有自己的大小M, 看最多能放多少value的书?

#### Backpack DP
- 做了Backpack I, 这个就如出一辙, 只不过: dp存的不是max weight, 而是 value的最大值.
- 想法还是，选了A[i - 1] 或者没选A[i - 1]时候不同的value值.
- 时间空间O(mn)
- Rolling Array, 空间O(m)

#### Previous DP Solution
- 如果无法达到的w, 应该mark as impossible. 一种简单做法是mark as -1 in dp. 
- 如果有负数value, 就不能这样, 而是要开一个can[i][w]数组, 也就是backpack I 的原型.
- 这样做似乎要多一些代码, 好像并不是非常需要




---

**52. [Backpack V.java](https://github.com/awangdev/LintCode/blob/master/Java/Backpack%20V.java)**      Level: Medium
      

#### Backpack DP
- 与背包1不同: 这里不是check可能性(OR)或者最多能装的size是多少; 而是计算有多少种正好fill的可能性.
- dp[i][w]: 用前i本书, 正好fill到 w weight的可能性.
- 对于末尾, 还是两种情况:
- 1. i-1位置没有加bag
- 2. i-1位置加了bag
- 两种情况可以fill满w的情况加起来, 就是我们要的结果.
- 如常: dp[n + 1][w + 1]
- 重点: dp[0][0] 表示0本书装满weight=0的包, 这里我们必须 dp[0][0] = 1, 给后面的 dp function 做base
- Space, time: O(MN)
- Rolling array, 空间优化, 滚动数组. Space: O(M)

#### 降维打击, 终极优化
- 分析row(i-1)的规律, 发现所有row(i)的值, 都跟row(i-1)的左边element相关, 而右边element是没用的.
- 所以可以被override.
- Space: O(M), 真*一维啊!
- Time: O(MN)



---

**53. [Decode Ways II.java](https://github.com/awangdev/LintCode/blob/master/Java/Decode%20Ways%20II.java)**      Level: Hard
      

给出一串数字, 要翻译(decode)成英文字母. [1 ~ 26] 对应相对的英文字母. 求有多少种方法可以decode.

其中字符可能是 "*", 可以代表 [1 - 9]

#### DP
- 跟decode way I 一样, 加法原理, 切割点时: 当下是取了 1 digit 还是 2 digits 来decode
- 定义dp[i] = 前i个digits最多有多少种decode的方法. new dp[n + 1].
- 不同的情况是: 每一个partition里面, 如果有"*", 就会在自身延伸出很多不同的可能
- 那么: dp[i] = dp[i - 1] * (#variations of ss[i]) + dp[i - 2] * (#variations of ss[i,i+1])

##### 特点
- 枚举的能力: 具体分析 '*' 出现的位置, 枚举出数字, 基本功. 注意!!题目说 * in [1, 9].   (如果 0 ~ 9 会更难一些)
- 理解取MOD的原因: 数字太大, 取mod来给最终结果: 其实在 10^9 + 7 这么大的 mod 下, 大部分例子是能通过的.
- 枚举好以后, 其实这个题目的写法和思考过程都不难




---

**54. [Palindrome Partitioning II.java](https://github.com/awangdev/LintCode/blob/master/Java/Palindrome%20Partitioning%20II.java)**      Level: Hard
      

给一个String s, 找出最少用多少cut, 使致 切割出的每一个substring, 都是palindrome

#### Partition DP
- Find minimum cut: 分割型DP
- dp[i]: 最少cut多少刀, 使得前 i 长度的string, 割出来都是palindrome
- 最终要得到 dp[n], 所以 int[n + 1]
- 移动切刀, 看在哪里切, index j in [0 ~ i]
- 考虑[j, i - 1] 是否是回文串, 如果是, 那么: dp[i]= min(dp[i], d[j] + 1).
- note: 估计遍历 j 的时候, 反过来遍历也可以.

#### 计算Palindrome的优化
- 利用palindrome的性质, 可以算出 boolean palindrome[i, j]的情况. 
- 找一个任意mid point:
- 1. 假设palindrome是奇数长度, 那么 mid 是单独的字符, 而两边的字符 [mid-1], [mid+1] 应该完全相等.
- 2. 假设palindrome是偶数长度, 那么 [mid] 和 [mid + 1] 这样位置的字符应该相等.
- 这样做出来 palindrome[i, j]: 从字符 i 到 字符 j 的 substring 是否是 palindrome
- 这样就给我们的问题合理降维, 目前是time: O(n^2). 
- 不然求一次palindrome, 就是n, 会变成O(n^3)

#### Previous Notes
- Double for loop 检查每种substring string (i~j). 若i,j相邻或者同点，那么肯定isPal；否则，i,j之间的（i+1, j-1）一定得isPal。
- 看上去，在检查i,j的时候，中间按的（i+1, j-1）怎么可能先知道？ 其实不然..在j慢慢长大的时候，所有的0~j的substring都检查过。所以isPal[i+1][j-1]一定是已经知道结果的。
- okay.那么假如以上任意一种情况成立，也就是说isPal[i][j] == true。那就要判断，切到第一层循环参数j的末尾点时，有多少种切法？
- 想法很顺：我们naturally会想到，把i之前的cut加上i~j之间发生的不就好了。
- 反正现在j不变，现在就看吧i定在哪里，cut[i - 1]是否更小/最小； 再在cut[i-1]基础上+1就完了。
- 当然，如果i==0, 而 i~j又是isPal,那没啥好谈的，不必切，0刀。
- 最终，刷到cut[s.length() - 1] 也就是最后一点。 return的理所应当。




---

**55. [Backpack III.java](https://github.com/awangdev/LintCode/blob/master/Java/Backpack%20III.java)**      Level: Hard
      

给n种不同的物品, int[] A weight, int[] V value, 每种物品可以用无限次

问最大多少value可以装进size是 m 的包?

#### DP
- 可以无限使用物品, 就失去了last i, last unique item的意义: 因为可以重复使用.
- 所以可以转换一个角度:
- 1. 用i **种** 物品, 拼出w, 并且满足题目条件(max value). 这里因为item i可以无限次使用, 所以考虑使用了多少次K.
- 2. K虽然可以无限, 但是也被 k*A[i]所限制: 最大不能超过背包大小.
- dp[i][w]: 前i种物品, fill weight w 的背包, 最大价值是多少.
- dp[i][w] = max {dp[i - 1][w - k*A[i-1]] + kV[i-1]}, k >= 0
- Time O(nmk)
- 如果k = 0 或者 1, 其实就是 Backpack II: 拿或者不拿

#### 优化
- 优化时间复杂度, 画图发现:
- 所计算的 (dp[i - 1][j - k*A[i - 1]] + k * V[i - 1]) 
- 其实跟同一行的 dp[i][j-A[i-1]] 那个格子, 就多出了 V[i-1]
- 所以没必要每次都 loop over k times
- 简化: dp[i][j] 其中一个可能就是: dp[i][j - A[i - 1]] + V[i - 1]
- Time O(mn)

#### 空间优化到1维数组
- 根据上一个优化的情况, 画出 2 rows 网格
- 发现 dp[i][j] 取决于: 1. dp[i - 1][j], 2. dp[i][j - A[i - 1]]
- 其中: dp[i - 1][j] 是上一轮 (i-1) 的结算结果, 一定是已经算好, ready to be used 的
- 然而, 当我们 i++,j++ 之后, 在之前 row = i - 1, col < j的格子, 全部不需要.
- 降维简化: 只需要留着 weigth 这个 dimension, 而i这个dimension 可以省略: 
- (i - 1) row 不过是需要用到之前算出的旧value: 每一轮, j = [0 ~ m], 那么dp[j]本身就有记录旧值的功能.
- 变成1个一位数组
- 降维优化的重点: 看双行的左右计算方向
- Time(mn). Space(m)



---

**56. [Longest Common Substring.java](https://github.com/awangdev/LintCode/blob/master/Java/Longest%20Common%20Substring.java)**      Level: Medium
      

#### Double Sequence DP
- 两个string, 找最值: longest common string length
- 序列型, 并且是双序列, 找两个序列 (两维的某种性质)
- dp[i][j]: 对于 A 的前i个字母, 对于 B 的前j个字母, 找最长公共substring的长度
- dp = new int[m + 1][n + 1]
- dp[i][j] = dp[i - 1][j - 1] + 1; only if A.charAt(i - 1) == B.charAt(j - 1)
- 注意track max, 最后return
- space O(n^2), time(n^2)

##### Rolling array
- 空间优化, [i] 只有和 [i - 1] 相关, 空间优化成 O(n)

#### String
- 找所有A的substring, 然后B.contains()
- track max substring length
- O(n^2) time



---

**57. [Longest Increasing Continuous subsequence.java](https://github.com/awangdev/LintCode/blob/master/Java/Longest%20Increasing%20Continuous%20subsequence.java)**      Level: Easy
      

https://leetcode.com/problems/longest-continuous-increasing-subsequence/description/

O(n)跑2遍for.
O(1)是用了两个int来存：每次到i点时，i点满足条件或不满足条件所有的longestIncreasingContinuousSubsequence.
特点：返跑一回，ans还是继续和left轮的ans作比较；求的所有情况的最大值嘛。



---

**58. [Longest Increasing Continuous subsequence II.java](https://github.com/awangdev/LintCode/blob/master/Java/Longest%20Increasing%20Continuous%20subsequence%20II.java)**      Level: Medium
      

#### Coordinate DP
- due to access permission, not test
- dp[i][j]: longest continuous subsequence length at coordinate (i, j)
- dp[i][j] should come from (i-1,j) and (i, j-1).
- dp[0][0] = 1
- condition: from up/left, must be increasing
- return dp[m-1][n-1]

#### Memoization
- O(mn) space for dp and flag.
- O(mn) runtime because each spot will be marked once visited. 
- 这个题目的简单版本一个array的例子：从简单题目开始想DP会简单一点。每个位置，都是从其他位置（上下左右）来的dpValue +　１.　如果啥也没有的时候，init state 其实都是1， 就一个数字，不增不减嘛。




---

**59. [Maximum Subarray.java](https://github.com/awangdev/LintCode/blob/master/Java/Maximum%20Subarray.java)**      Level: Easy
      

给一串数组, 找数组中间 subarray 数字之和的最大值

#### Sequence DP
- dp[i]: 前i个element, 包括element i 在内的 continous subsequence 的最大sum是多少?
- 因为continous sequence, 所以不满足条件的时候, 会断: track overall max,
- init dp[0] = 0; max = MIN_VALUE 因为有负数
- Time, space O(n)
- Rolling array, space O(1)

#### Divide and Conquer
- 找一个mid piont, 考虑3种情况: 只要左边, 只要右边, cross-mid
- left/rigth 的case, 直接 dfs
- corss-mid case: continuous sum max from left + continous sum max from right + mid
- continuous sum max from one direction:


---

**60. [Maximum Subarray II.java](https://github.com/awangdev/LintCode/blob/master/Java/Maximum%20Subarray%20II.java)**      Level: Medium
      

给一串数组, 找数组中间 两个不交互的 subarray 数字之和的最大值

#### DP
- 考虑两个方向的dp[i]: 包括i在内的subarray max sum. 
- dp[i] 的特点是: 如果上一个 dp[i - 1] + nums[i - 1] 小于 nums[i-1], 那么就舍弃之前, 从头再来:
- dp[i] = Math.max(dp[i - 1] + nums.get(i - 1), nums.get(i - 1));
- 缺点: 无法track全局max, 需要记录max.
- 因为我们现在要考虑从左边/右边来的所有max, 所以要记录maxLeft[] 和 maxRight[] 
- maxLeft[i]: 前i个元素的最大sum是多少 (不断递增); maxRight反之, 从右边向左边
- 最后比较maxLeft[i] + maxRight[i] 最大值
- Space, Time O(n)
- Rolling array, reduce some space, but can not reduce maxLeft/maxRight

#### preSum, minPreSum
- preSum是[0, i] 每个数字一次加起来的值
- 如果维持一个minPreSum, 就是记录[0, i]sum的最小值(因为有可能有负数)
- preSum - minPreSum 就是在 [0, i]里, subarray的最大sum值
- 把这个最大subarray sum 记录在array, left[] 里面
- right[] 是一样的道理
- enumerate一下元素的排列顺位, 最后 max = Math.max(max, left[i] + right[i + 1])



---

**61. [Fibonacci.java](https://github.com/awangdev/LintCode/blob/master/Java/Fibonacci.java)**      Level: Easy
      

#### Memoization
- fib[n] = fibonacci(n - 1) + fibonacci(n - 2);

#### DP array.
- 滚动数组, 简化DP

#### recursively calculate
- recursively calculate fib(n - 1) + fib(n - 2). 公式没问题, 但是时间太长, timeout.




---

**62. [Combination Sum IV.java](https://github.com/awangdev/LintCode/blob/master/Java/Combination%20Sum%20IV.java)**      Level: Medium
      

给一串数字candidates (no duplicates), 和一个target. 

找到所有unique的 组合(combination) int[], 要求每个combination的和 = target.

注意: 同一个candidate integer, 可以用任意多次.

#### Backpack DP
- 计数问题, 可以想到DP. 其实就是Backpack VI.
- 从x个数字里面找candidate(可以重复用同一个数字), 来sum up to target. 找: # of ways to form the sequence.
- Backpack VI: 给一个数组nums, 全正数, 无重复数字; 找: # of 拼出m的方法
- dp[i]: # of ways to build up to target i
- consider last step: 如果上一步取的是 candidate A, 那么就该加到dp[i]:
- dp[i] += dp[i - A]
- 要找overall dp[i], 就做一个for loop: dp[i] = sum{dp[i - num]}, where for (num: nums)
- Time: O(mn). m = size of nums, n = target
- If we optimize dp for loop, 需要Sort nums. O(mlogm). will efficient 如果m是constant或者relatively small. Overall: O(n)

#### DFS, backtracking
- 尽管思考方式是对的, 但是 times out
- 可以重复使用数字的时候, 比如用1 来拼出 999, 这里用1就可以走999 dfs level, 不efficient



---




 
 
 
## Double Sequence DP (4)
**0. [Longest Common Subsequence.java](https://github.com/awangdev/LintCode/blob/master/Java/Longest%20Common%20Subsequence.java)**      Level: Medium
      

给两个string, A, B. 找这两个string里面的LCS: 最长公共字符长度 (不需要是continuous substring)

#### Double Sequence DP
- 设定dp长度为(n+1), 因为dp[i]要用来表示前i个(ith)时候的状态, 所以长度需要时i+1才可以在i位置, hold住i.
- 双序列: 两个sequence之间的关系, 都是从末尾字符看起, 分析2种情况:
- 1. A最后字符不在common sequence 或者 B最后字符不在common sequence.
- 2. A/B最后字符都在common sequence. 总体count + 1.



---

**1. [Edit Distance.java](https://github.com/awangdev/LintCode/blob/master/Java/Edit%20Distance.java)**      Level: Hard
      

两个字符串, A要变成B, 可以 insert/delete/replace, 找最小变化operation count

#### Double Sequence
- 考虑两个字符串变换的最后点: 需要insert/delete/replace? 分析每种情况, 然后列出表达式.
- 先calculate最坏的情况, 3种operation count + 1; 然后在比较match的情况.
- 注意, 在i或者j为0的时候, 变成另外一个数字的steps只能是全变.
- 第一步, 空间时间都是O(MN)
- 滚动数组优化, 空间O(N)

#### Search



---

**2. [K Edit Distance.java](https://github.com/awangdev/LintCode/blob/master/Java/K%20Edit%20Distance.java)**      Level: Hard
      

给一串String, target string, int k. 找string array里面所有的candidate: 变化K次, 能变成target.

#### Trie
TODO

#### Double Sequence DP
- Edit Distance的follow up.
- 其实就是改一下 minEditDistance的function, 带入K作比较罢了.
- 写起来跟Edit Distance 的主要逻辑是一模一样的.
- 但是LintCode 86% test case 时候timeout. 
- Time O(mnh), where h = words.length, 如果 n ~ m, Time 就几乎是 O(n^2), 太慢.



---

**3. [Longest Common Substring.java](https://github.com/awangdev/LintCode/blob/master/Java/Longest%20Common%20Substring.java)**      Level: Medium
      

#### Double Sequence DP
- 两个string, 找最值: longest common string length
- 序列型, 并且是双序列, 找两个序列 (两维的某种性质)
- dp[i][j]: 对于 A 的前i个字母, 对于 B 的前j个字母, 找最长公共substring的长度
- dp = new int[m + 1][n + 1]
- dp[i][j] = dp[i - 1][j - 1] + 1; only if A.charAt(i - 1) == B.charAt(j - 1)
- 注意track max, 最后return
- space O(n^2), time(n^2)

##### Rolling array
- 空间优化, [i] 只有和 [i - 1] 相关, 空间优化成 O(n)

#### String
- 找所有A的substring, 然后B.contains()
- track max substring length
- O(n^2) time



---




 
 
 
## BFS (20)
**0. [Perfect Squares.java](https://github.com/awangdev/LintCode/blob/master/Java/Perfect%20Squares.java)**      Level: Medium
      

给一个数字n, 找到这个数字 最少能用多少个 平方数组成. 

平方数比如: 1, 4, 9, 16 ... etc

#### Partition DP
- 遇到最值, 想到DP.
- 看到分割字眼, 想到分割型 DP. 
- 思考, 如果 j * j = 9, 那么 j = 3 就是最少的一步; 但是如果是10呢? 就会分割成1 + 9 = 1 + j * j 
- 考虑最后的数字: 要是12割个1出来, 剩下11怎么考虑? 割个4出来,剩下8怎么考虑?
- partion的方式: 在考虑dp[i - x]的时候,  x 不是1, 而是 x = j*j.
- 就变成了dp = Min{dp[i - j^2] + 1}

#### 时间复杂度
- 乍一看是O(n*sqrt(n)). 实际也是. 但如何推导?
- 考虑上限: 把小的数字变成大的 推导上限; 考虑下限: 把数字整合归小, 找到下限.
- 考虑sqrt(1) + sqrt(2) + ....sqrt(n):找这个的upper bound and lower bound.
- 最后发现它的两边是 A*n*sqrt(n) <= actual time complexity <= B*n*sqrt(n)
- 那么就是O(n*sqrt(n))啦

#### Previous Notes
- 一开始没clue.看了一下提示
- １.　第一步想到了，从数学角度，可能是从最大的perfect square number开始算起。
- ２.　然后想法到了dp， 假设最后一步用了最大的maxSqrNum, 那么就在剩下的 dp[i - maxSqrNum^2] +１　不就好了？
- ３.　做了，发现有个问题．．．最后一步选不选maxSqrNum?  比如12就是个例子。
- 然后就根据提示，想到BFS。顺的。 把1～maxSqrNum 都试一试。找个最小的。
- 看我把12拆分的那个example. 那很形象的就是BFS了。
- 面试时候，如果拆分到这个阶段不确定，那跟面试官陶瓷一下，说不定也就提示BFS了。



---

**1. [Nested List Weight Sum.java](https://github.com/awangdev/LintCode/blob/master/Java/Nested%20List%20Weight%20Sum.java)**      Level: Easy
      

给一串integers, list里面可能有nest list. 算总的sum. 规则, 如果是nested list, 每深一个depth, sum要乘以depth.

#### DFS
- 简单的处理nested structure, dfs增加depth.

#### BFS
- bfs, queue, 处理queue.size().



---

**2. [Clone Graph.java](https://github.com/awangdev/LintCode/blob/master/Java/Clone%20Graph.java)**      Level: Medium
      

给一个graph node, 每个node有list of neighbors. 复制整个graph, return new head node.

#### 思想
- Use HashMap to mark cloned nodes.    
- 先能复制多少Node复制多少. 然后把neighbor 加上

#### DFS
- copy the node
- Mark 'added' using map(old, new)
- for loop on the each one of the neighbors: map copy, record in map, and further dfs
- once dfs completes, add newNeighbor as neighbor of the new node (get to it via map)
- 主要思想是: 一旦复制过了, 不必要重新复制

#### BFS
_ Copy the root node, then copy all the neighbors. 
_ Mark copied node in map.
_ Use queue to contain the newly added neighbors. Need to work on them in the future.

#### Note
initialize map with (node, newNode)



---

**3. [Number of Islands.java](https://github.com/awangdev/LintCode/blob/master/Java/Number%20of%20Islands.java)**      Level: Medium
      

给一个2Dmatrix, 里面是1和0, 找#of island.


#### DFS
- top level 有一个 double for loop, 查看每一个点.
- 每当遇到1, count+1, 然后DFS helper function 把每个跟这个当下island 相关的都Mark成 '0'
- 这样确保每个visited 过得island都被清扫干净

#### Union Find
- 可以用union-find， 就像Number of island II 一样。
- 只不过这个不Return list, 而只是# of islands
- 记住UnionFind的模板和几个变化(Connecting Graph I, II, III), 最后归总的代码写起来就比较简单.



---

**4. [Graph Valid Tree.java](https://github.com/awangdev/LintCode/blob/master/Java/Graph%20Valid%20Tree.java)**      Level: Review
      

M 

给一个数字n代表n nodes, marked from 1 ~ n, 和一串undirected edge int[][]. 检查这些edge是否能合成一个 valid tree

#### Union Find
- 复习Union-Find的另外一个种形式, track union size
- 题目类型：查找2个元素是不是在一个union里面。如果不在，false. 如果在，那就合并成一个set,共享parent.   
- 存储的关键都是：元素相对的index上存着他的root parent.    
- 注意: 结尾要检查, 是否只剩下1个union: Tree必须连接到所有给出的node.
- 另一个union-find, 用hashmap的:
- http://www.lintcode.com/en/problem/find-the-weak-connected-component-in-the-directed-graph/

#### DFS
- (还没做, 可以写一写)
- 检查: 1. 是否有cycle, 2. 是否所有的node全部链接起来

#### BFS
- (还没做, 可以写一写)
- 也是检查: 1. 是否有cycle, 2. 是否所有的node全部链接起来



---

**5. [Surrounded Regions.java](https://github.com/awangdev/LintCode/blob/master/Java/Surrounded%20Regions.java)**      Level: Review
      

给一个2D board, 里面是 'X' 和 'O'. 把所有被X包围的area都涂成'X'. 

从四个边的edge出发, 像感染僵尸病毒一样扩散, 把靠边的node全部mark, 然后将还是'O'的改成X, 最后回复marks -> 'O'

#### Union Find
- UnionFind里面这次用到了一个rank的概念, 需要review. rank[] 也就是在tracking每一个node所在union的size.
- 目的是: always并到大的union里面
- note: 将2D coordinate (x,y) 转换成1D: index = x * n + y

#### DFS
- TODO

#### BFS
- TODO




---

**6. [Trapping Rain Water II.java](https://github.com/awangdev/LintCode/blob/master/Java/Trapping%20Rain%20Water%20II.java)**      Level: Hard
      

用PriorityQueue把选中的height排序。为走位，create class Cell (x,y, height).

#### 注意几个理论
1. 从matrix四周开始考虑，发现matrix能Hold住的水，取决于height低的block。
2. 必须从外围开始考虑，因为水是被包裹在里面，外面至少需要现有一层。

以上两点就促使我们用min-heap: 也就是natural order的PriorityQueue<Cell>.

#### 具体步骤
1. process的时候，画个图也可以搞清楚: 就是四个方向都走走，用curr cell的高度减去周围cell的高度.
   若大于零，那么周围的cell就有积水。
2. 每个visited的cell都要mark. 
3. 根据4个方向的走位, 创建新cell 加进queue里面. 因为做的是缩小一圈的新围墙, height = Math.max(cell.h, neighbor.h);

再多一句解释: 和trapping water I 想法一样。刚刚从外围，只是能加到跟外围cell高度一致的水平面。往里面，很可能cell高度变化。   
这里要附上curr cell 和 move-to cell的最大高度。

#### 为什么想到用Heap (min-heap - priorityQueue)
- 要找到bucket的最短板
- 每次需要最先处理最短的那条 (on top)


#### 为什么从外向里遍历
- 木桶理论, 包水, 是从外面包住里面
- 洋葱剥皮, 用完丢掉



---

**7. [Course Schedule.java](https://github.com/awangdev/LintCode/blob/master/Java/Course%20Schedule.java)**      Level: Medium
      

- 一堆课用int[2] pair 来表示. [1, 0] 表示要上课1的话, 必须先把课0上了. 
- 每一个数字都是一个ndoe, 题目问是否能把所有的课排了
- input是 numOfCourses, 还有这个prerequisites [[]]

#### Topological Sort
- 给一个graph of nodes
- 至关重要: 用`List[] edges; edges[i] = new ArrayList<>();` 来表示graph: 就是每个node, to all its neighbors
- 目标是根据edge 的 direction, 把这个graph 里面的 node sort 一个list
- 如果有cycle, 这个item就不会被放在最后的list 里面. 
- 比如: 如果两个课互相是dependency, 就变成了cyclic dependency, 这样不好.


#### BFS
- Kahn algorithem:
- 先build一个graph map: <node, list of nodes >; or `List[] edges; edges[i] = new ArrayList<>();`
- count in-degree: inDegree就是每个node上面, 有多少个走进来的edge?
- 那些没有 in-coming-edge的, indegree 其实就 等于 0, 那么他们就应该在final result list里面
- 对这些 indegree == 0 的 nodes BFS, add to queue.
- 模拟visit每个ndoe, 如果visit过了, 这个node上的 indegree--, 然后如果最终 indegree == 0, 这个node就成功进入final list.

##### Indegree 原理
- Note: 如果有cycle, indegree是不会变成0的, 它也无法进入最终list. 
- indegree是周围的node到我这里的次数count. 
- 如果周围所有node的连线, 都意义切除后, 我的indegree还不等于0, 那么肯定有某些node间接地有重复连线, 也就是有cycle

#### DFS
- 这道题没有要求作出final list, 相对简单, 只要visit每个nodes, 最后确认没有cycle就好了
- 用 visited int[] 来确认是否有cycle. 1 代表 paretNode visited, -1 代表在DFS上一行的标记
- 如果遇到-1, 说明这个node在上一级或者以上的同一个dfs path里面已经走过, 那么证明有cycle, return false.
- 走完一个node的所有neighbor, 都没有fail, 那么backtracking, set visited[i] = 1
- 真的topo sort会在DFS的底端, 把record放进一个stack, 最后reverse, 就是真的sort order.

#### Notes:
- 还有 List[] arrayOfList = new ArrayList[]; 这样的操作啊, 代替了map<integer, integerList>

#### Previous notes
有点绕，但是做过一次就明白一点。    
是topological sort的题目。一般都是给有dependency的东西排序。    

最终都会到一个sink node， 再不会有向后的dependency, 在那个点截止。    
我就已这样子的点为map的key, 然后value是以这个node为prerequisite的 list of courses.    

画个图的话，prerequisite都是指向那个sink node， 然后我们在组成map的时候，都是从sink node 发散回来到dependent nodes.    

在DFS里面，我们是反向的， 然后，最先完全visited的那个node, 肯定是最左边的node了，它被mark的seq也是最高的。    

而我们的sink node，当它所有的支线都visit完了，seq肯定都已经减到最小了，也就是0，它就是第一个被visit的。   


最终结果：
每个有pre-requisit的node都trace上去（自底向上），并且都没有发现cycle.也就说明schedule可以用了。



---

**8. [Course Schedule II.java](https://github.com/awangdev/LintCode/blob/master/Java/Course%20Schedule%20II.java)**      Level: Medium
      

- 一堆课用int[2] pair 来表示. [1, 0] 表示要上课1的话, 必须先把课0上了. 
- 每一个数字都是一个ndoe, 题目求这个最后排好的课的list
- 如果排不好, 就给个空就好
- input是 numOfCourses, 还有这个prerequisites [[]]
- 做法跟Course Schedule I 非常像, 可以参考.

#### Topological Sort, Indegree, BFS
- 用`List[] edges; edges[i] = new ArrayList<>();` 来表示graph: 就是每个node, to all its neighbors
- 每个没有 inDegree==0 node, 都是可以加进 final list里面的. 比如一开始找到的那些 inDegree = 0的 node
- 注意, 如果 prerequisites = [], 那么就是说这些课都independent, 开个int[0 ~ n-1]的数组并赋值就好.
- 如果有cycle, 严格意义上就做不了topological sort, 也无法涵盖所有nodes,  那么return [ ]

#### DFS
- 根据 Course Schedule 里面的DFS 修改
- 维持visited int[]全局变量
- 维持sortedList int[] 全局变量, 注意加进去的时候是 add(0, node) 加在开头这样
- 每次到一个node的children全部DFS走完之后, 就可以把他加进final list里面
- 如果有cycle, 也就是dfs return false的时候, 这个题目判定排课失败, return new int[] { }



---

**9. [Alien Dictionary.java](https://github.com/awangdev/LintCode/blob/master/Java/Alien%20Dictionary.java)**      Level: Hard
      

给一个 array of strings: 假如这个array是按照一个新的字母排序表(alien dictionary)排出来的, 需要找到这个字母排序.

有可能有多重排序的方法, 给出一种就可以.

#### Graph
- 本质: 上下两行string, 相对应的相同的index上, 如果字母不同, 就说明排在第一行的字母在字母表里更领先
- 把 string array 变成topological sort的 graph: `map<char, list<char>>`
- 也可以`List[26] edges` (Course Schedule problem)
- Build edges: find char diff between two row, and store the order indication into graph
- 注意: indegree 永远是反向的 (跟 node to neighbors 相反的方式建立)

#### BFS
- topological sort 本身很好写, 但是要在题目中先了解到字母排序的本质
- 其实上面这个排序的本质很好想, 但是把它具体化成构建graph的代码, 会稍微有点难想到
- 算indegree, 然后用 BFS 来找到那些 inDegree == 0的 node
- 最先inDegree == 0的node, 就排在字母表前面.
- 下面的解法, 用了Graph: map<Character, List<Character>>, 而不是 List[26], 其实更加试用超过26个字母的dictionary.

#### DFS
- 跟BFS建立 grpah 的过程一模一样
- DFS的不同在于: 用visited map 来标记走过的地方
- 走到leaf的时候, add to result: 但因为走到了底才add, 最终的顺序应该颠倒 (或者, sb.insert(0, x) 直接用颠倒的顺序add)



---

**10. [Binary Tree Preorder Traversal.java](https://github.com/awangdev/LintCode/blob/master/Java/Binary%20Tree%20Preorder%20Traversal.java)**      Level: Easy
      

#### Recursive
- 加root, left, then right. Obvious
- Divide and conquer
- 其实也不需要helper function

#### Iterative
- 先加root, 然后push上需要末尾process的在stack垫底(root.right), 然后push root.left
- Stack: push curr, push right, push left.   



---

**11. [Complete Binary Tree.java](https://github.com/awangdev/LintCode/blob/master/Java/Complete%20Binary%20Tree.java)**      Level: Easy
      

A complete binary tree is a binary tree in which every level, except possibly the last,

is completely filled, and all nodes are as far left as possible

#### BFS
- 当出现了第一次有 null children的node的时候, 说明到了leaf level, mark flag = true;
- 自此以后，queue再不该有node再有child; queue后面出现的node的left/right child应该都是null
- 否则就是有问题, return false;




---

**12. [Invert Binary Tree.java](https://github.com/awangdev/LintCode/blob/master/Java/Invert%20Binary%20Tree.java)**      Level: Easy
      

#### DFS
- 简单处理swap
- recursively swap children

#### BFS
- BFS with Queue
- 每次process一个node, swap children; 然后把child加进queue里面
- 直到queue process完



---

**13. [Minimum Depth of Binary Tree.java](https://github.com/awangdev/LintCode/blob/master/Java/Minimum%20Depth%20of%20Binary%20Tree.java)**      Level: Easy
      

#### DFS
- Divide and Conquery一个最小值. 
- 注意处理Leaf的null: null leaf 出现的时候, 就忽略这个leaf, 直接return算有leaf
- 另一种count的方法: 用Integer.MAX_VALUE代替 null leaf，这样可以避免错误counting. (不能直接recursive)
- 这个无论如何都要走所有node, 所以dfs应该比较适合.

#### BFS
- 还没做



---

**14. [Symmetric Tree.java](https://github.com/awangdev/LintCode/blob/master/Java/Symmetric%20Tree.java)**      Level: Easy
      

检查tree是否symmetric

注意Symmetric Binary Tree的例子和定义: 是镜面一样的对称. 并不是说左右两个sub-tree相等。

#### DFS
- Recursively check symmetrically相对应的Node.  
- 每个node的children都和镜面另外一边相对的node的children刚好成镜面反射位置。

#### Stack
- stack1: 左手边sub-tree先加left, 再加right child; 
- stack2: 右手边sub-tree先加right child, 再加left child。   
- process时，若symmetric，所有stack里面出来的node会一一对应。



---

**15. [Binary Tree Level Order Traversal.java](https://github.com/awangdev/LintCode/blob/master/Java/Binary%20Tree%20Level%20Order%20Traversal.java)**      Level: Medium
      

如题.

#### BFS
- 最普通,Non-recursive: BFS, queue, 用个queue.size()来end for loop:换行。   
- 或者用两个queue. 当常规queue empty，把backup queue贴上去

#### DFS
- 每个level都应该有个ArrayList. 那么用一个int level来查看：是否每一层都有了相应的ArrayList。   
- 如果没有，就加上一层。    
- 之后每次都通过DFS在相应的level上面加数字。




---

**16. [Binary Tree Level Order Traversal II.java](https://github.com/awangdev/LintCode/blob/master/Java/Binary%20Tree%20Level%20Order%20Traversal%20II.java)**      Level: Medium
      

如题, 但是output要倒序.

#### BFS
- 跟Binary Tree Level Order Traversal一样,只不过存result一直存在存在0位.


#### DFS
- 根据level来append每个list
- rst里面add(0,...)每次都add在list开头



---

**17. [Subset.java](https://github.com/awangdev/LintCode/blob/master/Java/Subset.java)**      Level: Medium
      

给一串unique integers, 找到所有可能的subset. result里面不能有重复.

#### DFS
- dfs的两种路子: 1. pick&&skip dfs, 2. for loop dfs
- 1. pick&&skip dfs: 取或者不取 + backtracking. 当level/index到底，return 一个list.
- 2. for loop dfs: for loop + backtracking. 记得：做subset的时候, 每个dfs recursive call是一种独特可能，先加进rst。
- Time&&space: subset means independent choice of either pick&&not pick. You pick n times: O(2^n), 3ms

#### Bit Manipulation
- n = nums.length, 那么在每一个index, 都是 pick / not pick: 0/1
- 考虑subset index 0/1的bit map: range 的就是 [0000...00 ~ 2^n-1]
- 每一个bitmap就能展现出一个subset的内容: all the 1 represents picked indexes
- 做法:
- 1. 找出Range
- 2. 遍历每一个bitmap candidate
- 3. 对每一个integer 的 bit representation 遍历, 如果是1, add to list
- time: O(2^n * 2^n) = O(4^n), still 3ms, fast.

#### Iterative, BFS
- Regular BFS, 注意考虑如果让one level to generate next level
- 1. 用queue来存每一次的candidate indexes
- 2. 每一次打开一层candiates, add them all to result
- 3. 并且用每一轮的candidates, populate next level, back into queue.
- should be same O(2^n), but actual run time 7ms, slower





---

**18. [Subsets II.java](https://github.com/awangdev/LintCode/blob/master/Java/Subsets%20II.java)**      Level: Medium
      

给一串integers(may have duplicates), 找到所有可能的subset. result里面不能有重复.

#### DFS
- DFS, 找准需要pass along的几个数据结构. 先sort input, 然后DFS
- Using for loop approach: 每个dfs call是一种可能性，直接add into result.     
- 为了除去duplicated result, skip used item at current level: `if (i > depth && nums[i] == nums[i - 1]) continue;`
- srot O(nlogn), subset: O(2^n)

#### BFS
- Regular BFS, 注意考虑如果让one level to generate next level
- skip duplicate: `if (i > endIndex && nums[i] == nums[i - 1]) continue;`
- 1. 用queue来存每一次的candidate indexes
- 2. 每一次打开一层candiates, add them all to result
- 3. 并且用每一轮的candidates, populate next level, back into queue.
- srot O(nlogn), subset: O(2^n)
- should be same O(2^n). slower than dfs

#### Previous notes:
- 在DFS种skip duplicate candidates, 基于sorted array的技巧：    
- 一旦for loop里面的i!=index，并且nums[i] == nums[i-1],
- 说明x=nums[i-1]已经在curr level 用过，不需要再用一次: [a,x1,x2]，x1==x2    
- i == index -> [a,x1]    
- i == index + 1 -> [a,x2]. 我们要skip这一种
- 如果需要[a,x1,x2]怎么办？ 其实这一种在index变化时，会在不同的两个dfs call 里面涉及到。

#### 注意
- 不能去用result.contains(), 这本身非常costly O(nlogn)




---

**19. [Binary Tree Right Side View.java](https://github.com/awangdev/LintCode/blob/master/Java/Binary%20Tree%20Right%20Side%20View.java)**      Level: Medium
      

给一个binary tree, 从右边看过来, return all visible nodes

#### BFS
- 最右:即level traversal每一行的最末尾.   
- BFS, queue 来存每一行的内容, save end node into list

#### DFS
- Use Map<Level, Integer> 来存每一个level的结果
- dfs(node.right), 然后 dfs(node.left)



---




 
 
 
## Segment Tree (1)
**0. [Building Outline.java](https://github.com/awangdev/LintCode/blob/master/Java/Building%20Outline.java)**      Level: Review
      

又叫做skyline. 用Sweep Line做的O(nLogN), 但是貌似还有很多做法: segement tree, hashheap, treeSet?

#### 方法1: Sweep Line, Time O(nLogN), Space O(n)
original reference http://codechen.blogspot.com/2015/06/leetcode-skyline-problem.html?_sm_au_=isVmHvFmFs40TWRt

sweep line:
- 把所有点分出来， 每个点有index x, 再加上一个height.         
- 在这个list上排序，根据index和height. 注意用负数标记building start point height, 这样保证start在end 之前
- 用负数的height标记start: 在priority queue里面同一个x-pos比较 startPoint.height, endPoint.height 的时候, 因为end height是整数, 所以compare时会自动把start point放在end point前面
- 当然了, 如果两个 start point比较, 第二个point的负数超大的话(也就是height很高), 就会顺理compare return正数, 成章形成倒位
- 在processs时候用max-heap (reversed priorityqueue)，再iterate heightPoints 来存最大的height . 遇到peek,就是一个合理的解    
- heightQueue里面加一个0, 用来在结尾的时候做closure

#### 方法2: Segment Tree
REVIEW

Binary Indexed Tree?

HashHeap?



---




 
 
 
## Design (11)
**0. [Binary Search Tree Iterator.java](https://github.com/awangdev/LintCode/blob/master/Java/Binary%20Search%20Tree%20Iterator.java)**      Level: Medium
      

画一下, BST in order traversal. 用stack记录最小值, 放在top. O(h) space.
每次消耗TreeNode, 都看看rightNode(其实就是下一个最小的candidate), 并且一条龙stack叠上rightNode所有的left子孙.

Previous Notes:
用O(h)空间的做法：

理解binary search tree inorder traversal的规律：
   先找left.left.left ....left 到底，这里是加进stack.
   然后考虑parent,然后再right.

例如这题：
   stack里面top，也就是tree最左下角的node先考虑,取名rst.
   其实这个rst拿出来以后, 它也同时是最底层left null的parent，算考虑过了最底层的parent。
   最后就考虑最底层的parent.right, 也就是rst.right.

注意:
   next()其实有个while loop, 很可能是O(h).题目要求average O(1),所以也是okay的.


用O(1)空间的做法：不存stack, 时刻update current为最小值。

找下一个最小值,如果current有right child：   
   和用stack时的iteration类似,那么再找一遍current.right的left-most child,就是最小值了。
   
如果current没有right child:    
    那么就要找current node的右上parent, search in BinarySearchTree from root.

注意：
   一定要确保找到的parent满足parent.left == current.
   反而言之，如果current是parent的 right child, 那么下一轮就会重新process parent。
   但是有错:binary search tree里面parent是小于right child的，也就是在之前一步肯定visit过，如此便会死循环。




---

**1. [Flatten Nested List Iterator.java](https://github.com/awangdev/LintCode/blob/master/Java/Flatten%20Nested%20List%20Iterator.java)**      Level: Medium
      

方法1: 用queue, 把需要的item全部打出来
方法2: 用stack, 把需要的item先存一行, 每次打开子序列时候, 全部加回stack.



---

**2. [Implement Trie.java](https://github.com/awangdev/LintCode/blob/master/Java/Implement%20Trie.java)**      Level: Medium
      

Implement Tire, 也即是 Prefix Tree. 做三个function: insert, search, startWith

#### Trie
- HashMap构建Trie. Trie三个Method:
- 1. Inset: 加 word   
- 2. Search: 找word    
- 3. StartWith: 找prefix    

##### 特点
- 只有两条children的是binary tree. 那么多个children就是Trie
- 那么没有left/right pointer怎么找孩子？   
- 用HashMap，以child的label为Key，value就是child node。 HashMap走位   

##### 其他
- node里的char在这是optional. 只要在每个TrieNode里面用map存储向下分布的children就好了.  
- 另外有种题目，比如是跟其他种类的search相关，在结尾要return whole string，就可以在node里存一个up-to-this-point的String。

##### Previous Note
- 如果是遇到一个一个字查询的题，可以考虑一下。
- 构建TrieNode的时候要注意：如何找孩子？如果是个map的话，其实就挺好走位的。
- 而且，每个node里面的 char 或者string有时候用处不大，
- 可以为空。但是有些题目，比如在结尾要return一些什么String，就可以在end string那边存一个真的String。





---

**3. [Add and Search Word.java](https://github.com/awangdev/LintCode/blob/master/Java/Add%20and%20Search%20Word.java)**      Level: Medium
      

Trie结构, prefix tree的变形： '.'可以代替任何字符，那么就要iterate这个node所有的children.

节点里面有char, isEnd, HashMap<Character, TrieNode>   
Build trie = Insert word:没node就加，有node就移动。   
Search word:没有node就报错. 到结尾return true   

这题因为'.'可以代替任何possible的字符，没一种都是一个新的path，所以recursive做比较好些。    
(iterative就要queue了,麻烦点)



---

**4. [Data Stream Median.java](https://github.com/awangdev/LintCode/blob/master/Java/Data%20Stream%20Median.java)**      Level: Hard
      

#### 原理
- 把Input stream想成向上的山坡. 山坡中间那点，自然就是median.
- 前半段，作为maxHeap,关注点是PriorityQueue的峰点，也就是实际上的median.   
- 后半段，作为minHeap,正常的PriorityQueue。 开头是最小的。

#### 注意
- 这里要首先定好, 哪一个queue是多存一个element的. 这里选maxHeap: maxHeap.size() == minHeap.size() + 1 || minHeap.size()
- 必须先维护maxHeap里面有个元素, 否则null了会在比较大小时出问题.



---

**5. [Sliding Window Median.java](https://github.com/awangdev/LintCode/blob/master/Java/Sliding%20Window%20Median.java)**      Level: Hard
      

Median还是用min-heap 和 max-heap. Time(logN)
加/减: prioirtyQueue, log(n)
findMedian: O(1)

#### 思想
- 加一个数, 减一个数。
- 加减时看好，是从前面的maxheap里面抽，还是从后面的minHeap里面抽。
- 抽完balance一下

#### 注意
用maxHeap, minHeap时候, 习惯选择让maxHeap多一个数字:
左边的maxHeap总有 x+1或者x个数字
后边minHeap应该一直有x个数字



---

**6. [Min Stack.java](https://github.com/awangdev/LintCode/blob/master/Java/Min%20Stack.java)**      Level: Easy
      

双Stack：一个正常stack，另一个minStack存当下level最小值. 注意维护minStack的变化

另外. 如果要maxStack，也是类似做法



---

**7. [Implement Queue using Stacks.java](https://github.com/awangdev/LintCode/blob/master/Java/Implement%20Queue%20using%20Stacks.java)**      Level: Easy
      

#### 双Stack
画图, 知道最后maintain的stack是那个 reverseStack: pop(), peek(), empty() 都在这个stack上, 无需变换.
push()里面做stack和reverseStack的来回倾倒.
相比老的code, 在PUSH里面做倾倒, 更容易读.

#### Previous notes
双Stack. 一个是等于是queue，一个是backfillStack.
Tricky: 是在pop()和peek()的时候backfill, 并且要等到stack用完再backfill.
写一下例子就知道，如果提早backfill，stack.peek()就不是queue的head了.




---

**8. [Singleton.java](https://github.com/awangdev/LintCode/blob/master/Java/Singleton.java)**      Level: Easy
      

让一个class 是 singleton



---

**9. [Implement Stack using Queues.java](https://github.com/awangdev/LintCode/blob/master/Java/Implement%20Stack%20using%20Queues.java)**      Level: Easy
      

如题.

#### Queue, 倒水
- 两个Queue,交互倒水
- 用一个Temp做swap

##### 做法1
- 逻辑在push里面:
- 1. x 放q2。
- 2. q1全部offer/append到q2.
- 3. 用一个Temp做swap q1, q2.
- q1的头，就一直是最后加进去的值.


##### 做法2
- 逻辑在top()/pop()里, 每次换水，查看末尾项.




---

**10. [LRU Cache.java](https://github.com/awangdev/LintCode/blob/master/Java/LRU%20Cache.java)**      Level: Hard
      

#### Double Linked List
- 用了一个特别的双向的ListNode，有了head和tail，这样就大大加快了速度。     
- 主要加快的就是那个‘更新排位’的过程，找到item hashmap O(1), 做减法换位也都是O(1)
- Overall O(1)

##### 巧妙点
- 1. head和tail特别巧妙：除掉头和尾，和加上头和尾，就都特别快。    
- 2. 用双向的pointer: pre和next, 当需要除掉任何一个node的时候，只要知道要除掉哪一个，     
- 直接把node.pre和node.next耐心连起来就好了，node就自然而然的断开不要了。     
- 一旦知道怎么解决了，就不是很特别，并不是难写的算法:    
- moveToHead()    
- insertHead()    
- remove()      

#### O(n) 检查重复
- timeout method, 天真的来了一个O(n) 的解法，结果果然timeout.     
- 一个map<key,value>存数值。一个queue<key>来存排位。     
- 每次有更新，就把最新的放在末尾；每次超过capaticity,就把大头干掉。很简单嘛，但是跑起来太久，失败了。     




---




 
 
 
## DFS (54)
**0. [Nested List Weight Sum.java](https://github.com/awangdev/LintCode/blob/master/Java/Nested%20List%20Weight%20Sum.java)**      Level: Easy
      

给一串integers, list里面可能有nest list. 算总的sum. 规则, 如果是nested list, 每深一个depth, sum要乘以depth.

#### DFS
- 简单的处理nested structure, dfs增加depth.

#### BFS
- bfs, queue, 处理queue.size().



---

**1. [Same Tree.java](https://github.com/awangdev/LintCode/blob/master/Java/Same%20Tree.java)**      Level: Easy
      

给两个 binary tree, 看两个tree是否identical.

#### DFS
- DFS. 确定leaf条件, && with all dfs(sub1, sub2).
- 这里无论如何都要走过所有的node, 所以dfs更加合适, 好写.

#### BFS
- 两个queue存每个tree的所有current level node. Check equality, check queue size.
- Populate next level by nodes at current level.



---

**2. [Convert Sorted Array to Binary Search Tree.java](https://github.com/awangdev/LintCode/blob/master/Java/Convert%20Sorted%20Array%20to%20Binary%20Search%20Tree.java)**      Level: Easy
      

如题

#### DFS
- Binary Search Tree特点: 左边的node都比右边的node小. 
- 如果要height相差<1, 必须左右sub tree均分. 做DFS(num, start, end)
- 在每一个level, 找到中间点, 然后分割2办, 继续dfs
- Divide and Conquer



---

**3. [Construct Binary Tree from Inorder and Preorder Traversal.java](https://github.com/awangdev/LintCode/blob/master/Java/Construct%20Binary%20Tree%20from%20Inorder%20and%20Preorder%20Traversal.java)**      Level: Medium
      

如题

#### DFS
- 和Construct from Inorder && Postorder 想法一样。
- 写出Preorder和Inorder的字母例子，发现Preorder的开头总是这Level的root。依此写helper,注意处理index。
- 跟Convert Sorted Array to Binary Tree类似, 找到对应的index, 然后:
- node.left = dfs(...), node.right = dfs(...)
- Divide and Conquer



---

**4. [Balanced Binary Tree.java](https://github.com/awangdev/LintCode/blob/master/Java/Balanced%20Binary%20Tree.java)**      Level: Medium
      

给一个binary tree, 看是否是height-balanced

#### DFS
- DFS using depth marker: 每个depth都存一下。然后如果有不符合条件的，存为-1.
- 一旦有 <0 或者差值大于1， 就全部返回Integer.MIN_VALUE. Integer.MIN_VALUE比较极端, 确保结果的正确性。
- 最后比较返回结果是不是<0. 是<0，那就false.
- Traverse 整个tree, O(n)


#### DFS, maxDepth function
- Same concept as in 1, but cost more traversal efforts.



---

**5. [Populating Next Right Pointers in Each Node.java](https://github.com/awangdev/LintCode/blob/master/Java/Populating%20Next%20Right%20Pointers%20in%20Each%20Node.java)**      Level: Medium
      

给一个特殊的binary tree, treeNode里面有一个 next pointer.

写一个function, 把所有node都更同level的node 连在一起. 最右边的node.next = NULL

#### DFS
- 题目要求DFS. 想清楚了如何在DFS level把几种情况都考虑了, 写起来很简单.
- 对于一个root来说, 只有几个点可以顾忌到: root.left, root.right, root.next. 
- 想办法把这三个方向的点, 能连起来的都连起来:
- 1. node.left.next = node.right
- 2. If node.next != null, link node.right.next = node.next.left;
- 然后在dfs(root.left), dfs(root.right)

#### BFS
- 不和题意，用了queue space，与Input成正比。太大。
- BFS over Tree。 用Queue 和 queue.size()，老规矩。   
- process每层queue时, 注意把next pointer加上去就好. 



---

**6. [Validate Binary Search Tree.java](https://github.com/awangdev/LintCode/blob/master/Java/Validate%20Binary%20Search%20Tree.java)**      Level: Medium
      

如题, 验证是否是BST.

#### DFS
- 查看每个parent-child关系: leftchild < root < rightChild
- 方法: 把root.val 传下来作为 max 或者 min, 然后检查children

##### Note: 
- min/max需要时long type. 
- 如果题目真的给node.val = Integer.MAX_VALUE, 我们需要能够与之比较, long就可以.



---

**7. [Convert Sorted List to Binary Search Tree.java](https://github.com/awangdev/LintCode/blob/master/Java/Convert%20Sorted%20List%20to%20Binary%20Search%20Tree.java)**      Level: Medium
      

如题, 把一个sorted singly linked list 转换成一个 height balanced BST

#### DFS
- Divide and Conquer   
- 找到mid node
- 然后分割两半, 分别dfs做各自两个subtree: node.left,node.right
- 用长度来定位mid, 每次找中间点做root, 然后前半段, 后半段分别dfs with length.
- 用快慢pointer 找到mid. Better: 不用traverse entire linked list

#### Details
- slowPointer = node;
- fastPointer = node.next;
- 然后把root = mid.next     
- 然后开始sortedListToBST(mid.next.next); //后半段    
- mid.next = null;//非常重要，要把后面拍过序的断掉    
- sortedListToBST(head); //从头开始的前半段     
- 最后root.left, root.right merge一下。   



---

**8. [Flatten Binary Tree to Linked List.java](https://github.com/awangdev/LintCode/blob/master/Java/Flatten%20Binary%20Tree%20to%20Linked%20List.java)**      Level: Medium
      

给一个binary tree, 把tree做成 linked list的形式, in-place.

#### DFS
- 分析题意后, 按照题意: Flatten the tree, no extra space.
1. reserve right child
2. DFS flatten部分
3. 移花接木
4. flatten 剩下的.

##### 注意
- 顺序一定要清楚, 不能写错, 写几个example可以看出来
- 移动的那些node, 要把node.left = null, 清扫干净



---

**9. [Binary Tree Paths.java](https://github.com/awangdev/LintCode/blob/master/Java/Binary%20Tree%20Paths.java)**      Level: Easy
      

给一个binary tree, 返回所有root-to-leaf path

#### DFS
- Recursive:分叉. dfs.

#### Iterative
- Iterative, 非递归练习了一下
- 因为要每次切短list, 所以再加了一个Stack 来存level
- 单这道题用dfs更简单, 因为找的就是从头到尾的path, 是dfs的pattern




---

**10. [Clone Graph.java](https://github.com/awangdev/LintCode/blob/master/Java/Clone%20Graph.java)**      Level: Medium
      

给一个graph node, 每个node有list of neighbors. 复制整个graph, return new head node.

#### 思想
- Use HashMap to mark cloned nodes.    
- 先能复制多少Node复制多少. 然后把neighbor 加上

#### DFS
- copy the node
- Mark 'added' using map(old, new)
- for loop on the each one of the neighbors: map copy, record in map, and further dfs
- once dfs completes, add newNeighbor as neighbor of the new node (get to it via map)
- 主要思想是: 一旦复制过了, 不必要重新复制

#### BFS
_ Copy the root node, then copy all the neighbors. 
_ Mark copied node in map.
_ Use queue to contain the newly added neighbors. Need to work on them in the future.

#### Note
initialize map with (node, newNode)



---

**11. [Number of Islands.java](https://github.com/awangdev/LintCode/blob/master/Java/Number%20of%20Islands.java)**      Level: Medium
      

给一个2Dmatrix, 里面是1和0, 找#of island.


#### DFS
- top level 有一个 double for loop, 查看每一个点.
- 每当遇到1, count+1, 然后DFS helper function 把每个跟这个当下island 相关的都Mark成 '0'
- 这样确保每个visited 过得island都被清扫干净

#### Union Find
- 可以用union-find， 就像Number of island II 一样。
- 只不过这个不Return list, 而只是# of islands
- 记住UnionFind的模板和几个变化(Connecting Graph I, II, III), 最后归总的代码写起来就比较简单.



---

**12. [Graph Valid Tree.java](https://github.com/awangdev/LintCode/blob/master/Java/Graph%20Valid%20Tree.java)**      Level: Review
      

M 

给一个数字n代表n nodes, marked from 1 ~ n, 和一串undirected edge int[][]. 检查这些edge是否能合成一个 valid tree

#### Union Find
- 复习Union-Find的另外一个种形式, track union size
- 题目类型：查找2个元素是不是在一个union里面。如果不在，false. 如果在，那就合并成一个set,共享parent.   
- 存储的关键都是：元素相对的index上存着他的root parent.    
- 注意: 结尾要检查, 是否只剩下1个union: Tree必须连接到所有给出的node.
- 另一个union-find, 用hashmap的:
- http://www.lintcode.com/en/problem/find-the-weak-connected-component-in-the-directed-graph/

#### DFS
- (还没做, 可以写一写)
- 检查: 1. 是否有cycle, 2. 是否所有的node全部链接起来

#### BFS
- (还没做, 可以写一写)
- 也是检查: 1. 是否有cycle, 2. 是否所有的node全部链接起来



---

**13. [Surrounded Regions.java](https://github.com/awangdev/LintCode/blob/master/Java/Surrounded%20Regions.java)**      Level: Review
      

给一个2D board, 里面是 'X' 和 'O'. 把所有被X包围的area都涂成'X'. 

从四个边的edge出发, 像感染僵尸病毒一样扩散, 把靠边的node全部mark, 然后将还是'O'的改成X, 最后回复marks -> 'O'

#### Union Find
- UnionFind里面这次用到了一个rank的概念, 需要review. rank[] 也就是在tracking每一个node所在union的size.
- 目的是: always并到大的union里面
- note: 将2D coordinate (x,y) 转换成1D: index = x * n + y

#### DFS
- TODO

#### BFS
- TODO




---

**14. [Word Search II.java](https://github.com/awangdev/LintCode/blob/master/Java/Word%20Search%20II.java)**      Level: Hard
      

给一串words, 还有一个2D character matrix. 找到所有可以形成的words. 条件: 2D matrix 只可以相邻走位.

#### Trie, DFS
- 相比之前的implementation, 有一些地方可以优化:
- 1. Backtracking时候, 在board[][] 上面mark就可以, 不需要开一个visited[][]
- 2. 不需要implement trie的所有方程, 用不到: 这里只需要insert.
- 普通的trie题目会让你search a word, 但是这里是用一个board, 看board的每一个字母能不能走出个Word.
- 也就是: 这里的search是自己手动写, 不是传统的trie search() funcombination
- 3. TrieNode里面存在 end的时候存string word, 表示到底. 用完了 word = null, 刚好截断重复查找的问题.

##### 关于Trie
- Build Trie with target words: insert, search, startWith.    
- 依然要对board matrix做DFS。
- no for loop on words. 直接对board DFS:   
- 每一层,都会有个up-to-this-point的string. 在Trie里面check它是不是存在。以此判断。   
- 若不存在，就不必继续DFS下去了。
- Trie solution time complexity, much better:      
- build Trie:   n * wordMaxLength
- search: boardWidth * boardHeight * (4^wordMaxLength + wordMaxLength[Trie Search])


#### Regular DFS
- for loop on words: inside, do board DFS based on each word.     
- Time cpmplexity: word[].length * boardWidth * boardHeight * (4^wordMaxLength)

#### Previous Notes
- Big improvement: use boolean visited on TrieNode!     
- 不要用rst.contains(...), 因为这个是O(n) 在leetcode还是会timeout（lintcode竟然可以pass）!    
- 在Trie search() method 里面，凡是visit过的，mark一下。  





---

**15. [Expression Expand.java](https://github.com/awangdev/LintCode/blob/master/Java/Expression%20Expand.java)**      Level: Medium
      

给一个expression string. 里面包括数字, 字母, 括号. 其中数字代表括号里面的内容重复几次.

括号里面可以是String, 也可能是expression.

目的: 把expression展开成一个正常的String.

#### DFS
- 与Stack时需要考虑的一些function类似. 特别之处: **检查[ ]的结尾**
- 因为DFS时候, 括号里的substring会被保留着进入下一个level, 所以我们在base level要keep track of substring.
- 用int paren 来track 括号的开合, 当paren再次==0的时候 找到closure ']'

#### Stack
- Stack存 [ ] 里面的内容, detect 括号开头结尾: 结尾时process inner string
- 有很多需要注意的细节才能做对:
- Stack<Object> 也可以用, 每个地方要注意 cast. 存进去的需要是Object: String, Integer
- 几个 type check: instanceof String, Character.isDigit(x), Integer.valueOf(int num)
- 出结果时候, 不能轻易 sb.reverse().toString(): sb.reverse() 翻转了整个连在一起的string, 错.
- 用另一个Stack<String>作为buffer, 先把stack里面的内容倒出来 (pure), 但是每个item里面顺序不变.
- 最后再从buffer里面倒进StringBuffer.




---

**16. [Find Peak Element II.java](https://github.com/awangdev/LintCode/blob/master/Java/Find%20Peak%20Element%20II.java)**      Level: Hard
      

2Dmatrix, 里面的value有一些递增, 递减的特点(细节比较长, 看原题). 目标是找到peak element

#### DFS

##### 基本原理
- 我们不可能一口气准确定位(x,y), 但是我们可以再一个row/col里面, 找到1D array的 peak.
- 根据这个点, 再往剩下两个方向移动
- 1. 在中间的一行i=midX, 找到peak所在的y.
- 2. 在中间的一列j=midY, 找到peak所在的x. (有可能强势override之前找到的y, 也就是放弃那一行的peak, 在midY上找peak)
- 3. 根据 (x,y) 的4个neighbor check (x,y)是不是 peak, 如果不是, 像更高的位置移动一格
- 4. 根据之前算的 midX, midY 把board分成4个象限, 在每一份里面再继续找
- 这个题目LintCode不给做了, 所以思路对的, 但是解答还没有再次验证.

##### 剪枝/切分象限
- 每次只是找到一个row/col里面的peak而已!
- 找到这个点, 就等于把board切成了两半.
- 然后, 再跟剩下的相邻的两个位置比较, 就知道了哪里更大, 就去哪里找peak, 也就是又切了第二刀.
- 切第二刀的时候, 也要把(x, y) 移到需要取的象限. 进行DFS
- 根据mid row 切割: 
- http://www.jiuzhang.com/solution/find-peak-element-ii/#tag-highlight-lang-java
- http://courses.csail.mit.edu/6.006/spring11/lectures/lec02.pdf

##### 时间复杂度
- 每一个level都减一半
- T(n) = n + T(n/2) = n + n/2 + n/4 + ... + 1 = n(1 + 1/2 + .... + 1/n) = 2n = O(n)

#### Binary Search
- TODO
- O(nLogN)



---

**17. [Longest Increasing Path in a Matrix.java](https://github.com/awangdev/LintCode/blob/master/Java/Longest%20Increasing%20Path%20in%20a%20Matrix.java)**      Level: Hard
      

m x n 的matrix, 找最长增序的序列长度. 这里默认连续的序列.

- 接成圈是不行的, 所以visit过得 (x,y)就不能再去了.
- 斜角方向不能走, 只能走上下左右
- 无法按照坐标DP来做, 因为计算顺序4个方向都可以走.
- 最终要visit所有node, 所以用DFS搜索比较合适.

#### DFS, Memoization
- DFS太多重复计算; memoization (dp[][], visited[][]) 省去了重复计算
- initialize dp[x][y] = 1, (x,y) 自己也算path里的一格
- dfs(matrix, x, y): 每次检查(x,y)的4个neighbor (nx, ny), 如果他们到(x,y)是递增, 那么就考虑和比较:
- Maht.max(dp[x][y], dp[nx][ny] + 1); where dp[n][ny] = dfs(matrix, nx, ny)
- top level: O(mn), 尝试从每一个 (x,y) 出发
- O(m * n * k), where k is the longest path

#### Topological sort
还没有做



---

**18. [Course Schedule.java](https://github.com/awangdev/LintCode/blob/master/Java/Course%20Schedule.java)**      Level: Medium
      

- 一堆课用int[2] pair 来表示. [1, 0] 表示要上课1的话, 必须先把课0上了. 
- 每一个数字都是一个ndoe, 题目问是否能把所有的课排了
- input是 numOfCourses, 还有这个prerequisites [[]]

#### Topological Sort
- 给一个graph of nodes
- 至关重要: 用`List[] edges; edges[i] = new ArrayList<>();` 来表示graph: 就是每个node, to all its neighbors
- 目标是根据edge 的 direction, 把这个graph 里面的 node sort 一个list
- 如果有cycle, 这个item就不会被放在最后的list 里面. 
- 比如: 如果两个课互相是dependency, 就变成了cyclic dependency, 这样不好.


#### BFS
- Kahn algorithem:
- 先build一个graph map: <node, list of nodes >; or `List[] edges; edges[i] = new ArrayList<>();`
- count in-degree: inDegree就是每个node上面, 有多少个走进来的edge?
- 那些没有 in-coming-edge的, indegree 其实就 等于 0, 那么他们就应该在final result list里面
- 对这些 indegree == 0 的 nodes BFS, add to queue.
- 模拟visit每个ndoe, 如果visit过了, 这个node上的 indegree--, 然后如果最终 indegree == 0, 这个node就成功进入final list.

##### Indegree 原理
- Note: 如果有cycle, indegree是不会变成0的, 它也无法进入最终list. 
- indegree是周围的node到我这里的次数count. 
- 如果周围所有node的连线, 都意义切除后, 我的indegree还不等于0, 那么肯定有某些node间接地有重复连线, 也就是有cycle

#### DFS
- 这道题没有要求作出final list, 相对简单, 只要visit每个nodes, 最后确认没有cycle就好了
- 用 visited int[] 来确认是否有cycle. 1 代表 paretNode visited, -1 代表在DFS上一行的标记
- 如果遇到-1, 说明这个node在上一级或者以上的同一个dfs path里面已经走过, 那么证明有cycle, return false.
- 走完一个node的所有neighbor, 都没有fail, 那么backtracking, set visited[i] = 1
- 真的topo sort会在DFS的底端, 把record放进一个stack, 最后reverse, 就是真的sort order.

#### Notes:
- 还有 List[] arrayOfList = new ArrayList[]; 这样的操作啊, 代替了map<integer, integerList>

#### Previous notes
有点绕，但是做过一次就明白一点。    
是topological sort的题目。一般都是给有dependency的东西排序。    

最终都会到一个sink node， 再不会有向后的dependency, 在那个点截止。    
我就已这样子的点为map的key, 然后value是以这个node为prerequisite的 list of courses.    

画个图的话，prerequisite都是指向那个sink node， 然后我们在组成map的时候，都是从sink node 发散回来到dependent nodes.    

在DFS里面，我们是反向的， 然后，最先完全visited的那个node, 肯定是最左边的node了，它被mark的seq也是最高的。    

而我们的sink node，当它所有的支线都visit完了，seq肯定都已经减到最小了，也就是0，它就是第一个被visit的。   


最终结果：
每个有pre-requisit的node都trace上去（自底向上），并且都没有发现cycle.也就说明schedule可以用了。



---

**19. [Course Schedule II.java](https://github.com/awangdev/LintCode/blob/master/Java/Course%20Schedule%20II.java)**      Level: Medium
      

- 一堆课用int[2] pair 来表示. [1, 0] 表示要上课1的话, 必须先把课0上了. 
- 每一个数字都是一个ndoe, 题目求这个最后排好的课的list
- 如果排不好, 就给个空就好
- input是 numOfCourses, 还有这个prerequisites [[]]
- 做法跟Course Schedule I 非常像, 可以参考.

#### Topological Sort, Indegree, BFS
- 用`List[] edges; edges[i] = new ArrayList<>();` 来表示graph: 就是每个node, to all its neighbors
- 每个没有 inDegree==0 node, 都是可以加进 final list里面的. 比如一开始找到的那些 inDegree = 0的 node
- 注意, 如果 prerequisites = [], 那么就是说这些课都independent, 开个int[0 ~ n-1]的数组并赋值就好.
- 如果有cycle, 严格意义上就做不了topological sort, 也无法涵盖所有nodes,  那么return [ ]

#### DFS
- 根据 Course Schedule 里面的DFS 修改
- 维持visited int[]全局变量
- 维持sortedList int[] 全局变量, 注意加进去的时候是 add(0, node) 加在开头这样
- 每次到一个node的children全部DFS走完之后, 就可以把他加进final list里面
- 如果有cycle, 也就是dfs return false的时候, 这个题目判定排课失败, return new int[] { }



---

**20. [Alien Dictionary.java](https://github.com/awangdev/LintCode/blob/master/Java/Alien%20Dictionary.java)**      Level: Hard
      

给一个 array of strings: 假如这个array是按照一个新的字母排序表(alien dictionary)排出来的, 需要找到这个字母排序.

有可能有多重排序的方法, 给出一种就可以.

#### Graph
- 本质: 上下两行string, 相对应的相同的index上, 如果字母不同, 就说明排在第一行的字母在字母表里更领先
- 把 string array 变成topological sort的 graph: `map<char, list<char>>`
- 也可以`List[26] edges` (Course Schedule problem)
- Build edges: find char diff between two row, and store the order indication into graph
- 注意: indegree 永远是反向的 (跟 node to neighbors 相反的方式建立)

#### BFS
- topological sort 本身很好写, 但是要在题目中先了解到字母排序的本质
- 其实上面这个排序的本质很好想, 但是把它具体化成构建graph的代码, 会稍微有点难想到
- 算indegree, 然后用 BFS 来找到那些 inDegree == 0的 node
- 最先inDegree == 0的node, 就排在字母表前面.
- 下面的解法, 用了Graph: map<Character, List<Character>>, 而不是 List[26], 其实更加试用超过26个字母的dictionary.

#### DFS
- 跟BFS建立 grpah 的过程一模一样
- DFS的不同在于: 用visited map 来标记走过的地方
- 走到leaf的时候, add to result: 但因为走到了底才add, 最终的顺序应该颠倒 (或者, sb.insert(0, x) 直接用颠倒的顺序add)



---

**21. [Binary Tree Preorder Traversal.java](https://github.com/awangdev/LintCode/blob/master/Java/Binary%20Tree%20Preorder%20Traversal.java)**      Level: Easy
      

#### Recursive
- 加root, left, then right. Obvious
- Divide and conquer
- 其实也不需要helper function

#### Iterative
- 先加root, 然后push上需要末尾process的在stack垫底(root.right), 然后push root.left
- Stack: push curr, push right, push left.   



---

**22. [House Robber III.java](https://github.com/awangdev/LintCode/blob/master/Java/House%20Robber%20III.java)**      Level: Medium
      

Houses被arrange成了binary tree, 规则还是一样, 连续相连的房子不能同时抄.

求Binary Tree neighbor max 能抄多少.

#### DFS
- 判断当下的node是否被采用，用一个boolean来表示. 
- 如果curr node被采用，那么下面的child一定不能被采用.
- 如果curr node不被采用，那么下面的children有可能被采用，但也可能略过，所以这里用Math.max() 比较一下两种可能有的dfs结果。
- dfs重复计算:每个root都有4种dive in的可能性, 假设level高度是h, 那么时间O(4^(h)), where h = logN, 也就是O(n^2)

#### DP, DFS
- 并不是单纯的DP, 是在发现DFS很费劲后, 想能不能代替一些重复计算?
- 基本思想是dfs解法一致: 取root找最大值, 或者不取root找最大值
- 在root上DFS, 不在dfs进入前分叉; 每一个level按照状态来存相应的值: dp[0] root not picked, dp[1] root picked.
- Optimization: DP里面, 一口气找leftDP[]会dfs到最底层, 然后自下向上做计算
- 这个过程里面, 因为没有在外面给dfs()分叉, 计算就不会重叠, 再也不用回去visit most-left-leaf了, 算过一遍就完事.
- 然而, 普通没有dp的dfs, 在算完visited的情况下的dfs, 还要重新dfs一遍!visited的情况.
- Space O(h), time O(n), 或者说是O(2^h), where h = log(n)

#### DP 特点
- 不为状态而分叉dfs
- 把不同状态model成dp
- 每一个dfs都return一个based on status的 dp array.
- 等于一次性dfs计算到底, 然后back track, 计算顶部的每一层.
- DP 并不一定要是以n为base的. 也可以是局部的去memorize状态->value.



---

**23. [Palindrome Partitioning.java](https://github.com/awangdev/LintCode/blob/master/Java/Palindrome%20Partitioning.java)**      Level: Medium
      

给个string s, partition(分段)后, 要确保每个partition都是palindrome. 

求所有partition palindrome组合. `list<list<string>>`

#### DFS
- 在遍历str的时候，考虑从每个curr spot 到 str 结尾，是能有多少种palindorme?
- 那就从curr spot当个字符开始算，开始back tracing.
- 如果所选不是palindrome， 那move on.
- 若所选的确是palindrome,　加到path里面，DFS去下个level，等遍历到了结尾，这就产生了一种分割成palindrome的串。
- 每次DFS结尾，要把这一层加的所选palindrome删掉，backtracking嘛

#### Optimization
- 可以再每一个dfs level 算 isPalindrome(S), 但是可以先把 boolean[][] isPalin 算出来, 每次O(1) 来用
- 注意: isPalin[i][j] 是 inclusive的, 所以用的时候要认准坐标
- Overall Space O(n^2): 存 isPlain[][]
- Time O(n!), 每一层的for loop spawn n * (n - 1) * (n - 2)



---

**24. [Flip Game II.java](https://github.com/awangdev/LintCode/blob/master/Java/Flip%20Game%20II.java)**      Level: Review
      

String 只包含 + , - 两个符号. 两个人轮流把consecutive连续的`++`, 翻转成 `--`.

如果其中一个人再无法翻转了, 另一个人就赢. 求: 给出string, 先手是否能赢.

#### Backtracking
- curr player 每走一步, 就生成一种新的局面, dfs on this
- 等到dfs结束, 不论成功与否, 都要backtracking
- curr level: 把"++" 改成 "--"; backtrack的时候, 改回 '--'
- 换成boolean[] 比 string/stringBuilder要快很多, 因为不需要重新生成string.
- ++ 可以走 (n - 1)个位置: 
- T(N) = T(1) + T(2) + T(3) + ... + T(N-2) + T(N - 1)
- => T(N) = 2T(N-1) = 2 * 2 * T(N - 2) = ... = (2^n)T(1) = O(2 ^ n)

##### iterate based on "++"
- 做一个String s的 replica: string or stringBuilder
- 每次dfs后, 然后更替里面的字符 "+" => "-"
- 目的只是Mark已经用过的index
- 真正的dfs 还是在 original input string s 身上展开
- 每次都重新生成substring, 并不是很efficient

##### Game theory
- 保证p1能胜利，就必须保持所有p2的move都不能赢
- 或者说, 在知道棋的所有情况时, 只要p2有一种路子会输, p1就一定能走对路能赢.
- 同时，p1只要在可走的Move里面，有一个move可以赢就足够了。
- p1: player1, p2: player2

#### O(N^2) 的 DP
- 需要Game Theory的功底, Nim game. https://www.jiuzhang.com/qa/941/
- http://www.1point3acres.com/bbs/thread-137953-1-1.html



---

**25. [Expression Evaluation.java](https://github.com/awangdev/LintCode/blob/master/Java/Expression%20Evaluation.java)**      Level: Hard
      

给一个公式 expression, array of strings, 然后evaluate expression 结果.

#### DFS on Expression Tree
- 计算 expression 的值: 1. 建造 expression tree. 2. DFS计算结果
- Expression Tree: Minimum Binary Tree (https://lintcode.com/en/problem/expression-tree-build/)
- build好Min Tree以后，做PostTraversal. 
- Divde and Conquer: 先recursively找到 left和right的大小， 然后evaluate中间的符号
- Time, Space O(n), n = # expression nodes

### Note
- 1. Handle数字时，若left&&right Child全Null,那必定是我们weight最大的数字node了。   
- 2. 若有个child是null,那就return另外一个node。    
- 3. prevent Integer overflow　during operation:过程中用个Long，最后结局在cast back to int.



---

**26. [Convert Expression to Polish Notation.java](https://github.com/awangdev/LintCode/blob/master/Java/Convert%20Expression%20to%20Polish%20Notation.java)**      Level: Hard
      

给一串字符, 用来表示公式expression. 把这个expression转换成 Polish Notation (PN).

#### Expression Tree
- Expression Tree: Minimum Binary Tree (https://lintcode.com/en/problem/expression-tree-build/)
- 根据题意做出Expression Tree出来以后: 来个Pre-order-traversal 就能记录下 Polish Notation
- 本题没有给'ExpressionTreeNode', 所以把TreeNode就当做成我们需要的node, 里面扩展成有left/right child就可以了.
- Note: label需要是String. 虽然 Operator是长度为1的char, 但是数字可为多位



---

**27. [Convert Expression to Reverse Polish Notation.java](https://github.com/awangdev/LintCode/blob/master/Java/Convert%20Expression%20to%20Reverse%20Polish%20Notation.java)**      Level: Hard
      

给一串字符, 用来表示公式expression. 把这个expression转换成 Reverse Polish Notation (RPN).

#### Expression Tree
- Expression Tree: Minimum Binary Tree (https://lintcode.com/en/problem/expression-tree-build/)
- 根据题意做出Expression Tree出来以后: 来个Post-order-traversal 就能记录下 Reverse Polish Notation
- 本题没有给'ExpressionTreeNode', 所以把TreeNode就当做成我们需要的node, 里面扩展成有left/right child就可以了.



---

**28. [Maximum Subarray.java](https://github.com/awangdev/LintCode/blob/master/Java/Maximum%20Subarray.java)**      Level: Easy
      

给一串数组, 找数组中间 subarray 数字之和的最大值

#### Sequence DP
- dp[i]: 前i个element, 包括element i 在内的 continous subsequence 的最大sum是多少?
- 因为continous sequence, 所以不满足条件的时候, 会断: track overall max,
- init dp[0] = 0; max = MIN_VALUE 因为有负数
- Time, space O(n)
- Rolling array, space O(1)

#### Divide and Conquer
- 找一个mid piont, 考虑3种情况: 只要左边, 只要右边, cross-mid
- left/rigth 的case, 直接 dfs
- corss-mid case: continuous sum max from left + continous sum max from right + mid
- continuous sum max from one direction:


---

**29. [Invert Binary Tree.java](https://github.com/awangdev/LintCode/blob/master/Java/Invert%20Binary%20Tree.java)**      Level: Easy
      

#### DFS
- 简单处理swap
- recursively swap children

#### BFS
- BFS with Queue
- 每次process一个node, swap children; 然后把child加进queue里面
- 直到queue process完



---

**30. [Maximum Depth of Binary Tree.java](https://github.com/awangdev/LintCode/blob/master/Java/Maximum%20Depth%20of%20Binary%20Tree.java)**      Level: Easy
      

给一个binary tree, 找最深depth

#### DFS
- 这里要走过所有的node, 所以dfs非常合适
- Divide and conquer. 
- 维持一个最大值: Math.max(maxDepth(root.left), maxDepth(root.right)) + 1;
- 注意check root == null



---

**31. [Minimum Depth of Binary Tree.java](https://github.com/awangdev/LintCode/blob/master/Java/Minimum%20Depth%20of%20Binary%20Tree.java)**      Level: Easy
      

#### DFS
- Divide and Conquery一个最小值. 
- 注意处理Leaf的null: null leaf 出现的时候, 就忽略这个leaf, 直接return算有leaf
- 另一种count的方法: 用Integer.MAX_VALUE代替 null leaf，这样可以避免错误counting. (不能直接recursive)
- 这个无论如何都要走所有node, 所以dfs应该比较适合.

#### BFS
- 还没做



---

**32. [Symmetric Tree.java](https://github.com/awangdev/LintCode/blob/master/Java/Symmetric%20Tree.java)**      Level: Easy
      

检查tree是否symmetric

注意Symmetric Binary Tree的例子和定义: 是镜面一样的对称. 并不是说左右两个sub-tree相等。

#### DFS
- Recursively check symmetrically相对应的Node.  
- 每个node的children都和镜面另外一边相对的node的children刚好成镜面反射位置。

#### Stack
- stack1: 左手边sub-tree先加left, 再加right child; 
- stack2: 右手边sub-tree先加right child, 再加left child。   
- process时，若symmetric，所有stack里面出来的node会一一对应。



---

**33. [Tweaked Identical Binary Tree.java](https://github.com/awangdev/LintCode/blob/master/Java/Tweaked%20Identical%20Binary%20Tree.java)**      Level: Easy
      

检查binary tree是否 identical. 

特点: subtree如果是有旋转的, 只要tree node value相等, 就可以算是identical

#### DFS
- 在DFS的基础上, 比对左左,左右,右左,右右



---

**34. [Merge Two Binary Trees.java](https://github.com/awangdev/LintCode/blob/master/Java/Merge%20Two%20Binary%20Trees.java)**      Level: Easy
      

#### DFS
- 基础binary tree traversal. 注意对null child的判断



---

**35. [Subtree.java](https://github.com/awangdev/LintCode/blob/master/Java/Subtree.java)**      Level: Easy
      

给一个binary tree s, 和一个binary tree t, 检查t是不是s的subtree.

#### DFS
- 跟 identical binary tree的写法很像
- 只有 current s.val = t.val 的时候才需要compare same tree.
- 其他情况, 继续recursively isSubtree
- 注意：即使找到T1 == T2, 但很可能只是数字相同（这里不是binary search tree!!）, 而children不同
- 所以同时要继续recursively isSubtree(T1.left, T2) ...etc.



---

**36. [Lowest Common Ancestor of a Binary Tree.java](https://github.com/awangdev/LintCode/blob/master/Java/Lowest%20Common%20Ancestor%20of%20a%20Binary%20Tree.java)**      Level: Medium
      

给一个Binary Tree root, 以及两个node p, q. 找 p 和 q 的 lowest common ancestor

#### DFS
- 因为是 binary tree, 所以直接盲目搜索搜索path不efficient. 巧用DFS来找每一个node的common ancestor
- 当root == null或者 p q 任何一个在findLCA底部被找到了(root== A || root == B)，那么就return 这个root.     
- 三种情况:
- 1. A,B都找到，那么这个level的node就是其中一层的ancestor: 其实，最先recursively return到的那个，就是最底的LCA parent.   
- 2. A 或者 B 找到，那就还没有公共parent, return 非null得那个。   
- 3. A B 都null, 那就找错了没有呗, return null
- Worst case, visit all nodes to find p q at last level, last two leaves: time/space O(n)



---

**37. [Lowest Common Ancestor of a Binary Search Tree.java](https://github.com/awangdev/LintCode/blob/master/Java/Lowest%20Common%20Ancestor%20of%20a%20Binary%20Search%20Tree.java)**      Level: Medium
      

给 binary search tree root, q node, p node. 找到p q 的lowest common ancestor

#### Find path with BST
- 利用 BST 的性质，可以直接搜到target node，而做成两个长度不一定相等的list
- 然后很简单找到LCA 

#### DFS
- Brutly寻找p和q的common ancestor, 然后recursively drive left/right
- 非常巧妙, 但是也比较局限; 稍微变条件, 就很难recursive.
- 几种情况:
- 1. one of p, q 在leaf, 那么此时的root其实就是lowest common ancestor
- 2. 如果p, q 在root的左右两边, 这就是分叉口, 那么root就是lowest common ancestor
- 3. 如果p,q 在root的同一边 (左,右), 那么继续dfs



---

**38. [Binary Tree Level Order Traversal.java](https://github.com/awangdev/LintCode/blob/master/Java/Binary%20Tree%20Level%20Order%20Traversal.java)**      Level: Medium
      

如题.

#### BFS
- 最普通,Non-recursive: BFS, queue, 用个queue.size()来end for loop:换行。   
- 或者用两个queue. 当常规queue empty，把backup queue贴上去

#### DFS
- 每个level都应该有个ArrayList. 那么用一个int level来查看：是否每一层都有了相应的ArrayList。   
- 如果没有，就加上一层。    
- 之后每次都通过DFS在相应的level上面加数字。




---

**39. [Binary Tree Longest Consecutive Sequence II.java](https://github.com/awangdev/LintCode/blob/master/Java/Binary%20Tree%20Longest%20Consecutive%20Sequence%20II.java)**      Level: Medium
      

找到binary tree 里的最长 consecutive sequence. Sequence可以递增递减, Sequence顺序可以回溯parent.

#### DFS
- Similar to Binary Tree Longest Consecutive Sequence I
- 只不过可以递增递减, 还有连接上parent的方向.
- 对于任何一个节点, 都可能: 
- 1. 自己跟两个child链接, 成为一个sequence
- 2. 左边孩子, 右边孩子各自是一个consecutive sequence, 但是不跟root相连
- main function 一开始就divide成这三份, 然后dfs
- dfs take diff == 1, diff == -1, 来做递增递减的校对.
- dfs rules:
- 1. if node == null, leaf depth = 0
- 2. if not consecutive, reset the depth = 0 (same for both left child, and right child)
- 3. compare the leftDepth && rightDepth to find the maximum
- 4. diff is the same in the same dfs loop to maintain consistant increase/decrease

##### 注意
- dfs的结果很可能是0, 如果没有任何结果, 那么上一层的caller depth = dfs() + 1 = 1
- 那么回归到root, dfs的结果很可能就是1.
- 可能会问: 那么在tree里面的partial sequence (不连接到root)的被忽略了?
- 这里 `longestConsecutive(root.left)` 就很重要了
- 这一步特地忽略掉了root, 然后走下去一层: 因为是recursive, 所以还会继续divde && conquer
- 最后, 任何一层的孩子都会被照顾到.



---

**40. [Binary Tree Maximum Path Sum.java](https://github.com/awangdev/LintCode/blob/master/Java/Binary%20Tree%20Maximum%20Path%20Sum.java)**      Level: Hard
      

找max path sum,  可以从任意treeNode 到任意 treeNode.

#### DFS, PathSum object
- that just solves everything


---

**41. [Path Sum.java](https://github.com/awangdev/LintCode/blob/master/Java/Path%20Sum.java)**      Level: Easy
      

给一个inputSum, 然后dfs, 找到是否有一条path, 得出的path sum 跟 inputSum 一样.

#### DFS
- 确定好结尾的条件: is leaf && val == sum
- 每一层减掉node.val, 然后dfs.
- 写一写: root == null => false 对parent nodes的影响. 这里发现没影响, 所以可以简化成用1个functionDFS.




---

**42. [Path Sum II.java](https://github.com/awangdev/LintCode/blob/master/Java/Path%20Sum%20II.java)**      Level: Easy
      

给一个inputSum, 然后dfs, 找到所有path, 满足: path sum 跟 inputSum 一样.

#### DFS, Backtracking
- 用remaining sum 来检测是否满足 input path sum 条件
- 满足的时候add to result list
- 两种backtracking:
- 1. backtrack 当下node, 加进list, 然后dfs. dfs结束后删掉之前加进去的元素. 非常clean.
- 2. backtrack 下一个dfs level增加的value. dfs return 之后, 删掉list里面的末尾元素: 但是删掉的dfs余下的value.
- 第一种backtrack更加好掌握.

#### Previous Notes:
- Binary Tree的一个基本题: 找到所有满足条件的path
- 遍历到底，比较sum vs. target
- 注意divide的情况。要把遍历的例子写写



---

**43. [Path Sum III.java](https://github.com/awangdev/LintCode/blob/master/Java/Path%20Sum%20III.java)**      Level: Easy
      

count所有存在的 path sum == target sum. 可以从任意点开始. 但是只能parent -> child .

#### DFS
- 对所给的input sum 做减法, 知道 sum 达到一个目标值截止
- 因为可以从任意点开始, 所以当sum达标时候, 需要继续recursive, 从而找到所有情况 (有正负数, sum可能继续增加/减少)
- 经典的 helper dfs recursive + self recursive
- 1. helper dfs recursive 处理包括root的情况
- 2. self recursive 来引领  skip root的情况.

#### 特点
- 与 `Binary Tree Longest Consecutive Sequence II` 在recursive的做法上很相似: 
- 利用dfs做包括root的recursive computation
- 利用这个function自己, 做不包括root的recursive computation



---

**44. [Path Sum IV.java](https://github.com/awangdev/LintCode/blob/master/Java/Path%20Sum%20IV.java)**      Level: Medium
      

给一串3-digit 的数组. 每个数字的表达一个TreeNode, 3 digit分别代表: depth.position.value

这串数字已经从小到大排列. 求: 所有可能的 root->leaf path 的所有可能的 path sum 总和. 

#### DFS, Hash Map
- 因为前两个digit可以locate一个node, 所以可以把前两个digit作为key, 定位node.
- 特点: 比如考虑root, 有 n 个leaf, 就会加 n 遍root, 因为有 n 个 unique path嘛.
- 对于每一个node也是一样: 只要有child, 到这个node位置的以上path sum 就要被重加一次.
- format: depth.position.value. (on same level, position may not be continuous)
- approach: map each number into: <depth.position, value>, and dfs. 
- Start from dfs(map, rootKey, sum):
- 1. add node value to sum
- 2. compute potential child.
- 3. check child existence, if exist, add sum to result (for both left/right child). Check existence using the map.
= 4. also, if child exist, dfs into next level



---

**45. [Combinations.java](https://github.com/awangdev/LintCode/blob/master/Java/Combinations.java)**      Level: Medium
      

Given two integers n and k, return all possible combinations of k numbers out of 1 ... n.

#### DFS, Backtracking
- for loop, recursive (dfs).
- 每个item用一次, 下一个level dfs(index + 1)
- Combination DFS. 画个图想想. 每次从1~n里面pick一个数字i
- 因为下一层不能重新回去 [0~i]选，所以下一层recursive要从i+1开始选。



---

**46. [Combination Sum.java](https://github.com/awangdev/LintCode/blob/master/Java/Combination%20Sum.java)**      Level: Medium
      

给一串数字candidates (no duplicates), 和一个target. 

找到所有unique的 组合(combination) int[], 要求每个combination的和 = target.

注意: 同一个candidate integer, 可以用任意多次.


#### DFS, Backtracking
- 考虑input: 没有duplicate, 不需要sort
- 考虑重复使用的规则: 可以重复使用, 那么for loop里面dfs的时候, 使用curr index
- the result is trivial, save success list into result.

##### Combination DFS 思想
- 在每个index上面都要面临: pick/not pick的选择
- 每次pick以后, 就生成一条新的routine, from this index
- 下一个level的dfs从这个index开始, 对后面(或者当下/if allow index reuse) 进行同样的 pick/not pick 的选择
- 注意1: 每个level dfs 里面, for loop 里会有 end condition: 就不必要dfs下去了.
- 注意2: Backtracking在success case && dfs case 后都要做, 因为backtrack 是为了之前上一层dfs.




---

**47. [Combination Sum II.java](https://github.com/awangdev/LintCode/blob/master/Java/Combination%20Sum%20II.java)**      Level: Medium
      

给一串数字candidates (can have duplicates), 和一个target. 

找到所有unique的 组合(combination) int[], 要求每个combination的和 = target.

注意: 同一个candidate integer, 只可以用一次.

#### DFS, Backtracking
- when the input has duplicates, and want to skip redundant items? 
- 1. sort. 2. in for loop, skip same neighbor.
- 考虑input: 有duplicate, 必须sort
- 考虑重复使用的规则: 不可以重复使用
- 1. for loop里面dfs的时候, 使用curr index + 1
- 2. for loop里面, 同一个level, 同一个数字, 不能重复使用: `(i > index && candidates[i] == candidates[i - 1]) continue`
- 因为在同一个level里面重复的数字在下一个dfs level里面是会被考虑到的, 这里必须skip (这个就记住吧)
- the result is trivial, save success list into result.




---

**48. [Combination Sum III.java](https://github.com/awangdev/LintCode/blob/master/Java/Combination%20Sum%20III.java)**      Level: Medium
      

给一个integer k, 和一个target n. 

从positive数字[1 ~ 9], 找到所有unique的 组合(combination) int[], size = k, 要求每个combination的和 = n.

(隐藏条件, 需要clarify): 同一个candidate integer [1 ~ 9], 只可以用一次.

#### DFS, Backtracking
- 跟Combination Sum I, II 没什么太大区别, 只不过, 一定要用k个数字, 也就是一个for loop里面的特别条件
- 考虑input: 没有重复数字 [1 ~ 9]
- 考虑candidate重复利用: 不可以重复利用, next level dfs 时候, curr index + 1
- the result is trivial, save success list into result.



---

**49. [Subset.java](https://github.com/awangdev/LintCode/blob/master/Java/Subset.java)**      Level: Medium
      

给一串unique integers, 找到所有可能的subset. result里面不能有重复.

#### DFS
- dfs的两种路子: 1. pick&&skip dfs, 2. for loop dfs
- 1. pick&&skip dfs: 取或者不取 + backtracking. 当level/index到底，return 一个list.
- 2. for loop dfs: for loop + backtracking. 记得：做subset的时候, 每个dfs recursive call是一种独特可能，先加进rst。
- Time&&space: subset means independent choice of either pick&&not pick. You pick n times: O(2^n), 3ms

#### Bit Manipulation
- n = nums.length, 那么在每一个index, 都是 pick / not pick: 0/1
- 考虑subset index 0/1的bit map: range 的就是 [0000...00 ~ 2^n-1]
- 每一个bitmap就能展现出一个subset的内容: all the 1 represents picked indexes
- 做法:
- 1. 找出Range
- 2. 遍历每一个bitmap candidate
- 3. 对每一个integer 的 bit representation 遍历, 如果是1, add to list
- time: O(2^n * 2^n) = O(4^n), still 3ms, fast.

#### Iterative, BFS
- Regular BFS, 注意考虑如果让one level to generate next level
- 1. 用queue来存每一次的candidate indexes
- 2. 每一次打开一层candiates, add them all to result
- 3. 并且用每一轮的candidates, populate next level, back into queue.
- should be same O(2^n), but actual run time 7ms, slower





---

**50. [Subsets II.java](https://github.com/awangdev/LintCode/blob/master/Java/Subsets%20II.java)**      Level: Medium
      

给一串integers(may have duplicates), 找到所有可能的subset. result里面不能有重复.

#### DFS
- DFS, 找准需要pass along的几个数据结构. 先sort input, 然后DFS
- Using for loop approach: 每个dfs call是一种可能性，直接add into result.     
- 为了除去duplicated result, skip used item at current level: `if (i > depth && nums[i] == nums[i - 1]) continue;`
- srot O(nlogn), subset: O(2^n)

#### BFS
- Regular BFS, 注意考虑如果让one level to generate next level
- skip duplicate: `if (i > endIndex && nums[i] == nums[i - 1]) continue;`
- 1. 用queue来存每一次的candidate indexes
- 2. 每一次打开一层candiates, add them all to result
- 3. 并且用每一轮的candidates, populate next level, back into queue.
- srot O(nlogn), subset: O(2^n)
- should be same O(2^n). slower than dfs

#### Previous notes:
- 在DFS种skip duplicate candidates, 基于sorted array的技巧：    
- 一旦for loop里面的i!=index，并且nums[i] == nums[i-1],
- 说明x=nums[i-1]已经在curr level 用过，不需要再用一次: [a,x1,x2]，x1==x2    
- i == index -> [a,x1]    
- i == index + 1 -> [a,x2]. 我们要skip这一种
- 如果需要[a,x1,x2]怎么办？ 其实这一种在index变化时，会在不同的两个dfs call 里面涉及到。

#### 注意
- 不能去用result.contains(), 这本身非常costly O(nlogn)




---

**51. [Binary Tree Right Side View.java](https://github.com/awangdev/LintCode/blob/master/Java/Binary%20Tree%20Right%20Side%20View.java)**      Level: Medium
      

给一个binary tree, 从右边看过来, return all visible nodes

#### BFS
- 最右:即level traversal每一行的最末尾.   
- BFS, queue 来存每一行的内容, save end node into list

#### DFS
- Use Map<Level, Integer> 来存每一个level的结果
- dfs(node.right), 然后 dfs(node.left)



---

**52. [Binary Tree Maximum Path Sum II.java](https://github.com/awangdev/LintCode/blob/master/Java/Binary%20Tree%20Maximum%20Path%20Sum%20II.java)**      Level: Medium
      

找到从max path sum from root. 条件: 至少有一个node.

#### DFS
- 比Binary Tree Maximum Path Sum I 简单许多. 因为条件给的更多：at least 1 node + have to start from root
- root一定用到
- 3种情况: curr node, curr+left, curr+right
- 因为一定包括root, 说以从 `dfs(root, sum=0)` 开始, 每个level先加root, sum += root.val



---

**53. [Binary Tree Longest Consecutive Sequence.java](https://github.com/awangdev/LintCode/blob/master/Java/Binary%20Tree%20Longest%20Consecutive%20Sequence.java)**      Level: Medium
      

找到binary tree 里的最长 consecutive sequence.

#### DFS
- Divide and Conquer. dfs
- 分开 看左边/右边
- 如果左边满足连续递增的规则, dfs (depth + 1), 如果不满足规则, dfs(depth = 1)
- 右边也是一样
- 对结果跟max作比较, return



---




 
 
 
## Game Theory (4)
**0. [Coins in a Line.java](https://github.com/awangdev/LintCode/blob/master/Java/Coins%20in%20a%20Line.java)**      Level: Medium
      

拿棋子游戏, 每个人可以拿1个或者2个, 拿走最后一个子儿的输. 问: 根据给的棋子输, 是否能确定先手的输赢?

Game Theory: 如果我要赢, 后手得到的局面一定要'有输的可能'.

#### DP, Game Theory
- 要赢, 必须保证对手拿到棋盘时, 在所有他可走的情况中, '有可能败', 那就足够.
- 设计dp[i]:表示我面对i个coins的局面时是否能赢, 取决于我拿掉1个,或者2个时, 对手是不是会可能输?
- dp[i] = !dp[i - 1] || !dp[i-2]
- 时间: O(n), 空间O(n)
- 博弈问题, 常从'我的第一步'角度分析, 因为此时局面最简单.

#### Rolling Array
空间优化O(1). Rolling array, %2



---

**1. [Coins in a Line II.java](https://github.com/awangdev/LintCode/blob/master/Java/Coins%20in%20a%20Line%20II.java)**      Level: Medium
      

给一串coins, 用values[]表示; 每个coin有自己的value. 先手/后手博弈,
每次只能 按照从左到右的顺序, 拿1个或者2个棋子, 最后看谁拿的总值最大.

MiniMax的思考方法很神奇, 最后写出来的表达式很简单

#### DP, Game Theory 自考过程比较长
- 跟Coins in a line I 不一样: 每个coin的value不同.
- 用到MiniMax的思想, 这里其实是MaxiMin. Reference: http://www.cnblogs.com/grandyang/p/5864323.html
- Goal: 使得player拿到的coins value 最大化.
- 设定dp[i]: 从index i 到 index n的最大值. 所以dp[0]就是我们先手在[0 ~ n]的最大取值 
- 于此同时, 你的对手playerB也想最大化, 而你的选择又不得不被对手的选择所牵制.
- 用MaxiMin的思想, 我们假设一个当下的状态, 假想对手playerB会做什么反应(从对手角度, 如何让我输)
- 在劣势中(对手让我输的目标下)找到最大的coins value sum


##### 推算表达式
- Reference里面详细介绍了表达式如何推到出来, 简而言之:
- 如果我选了i, 那么对手就只能选(i+1), (i+2) 两个位置, 而我在对方掌控时的局面就是min(dp[i+2], dp[i+3])
- 如果我选了i和(i+1), 那么对手就只能选(i+2), (i+3) 两个位置, 而我在对方掌控时的局面就是min(dp[i+3], dp[i+4])
- 大家都是可选1个或者2个coins
- 目标是maximize上面两个最坏情况中的最好结果

##### 简化表达式
- 更加简化一点: 如果我是先手, dp[i]代表我的最大值.
- 取决于我拿了[i], 还是[i] + [i+1], 对手可能是dp[i + 1], 或者是dp[i+2]
- 其实dp[i] = Math.max(sum - dp[i + 1], sum - dp[i + 2]);
- 这里的sum[i] = [i ~ n] 的sum, 减去dp[i+1], 剩下就是dp[i]的值没错了

##### Initialization
- 这个做法是从最后往前推的, 注意initialize dp末尾的值.
- dp = new int[n + 1]; dp[n] = 0; // [n ~ n]啥也不选的时候, 为0.
- sum = new int[n + 1]; sum[n] = 0; // 啥也不选的时候, 自然等于0
- 然后记得initialize (n-1), (n-2)

##### 时间/空间
Time O(n)
Space O(n): dp[], sum[]



---

**2. [Coins in a Line III.java](https://github.com/awangdev/LintCode/blob/master/Java/Coins%20in%20a%20Line%20III.java)**      Level: Hard
      

还是2个人拿n个coin, coin可以有不同的value. 

只不过这次选手可以从任意的一头拿, 而不限制从一头拿. 算先手会不会赢?

#### Memoization + Search
- 跟Coins in a Line II 一样, MaxiMin的思想: 找到我的劣势中的最大值
- dp[i][j] 代表在[i,j]区间上 选手最多能取的value 总和
- 同样, sum[i][j]表示[i] 到 [j]间的value总和
- 对手的最差情况, 也就是先手的最好情况:
- dp[i][j] = sum[i][j] - Math.min(dp[i][j - 1], dp[i + 1][j]);
- 这里需要search, 画出tree可以看明白是如何根据取前后而分段的.

#### 博弈 + 区间DP
- 因为是看区间[i,j]的情况, 所以可以想到是区间 DP
- 这个方法需要复习, 跟数学表达式的推断相关联: S(x) = - S(y) + m. 参考下面的公式推导.
- dp[i][j]表示 从index(i) 到 index(j), 先手可以拿到的最大值与对手的数字差. 也就是S(x).
- 其中一个S(x) = dp[i][j] = a[i] - dp[i + 1][j]
- m 取在开头, m 取在末尾的两种情况:
- dp[i][j] = max{a[i] - dp[i + 1][j], a[j] - dp[i][j - 1]}
- len = 1, 积分就是values[i]
- 最后判断 dp[0][n] >= 0, 最大数字和之差大于0, 就赢.
- 时间/空间 O(n^2)

##### 公式推导
- S(x) = X - Y, 找最大数字和之差, 这里X和Y是选手X的总分, 选手Y的总分. 
- 对于选手X而言: 如果S(x)最大值大于0, 就是赢了; 如果最大值都小于0, 就一定是输了. 
- 选手Y: S(y)来表示 对于Y,  最大数字和之差. S(y) = Y - X
- 根据S(x) 来看, 如果从 数字和X里面, 拿出一个数字 m, 也就是 X = m + Xwithout(m)
- S(x) = m + Xwithout(m) - Y = m + (Xwithout(m) - Y). 
- 如果我们从全局里面索性去掉m, 那么 S(y'') = Y - Xwithout(m)
- 那么推算下来: S(x) = m + (Xwithout(m) - Y) = m - (Y - Xwithout(m)) = m - S(y'')
- 在这个问题里面, 我们model X 和 Y的时候, 其实都是 dp[i][j], 而区别在于先手/后手.
- 将公式套用, 某一个S(x) = a[i] - dp[i + 1][j],  也就是m=a[i], 而 S(y'') = dp[i + 1][j]

##### 注意
- 如果考虑计算先手[i, j]之间的最大值, 然后可能还需要两个数组, 最后用于比较先手和opponent的得分大小 => 那么就要多开维.
- 我们这里考虑的数字差, 刚好让人不需要计算先手的得分总值, 非常巧妙.
- Trick: 利用差值公式, 推导有点难想到.

##### 区间型动态规划
- 找出[i, j]区间内的性质: dp[i][j]下标表示区间范围 [i, j]
- 子问题: 砍头, 砍尾, 砍头砍尾
- loop应该基于区间的length
- template: 考虑len = 1, len = 2; 设定i的时候一定是 i <= n - len; 设定j的时候, j = len + i - 1;




---

**3. [Nim Game.java](https://github.com/awangdev/LintCode/blob/master/Java/Nim%20Game.java)**      Level: Easy
      

#### Brainteaser
- 著名Nim游戏
- 写一些，发现n=4,5,6,7,8...etc之后的情况有规律性: 谁先手拿到4就输了.
- 最终很简单n%4!=0就可以了,  time, space O(1)

#### DP
- 正规地找规律做, 就跟 coins in a line 一样, 按照先手后手来做
- 可以rolling array 优化空间
- Time O(n), 当然啦, 这个题目这样会timeout, 可以使用brainteaser的做法写出结果.



---




 
 
 
## Hash Table (26)
**0. [Jewels and Stones.java](https://github.com/awangdev/LintCode/blob/master/Java/Jewels%20and%20Stones.java)**      Level: Easy
      
1524017454

给J 和 S两个string. J里的character是unique 的珠宝, S 里面的character包含珠宝和石头. 找S里面有多少珠宝

#### Basic HashSet



---

**1. [Find Anagram Mappings.java](https://github.com/awangdev/LintCode/blob/master/Java/Find%20Anagram%20Mappings.java)**      Level: Easy
      

比较简单, 用HashMap 存index list. 最后再遍历一遍数组A, 列举出所有元素.
O(n)



---

**2. [Island Perimeter.java](https://github.com/awangdev/LintCode/blob/master/Java/Island%20Perimeter.java)**      Level: Easy
      

最简单的方法: 每个格子4个墙;每个shared的墙要-2 (墙是两面, -1 * 2)
最后合计结果就好.

不必想太多用HashMap做.但是也可以思考一下:
- 把每个block相连的block全部存在以当下block为key的list里面. 那么这里需要把2D坐标, 转化成一个index.
- 最后得到的map, 所有的key-value应该都有value-key的反向mapping, 那么久可以消除干净, 每一次消除就是一个shared wall.
- 一点点optimization: DFS去找所有的island, 如果island的图非常大, 而island本身不打,那么适合optimize.
  但是整体代码过于复杂. 不建议写.




---

**3. [First Unique Character in a String.java](https://github.com/awangdev/LintCode/blob/master/Java/First%20Unique%20Character%20in%20a%20String.java)**      Level: Easy
      

方法1: 按照题意, 找到第一个 first index == last index的字母.

方法2: 用hashmap存字母的index, 有些重复字母的index就会是个list. 找到单一index, 结合成list, sort, return list.get(0)



---

**4. [Encode and Decode TinyURL.java](https://github.com/awangdev/LintCode/blob/master/Java/Encode%20and%20Decode%20TinyURL.java)**      Level: Medium
      

其实想到了切入点, 是个可难可简单的题目. 这里的encode就是想办法把url存起来, 然后给个 key.
那么具体怎么做这个key, 简单就可以用一个map, 然后counting. 复杂一点就可以做random letter/number组成key.



---

**5. [2 Sum.java](https://github.com/awangdev/LintCode/blob/master/Java/2%20Sum.java)**      Level: Easy
      

tutorial:https://www.youtube.com/watch?v=P8zBxoVY1oI&feature=youtu.be

解法1：相对暴力简洁, HashMap<value, index>，找到一个value, 存一个; 若在HashMap里面 match 到结果, 就return HashMap里存的index. O(n) space && time.

解法2：Sort array, two pointer 前后++,--搜索。Sort 用时O(nlogn).     
1. 第一步 two pointer 找 value.       
2. 注意，要利用额外的空间保留original array， 用来时候找index. (此处不能用HashMap，因为以value 为key，但value可能重复)      
O(n) space, O(nlogn) time.    




---

**6. [4 Sum.java](https://github.com/awangdev/LintCode/blob/master/Java/4%20Sum.java)**      Level: Medium
      

方法1：  
   1. 利用2Sum的原理，把4Sum分为连个2Sum。左一个pair,右一个pair，每个pair里面放2个数字。   
   2. 以一个点，i，作为分界口，也要列举出所有i之前的pair,作为基础。   
   3. 再尝试从所有i+1后面,找合适的2nd pair。   
 
   可以用HashSet<List>, 可以直接比较list里面每一个元素, 保证set不重复.
   Previous Notes: 在造class Pair时候，要做@override的function: hashCode(), equals(Object d). 平时不太想得起来用。
   参见 http://lifexplorer.me/leetcode-3sum-4sum-and-k-sum/    

方法2： 3Sum外面再加一层. 参考3Sum. 时间O(n^3)。 但此方法在k-sum时候，无疑过于费时间. O(n^k)



---

**7. [Intersection of Two Arrays II.java](https://github.com/awangdev/LintCode/blob/master/Java/Intersection%20of%20Two%20Arrays%20II.java)**      Level: Easy
      

方法1:
用HashMap: 存一个nums1, 再拿nums2 check against map. 时间/空间:O(n)

方法2:
Binary search? 需要array sorted. 否则时间O(nlogn)不值得.
[没做完, 有错]



---

**8. [Valid Anagram.java](https://github.com/awangdev/LintCode/blob/master/Java/Valid%20Anagram.java)**      Level: Easy
      

HashMap



---

**9. [Longest Substring Without Repeating Characters.java](https://github.com/awangdev/LintCode/blob/master/Java/Longest%20Substring%20Without%20Repeating%20Characters.java)**      Level: Medium
      

方法1:
Two Pointers
双指针: 从start开始遍历, 但是第一步是while loop来推进end; 直到推不动end, 然后start++
巧妙点: 因为end是外围variable, 在start的loop上, end不会重置;[star ~ end] 中间不需要重复计算.
最终可以O(n);

Previous verison of two pointers:
用两个pointer, head和i.
注意：head很可能被退回到很早的地方，比如abbbbbba,当遇到第二个a，head竟然变成了 head = 0+1 = 1.      
当然这是不对的，所以head要确保一直增长，不回溯

方法2:
   HashMap<Char, Integer>: <character, last occurance index>
   一旦有重复, rest map.
   没有重复时候, 不断map.put(), 然后求max值

问题: 每次reset map之后就开始从新从一个最早的index计算, 最坏情况是O(n^2):
'abcdef....xyza'




---

**10. [Minimum Window Substring.java](https://github.com/awangdev/LintCode/blob/master/Java/Minimum%20Window%20Substring.java)**      Level: Hard
      

基本思想: 用个char[]存string的frequency. 然后2pointer, end走到底, 不断validate.
符合的就process as result candidate.

HashMap的做法比char[]写起来要复杂一点, 但是更generic



---

**11. [Longest Substring with At Most K Distinct Characters.java](https://github.com/awangdev/LintCode/blob/master/Java/Longest%20Substring%20with%20At%20Most%20K%20Distinct%20Characters.java)**      Level: Medium
      

大清洗 O(nk)   
map.size一旦>k，要把longest string最开头（marked by pointer:start）的那个char抹掉    
一旦某一个char要被清除，所以在这个char 的1st and last appearance之间的char都要被清洗from map




---

**12. [Palindrome Pairs.java](https://github.com/awangdev/LintCode/blob/master/Java/Palindrome%20Pairs.java)**      Level: Hard
      

Obvious的做法是全部试一遍, 判断, 变成 O(n^2) * O(m) = O(mn^2). O(m): isPalindrome() time.

当然不行了, 那就看是O(nlogN), 还是O(n)?

#### 方法1: Hash Table + Palindrome的性质. 复合型.
O(mn)

##### 思路
- 每一个word, 都可以拆分成 front + mid + end. 如果这个word + 其他word可以组成palindrome,那就是说
- 砍掉 (mid+end), front.reverse() 应该存在 words[] 里面.
- 砍掉 (front+mid), end.reverse() 应该存在 words[] 里面.
- 我们用HashMap存所有的<word, index>, 然后reverse, 找配对就好.

##### Corner case
- 如果有 empty string "", 那么它跟任何一个palindrome word, 都可以配对, 并且根据位置前后变换, 凑成2份 distinct indexes.
- 这样就有了那个 `if (reverseEnd.equals("")) {...}` 的logic.
- 注意: 虽然在处理砍头/砍尾的两个 for loop里面都在根据 empty string 重复记录, 
  但因为 "" 自己本身不能作为起点, 所以overall只会在被其他palindrome配对时记录一次.


#### 方法2: Trie
还要做一下那.



---

**13. [Maximal Rectangle.java](https://github.com/awangdev/LintCode/blob/master/Java/Maximal%20Rectangle.java)**      Level: Hard
      

#### 方法1: monotonous stack
分解开来, 其实是'Largest Rectangle in Histogram', 只不过这里要自己model heights.
一个2D array里面的rectangle, 最终也是用height * width做出来的.
巧妙在于, 把每一行当做底边, 算出这个底边, 到顶部的height: 
- 如果底边上的一个value==0, 那么算作没有height(以这个底边做rectangle, value==0的位置是空中楼阁, 不能用)
- 如果底边上的value==1, 那么就把上面的height加下来, 做成histogram

如果看具体实例, 有些row似乎是白算的, 但是没有办法, 这是一个搜索的过程, 最终会比较出最优解.

#### 方法2: DP
Coordinate DP?



---

**14. [Binary Tree Inorder Traversal.java](https://github.com/awangdev/LintCode/blob/master/Java/Binary%20Tree%20Inorder%20Traversal.java)**      Level: Easy
      

Inorder traverse Binary Tree

#### Recursive
- 在自己的基础上recursive, 不用helper function
- Divide and Conquer, with helper(dfs) method
- O(n) time, no extra space

#### Iterative: Stack
- Add left nodes all the way   
- Print curr   
- Move to right, add right if possible
- O(n) time, O(h) space
  
注意stack.pop()在加完left-most child 的后，一定要curr = curr.right.

若不右移, 很可能发生窘境:
curr下一轮还是去找自己的left-most child，不断重复curr and curr.left, 会infinite loop, 永远在左边上下上下。

#### HashMap
? How?



---

**15. [Contains Duplicate.java](https://github.com/awangdev/LintCode/blob/master/Java/Contains%20Duplicate.java)**      Level: Easy
      

无序数组, 找是否有重复element, return true/false.

#### HashSet
- No brain: HashSet.
- Time O(n), Space O(n)

#### Sort, Binary Search
- Arrays.sort(x): Time O(nLogN), Space O(1)
- 排序后, 重复数会排在一起, 然后 binary search



---

**16. [Contains Duplicate II.java](https://github.com/awangdev/LintCode/blob/master/Java/Contains%20Duplicate%20II.java)**      Level: Easy
      

Unsorted array, 找出是否有duplicate elemenets: 必要条件是, 这两个element的index i,j 的大小最多相差k.

#### HashSet
- 很巧妙地根据k range地条件, 把HashSet里面的值控制在[i - k, i]
- 每次不断地往set里面加新元素, 从set里减去末尾index的元素
- 而set.add(x)如果遇到重复, 会return false.
- 一旦在这个length k 的 range里面, 有重复, 就符合条件. 
- Time O(n)

#### HashTable<value, List of duplicates>
- 记录每个element value的index in the list
- 一旦有重复element重复, 就把整个list of indexes 端出来, 查看有没有符合条件的: (index - i) <= k
- Time O(nm), m = # of duplicates

#### 这两种做法的区别很有艺术感觉
- 方法1是限定选拔的candidate, 不合格就去掉, 那么一旦有符合条件的(duplicates), 那么一定中, 剩下的就不看了.
- 方法2是把符合条件的index找出来, 集中处理, 但是所有candidate都会选出来
- 就好像招人一样: 一种是遇到好的就停止; 第二种是看过所有人, 从中选拔最好的. 显然第一种更快.




---

**17. [Find All Anagrams in a String.java](https://github.com/awangdev/LintCode/blob/master/Java/Find%20All%20Anagrams%20in%20a%20String.java)**      Level: Easy
      

跟 Permutation in String 很像. 给短string p， 长string s.

找所有p的 anagram (permutation) 在s 里面的起始index.

#### HashTable
- count character apperance 就想到hashtable
- 注意countS, countP 的技巧: 作比较只需要O(26)
- Overall timeO(n)
- 小心不要用一个int[] count 来技术 查0, 复杂度是O(n)



---

**18. [Group Anagrams.java](https://github.com/awangdev/LintCode/blob/master/Java/Group%20Anagrams.java)**      Level: Medium
      

给一串string, return list of list, 把anagram 放在一起.

#### Hash Table, key 是 character frequency
- 存anagram
- 用 character frequency 来做unique key
- 用固定长度的char[26] arr 存每个字母的frequency; 然后再 new string(arr).   
- 因为每个位子上的frequency的变化，就能构建一个unique的string
- O(nk), k = max word length


#### Hash Table, key 是 sorted string
- 和check anagram 想法一样：转化并sort char array，用来作为key。
- 把所有anagram 存在一起。注意结尾Collections.sort().
- O(NKlog(K)), N = string[] length, k = longest word length    




---

**19. [Count Primes.java](https://github.com/awangdev/LintCode/blob/master/Java/Count%20Primes.java)**      Level: Easy
      

计数: 所有小于n的prime number.

#### prime number定义
- >=2的没有除自己和1以外公约数的数。   
- 还有另外一个定义方法: 这个n,有没有小于n的一个i, 而达到： i * i + # of i = n. 如果有，那就不是 prime   

#### Steps
- 一个boolean长条，存isPrime[]。 然后从i=2， 全部变true.
- hash key: the number itself
- 然后利用这个因子的性质，非prime满足条件： self*self, self * self + self ... etc.     
- 所以就check每一个j, j+i, j+i+i, 然后把所有non-prime全部mark成false.     
- 最后，数一遍还剩下的true个数就好了   



---

**20. [Palindrome Permutation.java](https://github.com/awangdev/LintCode/blob/master/Java/Palindrome%20Permutation.java)**      Level: Easy
      

给String, 看permutation是否能是palindrome

#### Hash, or ASCII array
- count occurrance
- 只可以接受一个odd # appearance.
- 考虑所有 256 ASCII code, 如果还要拓展, 就用HashMap<Character, Integer>
- 注意, 不能assum lower case letter. 应该至少是所有ASCII code



---

**21. [Lowest Common Ancestor II.java](https://github.com/awangdev/LintCode/blob/master/Java/Lowest%20Common%20Ancestor%20II.java)**      Level: Easy
      

给一个Binary Tree root, 以及两个node A, B. 特点: node里面存了parent pointer. 找 lowest common ancestor


#### Hash Set
- 这个题有个奇葩的地方, 每个node还有一个parent, 所以可以自底向上.
- save visited in hashset. 第一个duplicate, 就是A B 的 lowest common ancestor

#### Save in lists
- 自底向上。利用parent往root方向返回
- 把所有parent存下来, 然后在两个list里面找最后一个 common node

#### 注意
- 无法从root去直接搜target node 而做成两个list. 因为根本不是Binary Search Tree！




---

**22. [Hash Function.java](https://github.com/awangdev/LintCode/blob/master/Java/Hash%20Function.java)**      Level: Easy
      

#### Hash Function
- 解释Hash怎么做. 
- Hash function例子：    
- hashcode("abcd") = (ascii(a) * 33^3 + ascii(b) * 33^2 + ascii(c) *33^1 + ascii(d)*33^0) % HASH_SIZE 
- 用到的参数比如: magic number 33, HASH_SIZE.

- Hash的意义是：给一个string key, 转换成数字，从而把size变得更小。    
- 真实的implementation还要处理collision, 可能需要design hash function 等等。


- 每一步都:
- hashRst = hashRst * 33 + (int)(key[i]);       
- hashRst = hashRst % HASH_SIZE;       
- 原因是，hashRst会变得太大，所以不能算完和 再 %...



---

**23. [LRU Cache.java](https://github.com/awangdev/LintCode/blob/master/Java/LRU%20Cache.java)**      Level: Hard
      

#### Double Linked List
- 用了一个特别的双向的ListNode，有了head和tail，这样就大大加快了速度。     
- 主要加快的就是那个‘更新排位’的过程，找到item hashmap O(1), 做减法换位也都是O(1)
- Overall O(1)

##### 巧妙点
- 1. head和tail特别巧妙：除掉头和尾，和加上头和尾，就都特别快。    
- 2. 用双向的pointer: pre和next, 当需要除掉任何一个node的时候，只要知道要除掉哪一个，     
- 直接把node.pre和node.next耐心连起来就好了，node就自然而然的断开不要了。     
- 一旦知道怎么解决了，就不是很特别，并不是难写的算法:    
- moveToHead()    
- insertHead()    
- remove()      

#### O(n) 检查重复
- timeout method, 天真的来了一个O(n) 的解法，结果果然timeout.     
- 一个map<key,value>存数值。一个queue<key>来存排位。     
- 每次有更新，就把最新的放在末尾；每次超过capaticity,就把大头干掉。很简单嘛，但是跑起来太久，失败了。     




---

**24. [Longest Word in Dictionary.java](https://github.com/awangdev/LintCode/blob/master/Java/Longest%20Word%20in%20Dictionary.java)**      Level: Easy
      

#### Sort, HashSet
- 先排序, 排序以后才能逐个看是否partial string已经存在
- 用 set.contains(substring(0, n - 1)) 来查看上一步的 substring 是否存在
- 如果找到, 因为已经按照字母表排序, 找到的这个肯定是这个长度里面最符合的解答.
- 然后brutally找下一个更大的.
- Sort O(n log n), O(n) set space

#### Trie
- 可以先sort words Array: 1. 长 string 排在前; 2. 相等length, 按照dictionary order 排序
- 全部放入Trie. Trie.insert()
- 针对sorted words array, 从最长的开始找 Trie.startWith.
- 一旦找到, 就是符合题意的, 直接return.
- 注意: startWith 必须每一个node都是 isEnd, 才满足'逐个字母拼出' 的条件.
- Time: build Trie O(mn) + sort:O(nlogn) => O(nlogn)
- Space: O(mn)

#### 
- 按大小排序 -> 从最大的开始做contains()的比较 -> 结果再按照字母表顺序(lexicographically) sort一下.
- 但是Collections.sort()了两次, 而且再list.contains(), 比较慢




---

**25. [Longest Consecutive Sequence.java](https://github.com/awangdev/LintCode/blob/master/Java/Longest%20Consecutive%20Sequence.java)**      Level: Hard
      

给一串数字, unsorted, 找这串数字里面的连续元素序列长度 (consecutive序列, 是数字连续, 并不是说要按照原order)

#### HashSet
- 要想看连续元素, 必须要num++, num--这样搜索
- 1. 需要O(1)找到元素
- 2. 需要简单快速找到 num - 1, num + 1.
- 如果用min,max开array, 耗费空间
- 用HashSet来存, 用set.contains() 来查找 num - 1, num + 1 存在与否
- for loop. O(n) 
- 里面的while loop 一般不会有O(n); 一旦O(n), 也意味着set 清零, for loop也不会有更多 inner while 的衍生.
- overall O(n) 时间复杂度


#### Union Find
- 最终是要把相连的元素算一下总长, 其实也就是把元素group起来, 相连的group在一起, 于是想到UnionFind
- 这里用到了一个`int[] size` 来帮助处理 `合并的时候parent是哪个`的问题: 永远往group大的union里去
- main function 里面, 有一个map来track, 每个元素, 只处理1遍.
- union的内容: current number - 1, current number + 1
- https://www.jianshu.com/p/e6b955ca208f

##### 特点
- Union Find 在index上做好像更加容易
- 其他union find function: `boolean connected(a,b){return find(a) == find(b)}`



---




 
 
 
## Backtracking (22)
**0. [Letter Combinations of a Phone Number.java](https://github.com/awangdev/LintCode/blob/master/Java/Letter%20Combinations%20of%20a%20Phone%20Number.java)**      Level: Medium
      

方法1: Iterative with BFS using queue.

方法2: Recursively adding chars per digit



---

**1. [Regular Expression Matching.java](https://github.com/awangdev/LintCode/blob/master/Java/Regular%20Expression%20Matching.java)**      Level: Review
      



---

**2. [Wildcard Matching.java](https://github.com/awangdev/LintCode/blob/master/Java/Wildcard%20Matching.java)**      Level: Hard
      

Double sequence DP. 与regular expression 很像.

注意1: 分析字符 ?, * 所代表的真正意义, 然后写出表达式.
注意2: 搞清楚initialization 的时候 dp[i][0] 应该always false.当p为empty string, 无论如何都match不了 (除非s="" as well)
    同时 dp[0][j]不一定是false. 比如s="",p="*" 就是一个matching.



---

**3. [Word Break II.java](https://github.com/awangdev/LintCode/blob/master/Java/Word%20Break%20II.java)**      Level: Review
      

两个DP一起用.解决了timeout的问题     
1. isWord[i][j], subString(i,j)是否存在dict中？

2. 用isWord加快 isValid[i]: [i ～ end]是否可以从dict中找到合理的解？      
	从末尾开始查看i：因为我们需要测试isWord[i][j]时候，j>i, 而我们观察的是[i,j]这区间；       
	j>i的部分同样需要考虑，我们还需要知道isValid[0～j+1]。 所以isValid[x]这次是表示[x, end]是否valid的DP。     
	i 从 末尾到0, 可能是因为考虑到isWord[i][j]都是在[0~n]之内，所以倒过来数，坐标比较容易搞清楚。     
	(回头看Word Break I， 也有坐标反转的做法)

3. dfs 利用 isValid 和isWord做普通的DFS。

Note:
在Word Break里面用了set.contains(...), 在isValid里面，i 从0开始。 但是，contains()本身是O(n).     
在这道题里面应该是因为word dictionary太大，加上nest for, 变成O(n^3)所以timeout.

istead,用一个isWord[i][j]，就O(1)判断了i~j是不是存在dictionary里面。



---

**4. [Binary Tree Paths.java](https://github.com/awangdev/LintCode/blob/master/Java/Binary%20Tree%20Paths.java)**      Level: Easy
      

给一个binary tree, 返回所有root-to-leaf path

#### DFS
- Recursive:分叉. dfs.

#### Iterative
- Iterative, 非递归练习了一下
- 因为要每次切短list, 所以再加了一个Stack 来存level
- 单这道题用dfs更简单, 因为找的就是从头到尾的path, 是dfs的pattern




---

**5. [Add and Search Word.java](https://github.com/awangdev/LintCode/blob/master/Java/Add%20and%20Search%20Word.java)**      Level: Medium
      

Trie结构, prefix tree的变形： '.'可以代替任何字符，那么就要iterate这个node所有的children.

节点里面有char, isEnd, HashMap<Character, TrieNode>   
Build trie = Insert word:没node就加，有node就移动。   
Search word:没有node就报错. 到结尾return true   

这题因为'.'可以代替任何possible的字符，没一种都是一个新的path，所以recursive做比较好些。    
(iterative就要queue了,麻烦点)



---

**6. [Word Search II.java](https://github.com/awangdev/LintCode/blob/master/Java/Word%20Search%20II.java)**      Level: Hard
      

给一串words, 还有一个2D character matrix. 找到所有可以形成的words. 条件: 2D matrix 只可以相邻走位.

#### Trie, DFS
- 相比之前的implementation, 有一些地方可以优化:
- 1. Backtracking时候, 在board[][] 上面mark就可以, 不需要开一个visited[][]
- 2. 不需要implement trie的所有方程, 用不到: 这里只需要insert.
- 普通的trie题目会让你search a word, 但是这里是用一个board, 看board的每一个字母能不能走出个Word.
- 也就是: 这里的search是自己手动写, 不是传统的trie search() funcombination
- 3. TrieNode里面存在 end的时候存string word, 表示到底. 用完了 word = null, 刚好截断重复查找的问题.

##### 关于Trie
- Build Trie with target words: insert, search, startWith.    
- 依然要对board matrix做DFS。
- no for loop on words. 直接对board DFS:   
- 每一层,都会有个up-to-this-point的string. 在Trie里面check它是不是存在。以此判断。   
- 若不存在，就不必继续DFS下去了。
- Trie solution time complexity, much better:      
- build Trie:   n * wordMaxLength
- search: boardWidth * boardHeight * (4^wordMaxLength + wordMaxLength[Trie Search])


#### Regular DFS
- for loop on words: inside, do board DFS based on each word.     
- Time cpmplexity: word[].length * boardWidth * boardHeight * (4^wordMaxLength)

#### Previous Notes
- Big improvement: use boolean visited on TrieNode!     
- 不要用rst.contains(...), 因为这个是O(n) 在leetcode还是会timeout（lintcode竟然可以pass）!    
- 在Trie search() method 里面，凡是visit过的，mark一下。  





---

**7. [Word Search.java](https://github.com/awangdev/LintCode/blob/master/Java/Word%20Search.java)**      Level: Medium
      

Backtracking:
找到开头的字母, 然后recursively DFS 去把word串到底:
每到一个字母, 朝四个方向走, 之中一个true就可以.

Note:每次到一个字母，mark一下'#'. 4个path recurse回来后，mark it back.

Backtracking方法2:    
用一个boolean visited[][]





---

**8. [Word Squares.java](https://github.com/awangdev/LintCode/blob/master/Java/Word%20Squares.java)**      Level: Hard
      

可以开Trie class, 里面用到TrieNode. 开Trie(words) 可以直接initalize with for loop
TrieNode 里面可以有一个 List<String> startWith: 记录可以到达这个点的所有string: 有点像树形, ancestor形状的存储.

神操作:
根据square的性质, 如果选中了list of words, 设定 int prefixIndex = list.size().
取出list里面的所有word[prefixedIndex], 并且加在一起, 就是下一个word candidate的 prefix.

形象一点:
list = ["ball", "area"];
prefixIndex = list.size(); ball[prefixIndex] = 'l'; area[prefixIndex] = 'e';
//then
candidatePrefix = ball[prefixIndex] + area[prefixIndex] = "le";
这里就可以用到Trie的那个 findByPrefix function, 在每个点, 都存有所有这个点能产生的candidate.
这时, 试一试所有candidate: dfs

能想到这种倒转的结构来存prefix candidates 在 Trie里面, 这个想法非常值得思考.



---

**9. [Course Schedule.java](https://github.com/awangdev/LintCode/blob/master/Java/Course%20Schedule.java)**      Level: Medium
      

- 一堆课用int[2] pair 来表示. [1, 0] 表示要上课1的话, 必须先把课0上了. 
- 每一个数字都是一个ndoe, 题目问是否能把所有的课排了
- input是 numOfCourses, 还有这个prerequisites [[]]

#### Topological Sort
- 给一个graph of nodes
- 至关重要: 用`List[] edges; edges[i] = new ArrayList<>();` 来表示graph: 就是每个node, to all its neighbors
- 目标是根据edge 的 direction, 把这个graph 里面的 node sort 一个list
- 如果有cycle, 这个item就不会被放在最后的list 里面. 
- 比如: 如果两个课互相是dependency, 就变成了cyclic dependency, 这样不好.


#### BFS
- Kahn algorithem:
- 先build一个graph map: <node, list of nodes >; or `List[] edges; edges[i] = new ArrayList<>();`
- count in-degree: inDegree就是每个node上面, 有多少个走进来的edge?
- 那些没有 in-coming-edge的, indegree 其实就 等于 0, 那么他们就应该在final result list里面
- 对这些 indegree == 0 的 nodes BFS, add to queue.
- 模拟visit每个ndoe, 如果visit过了, 这个node上的 indegree--, 然后如果最终 indegree == 0, 这个node就成功进入final list.

##### Indegree 原理
- Note: 如果有cycle, indegree是不会变成0的, 它也无法进入最终list. 
- indegree是周围的node到我这里的次数count. 
- 如果周围所有node的连线, 都意义切除后, 我的indegree还不等于0, 那么肯定有某些node间接地有重复连线, 也就是有cycle

#### DFS
- 这道题没有要求作出final list, 相对简单, 只要visit每个nodes, 最后确认没有cycle就好了
- 用 visited int[] 来确认是否有cycle. 1 代表 paretNode visited, -1 代表在DFS上一行的标记
- 如果遇到-1, 说明这个node在上一级或者以上的同一个dfs path里面已经走过, 那么证明有cycle, return false.
- 走完一个node的所有neighbor, 都没有fail, 那么backtracking, set visited[i] = 1
- 真的topo sort会在DFS的底端, 把record放进一个stack, 最后reverse, 就是真的sort order.

#### Notes:
- 还有 List[] arrayOfList = new ArrayList[]; 这样的操作啊, 代替了map<integer, integerList>

#### Previous notes
有点绕，但是做过一次就明白一点。    
是topological sort的题目。一般都是给有dependency的东西排序。    

最终都会到一个sink node， 再不会有向后的dependency, 在那个点截止。    
我就已这样子的点为map的key, 然后value是以这个node为prerequisite的 list of courses.    

画个图的话，prerequisite都是指向那个sink node， 然后我们在组成map的时候，都是从sink node 发散回来到dependent nodes.    

在DFS里面，我们是反向的， 然后，最先完全visited的那个node, 肯定是最左边的node了，它被mark的seq也是最高的。    

而我们的sink node，当它所有的支线都visit完了，seq肯定都已经减到最小了，也就是0，它就是第一个被visit的。   


最终结果：
每个有pre-requisit的node都trace上去（自底向上），并且都没有发现cycle.也就说明schedule可以用了。



---

**10. [Alien Dictionary.java](https://github.com/awangdev/LintCode/blob/master/Java/Alien%20Dictionary.java)**      Level: Hard
      

给一个 array of strings: 假如这个array是按照一个新的字母排序表(alien dictionary)排出来的, 需要找到这个字母排序.

有可能有多重排序的方法, 给出一种就可以.

#### Graph
- 本质: 上下两行string, 相对应的相同的index上, 如果字母不同, 就说明排在第一行的字母在字母表里更领先
- 把 string array 变成topological sort的 graph: `map<char, list<char>>`
- 也可以`List[26] edges` (Course Schedule problem)
- Build edges: find char diff between two row, and store the order indication into graph
- 注意: indegree 永远是反向的 (跟 node to neighbors 相反的方式建立)

#### BFS
- topological sort 本身很好写, 但是要在题目中先了解到字母排序的本质
- 其实上面这个排序的本质很好想, 但是把它具体化成构建graph的代码, 会稍微有点难想到
- 算indegree, 然后用 BFS 来找到那些 inDegree == 0的 node
- 最先inDegree == 0的node, 就排在字母表前面.
- 下面的解法, 用了Graph: map<Character, List<Character>>, 而不是 List[26], 其实更加试用超过26个字母的dictionary.

#### DFS
- 跟BFS建立 grpah 的过程一模一样
- DFS的不同在于: 用visited map 来标记走过的地方
- 走到leaf的时候, add to result: 但因为走到了底才add, 最终的顺序应该颠倒 (或者, sb.insert(0, x) 直接用颠倒的顺序add)



---

**11. [Palindrome Partitioning.java](https://github.com/awangdev/LintCode/blob/master/Java/Palindrome%20Partitioning.java)**      Level: Medium
      

给个string s, partition(分段)后, 要确保每个partition都是palindrome. 

求所有partition palindrome组合. `list<list<string>>`

#### DFS
- 在遍历str的时候，考虑从每个curr spot 到 str 结尾，是能有多少种palindorme?
- 那就从curr spot当个字符开始算，开始back tracing.
- 如果所选不是palindrome， 那move on.
- 若所选的确是palindrome,　加到path里面，DFS去下个level，等遍历到了结尾，这就产生了一种分割成palindrome的串。
- 每次DFS结尾，要把这一层加的所选palindrome删掉，backtracking嘛

#### Optimization
- 可以再每一个dfs level 算 isPalindrome(S), 但是可以先把 boolean[][] isPalin 算出来, 每次O(1) 来用
- 注意: isPalin[i][j] 是 inclusive的, 所以用的时候要认准坐标
- Overall Space O(n^2): 存 isPlain[][]
- Time O(n!), 每一层的for loop spawn n * (n - 1) * (n - 2)



---

**12. [Permutations II.java](https://github.com/awangdev/LintCode/blob/master/Java/Permutations%20II.java)**      Level: Medium
      

给一串数组, 找出所有permutation数组. 注意: 给出的nums里面有重复数字, 而permutation的结果需要无重复.

#### Backtracking
- 排序, 
- Mark visited. 通过permutation规律查看是否排出了重复结果
- 并且要检查上一层recursive时有没有略过重复element
- time O(n!)

##### 背景1
- 在recursive call里面有for loop, 每次从i=0开始, 试着在当下list上加上nums里面的每一个。    
- 从i=0开始，所以会依次recursive每一个nums：
- 因此，例如i=2,肯定比i=3先被访问。也就是:取i=2的那个list permutation肯定先排出来。   

##### 背景2
- 重复的例子：给出Input[x, y1, y2], 假设y的值是一样的。那么，{x,y1,y2}和{x,y2,y1}是相同结果。

##### Note
- 综上，y1肯定比y2先被访问,{x,y1,y2}先出。 紧随其后，在另一个recursive循环里，{x,y2...}y2被先访问，跳过了y1。    
- 重点:规律在此，如果跳过y1，也就是visited[y1] == false, 而num[y2] == num[y1]，那么这就是一个重复的结果，没必要做，越过。
- 结果:那么，我们需要input像{x,y1,y2}这样数值放一起，那么必须排序。

#### Non-recursive, manuall swap
- Idea from: https://www.sigmainfy.com/blog/leetcode-permutations-i-and-ii.html
- 用到 sublist sort
- 用 swap function, 在原数组上调节出来新的permutation
- 注意: 每次拿到新的candidate, 都要把没有permutate的数位sort, 然后再开始swap.
- 这是为了确保, [j]和[j-1]在重复时候, 不用重新记录.

#### Queue
- 给一个visited queue
- 和queue在所有的地方一同populate. 
- 然后visited里面存得时visited indexes。 (Not efficient code. check again)



---

**13. [N-Queens.java](https://github.com/awangdev/LintCode/blob/master/Java/N-Queens.java)**      Level: Hard
      

N-Queen 问题, 给数字n, 和 nxn board, 找到所有N-queens的答案.

#### Backtracking
- 用dfs找所有情况, 每一个iteration, 从找一行里挑合适的点, dfs
- 选中的点加进candidate list 里面, 记得要backtracking.
- 每一个candidate都需要validation, 检查 row, col, 2 diagnal 有没有queen

#### validate n queue at certain (x, y)
- 1. array 里面不能有 target row#
- 2. diagnal. 记得公式：
- row1 - row2 == col1 - col2.     Diagnal elelment.fail
- row1 - row2 == - (col1 - col2). Diagnal element. fail
- Draw a 3x3 board to test the 2 scanarios:
- (0,0) and (3,3) are diagnal
- (0,2) and (2,0) are diagnal




---

**14. [N-Queens II.java](https://github.com/awangdev/LintCode/blob/master/Java/N-Queens%20II.java)**      Level: Hard
      

跟 N-Queens 一样, 不是找所有结果, 而是count多少结果.

#### Backtracking
- 当list.size() == n 的时候，说明找到了一个Solution。
- 1. dfs function (List<Integer>, n)
- 2. validate function



---

**15. [Path Sum II.java](https://github.com/awangdev/LintCode/blob/master/Java/Path%20Sum%20II.java)**      Level: Easy
      

给一个inputSum, 然后dfs, 找到所有path, 满足: path sum 跟 inputSum 一样.

#### DFS, Backtracking
- 用remaining sum 来检测是否满足 input path sum 条件
- 满足的时候add to result list
- 两种backtracking:
- 1. backtrack 当下node, 加进list, 然后dfs. dfs结束后删掉之前加进去的元素. 非常clean.
- 2. backtrack 下一个dfs level增加的value. dfs return 之后, 删掉list里面的末尾元素: 但是删掉的dfs余下的value.
- 第一种backtrack更加好掌握.

#### Previous Notes:
- Binary Tree的一个基本题: 找到所有满足条件的path
- 遍历到底，比较sum vs. target
- 注意divide的情况。要把遍历的例子写写



---

**16. [Combinations.java](https://github.com/awangdev/LintCode/blob/master/Java/Combinations.java)**      Level: Medium
      

Given two integers n and k, return all possible combinations of k numbers out of 1 ... n.

#### DFS, Backtracking
- for loop, recursive (dfs).
- 每个item用一次, 下一个level dfs(index + 1)
- Combination DFS. 画个图想想. 每次从1~n里面pick一个数字i
- 因为下一层不能重新回去 [0~i]选，所以下一层recursive要从i+1开始选。



---

**17. [Combination Sum.java](https://github.com/awangdev/LintCode/blob/master/Java/Combination%20Sum.java)**      Level: Medium
      

给一串数字candidates (no duplicates), 和一个target. 

找到所有unique的 组合(combination) int[], 要求每个combination的和 = target.

注意: 同一个candidate integer, 可以用任意多次.


#### DFS, Backtracking
- 考虑input: 没有duplicate, 不需要sort
- 考虑重复使用的规则: 可以重复使用, 那么for loop里面dfs的时候, 使用curr index
- the result is trivial, save success list into result.

##### Combination DFS 思想
- 在每个index上面都要面临: pick/not pick的选择
- 每次pick以后, 就生成一条新的routine, from this index
- 下一个level的dfs从这个index开始, 对后面(或者当下/if allow index reuse) 进行同样的 pick/not pick 的选择
- 注意1: 每个level dfs 里面, for loop 里会有 end condition: 就不必要dfs下去了.
- 注意2: Backtracking在success case && dfs case 后都要做, 因为backtrack 是为了之前上一层dfs.




---

**18. [Combination Sum II.java](https://github.com/awangdev/LintCode/blob/master/Java/Combination%20Sum%20II.java)**      Level: Medium
      

给一串数字candidates (can have duplicates), 和一个target. 

找到所有unique的 组合(combination) int[], 要求每个combination的和 = target.

注意: 同一个candidate integer, 只可以用一次.

#### DFS, Backtracking
- when the input has duplicates, and want to skip redundant items? 
- 1. sort. 2. in for loop, skip same neighbor.
- 考虑input: 有duplicate, 必须sort
- 考虑重复使用的规则: 不可以重复使用
- 1. for loop里面dfs的时候, 使用curr index + 1
- 2. for loop里面, 同一个level, 同一个数字, 不能重复使用: `(i > index && candidates[i] == candidates[i - 1]) continue`
- 因为在同一个level里面重复的数字在下一个dfs level里面是会被考虑到的, 这里必须skip (这个就记住吧)
- the result is trivial, save success list into result.




---

**19. [Combination Sum III.java](https://github.com/awangdev/LintCode/blob/master/Java/Combination%20Sum%20III.java)**      Level: Medium
      

给一个integer k, 和一个target n. 

从positive数字[1 ~ 9], 找到所有unique的 组合(combination) int[], size = k, 要求每个combination的和 = n.

(隐藏条件, 需要clarify): 同一个candidate integer [1 ~ 9], 只可以用一次.

#### DFS, Backtracking
- 跟Combination Sum I, II 没什么太大区别, 只不过, 一定要用k个数字, 也就是一个for loop里面的特别条件
- 考虑input: 没有重复数字 [1 ~ 9]
- 考虑candidate重复利用: 不可以重复利用, next level dfs 时候, curr index + 1
- the result is trivial, save success list into result.



---

**20. [Subset.java](https://github.com/awangdev/LintCode/blob/master/Java/Subset.java)**      Level: Medium
      

给一串unique integers, 找到所有可能的subset. result里面不能有重复.

#### DFS
- dfs的两种路子: 1. pick&&skip dfs, 2. for loop dfs
- 1. pick&&skip dfs: 取或者不取 + backtracking. 当level/index到底，return 一个list.
- 2. for loop dfs: for loop + backtracking. 记得：做subset的时候, 每个dfs recursive call是一种独特可能，先加进rst。
- Time&&space: subset means independent choice of either pick&&not pick. You pick n times: O(2^n), 3ms

#### Bit Manipulation
- n = nums.length, 那么在每一个index, 都是 pick / not pick: 0/1
- 考虑subset index 0/1的bit map: range 的就是 [0000...00 ~ 2^n-1]
- 每一个bitmap就能展现出一个subset的内容: all the 1 represents picked indexes
- 做法:
- 1. 找出Range
- 2. 遍历每一个bitmap candidate
- 3. 对每一个integer 的 bit representation 遍历, 如果是1, add to list
- time: O(2^n * 2^n) = O(4^n), still 3ms, fast.

#### Iterative, BFS
- Regular BFS, 注意考虑如果让one level to generate next level
- 1. 用queue来存每一次的candidate indexes
- 2. 每一次打开一层candiates, add them all to result
- 3. 并且用每一轮的candidates, populate next level, back into queue.
- should be same O(2^n), but actual run time 7ms, slower





---

**21. [Subsets II.java](https://github.com/awangdev/LintCode/blob/master/Java/Subsets%20II.java)**      Level: Medium
      

给一串integers(may have duplicates), 找到所有可能的subset. result里面不能有重复.

#### DFS
- DFS, 找准需要pass along的几个数据结构. 先sort input, 然后DFS
- Using for loop approach: 每个dfs call是一种可能性，直接add into result.     
- 为了除去duplicated result, skip used item at current level: `if (i > depth && nums[i] == nums[i - 1]) continue;`
- srot O(nlogn), subset: O(2^n)

#### BFS
- Regular BFS, 注意考虑如果让one level to generate next level
- skip duplicate: `if (i > endIndex && nums[i] == nums[i - 1]) continue;`
- 1. 用queue来存每一次的candidate indexes
- 2. 每一次打开一层candiates, add them all to result
- 3. 并且用每一轮的candidates, populate next level, back into queue.
- srot O(nlogn), subset: O(2^n)
- should be same O(2^n). slower than dfs

#### Previous notes:
- 在DFS种skip duplicate candidates, 基于sorted array的技巧：    
- 一旦for loop里面的i!=index，并且nums[i] == nums[i-1],
- 说明x=nums[i-1]已经在curr level 用过，不需要再用一次: [a,x1,x2]，x1==x2    
- i == index -> [a,x1]    
- i == index + 1 -> [a,x2]. 我们要skip这一种
- 如果需要[a,x1,x2]怎么办？ 其实这一种在index变化时，会在不同的两个dfs call 里面涉及到。

#### 注意
- 不能去用result.contains(), 这本身非常costly O(nlogn)




---




 
 
 
## Double Recursive (2)
**0. [Binary Tree Longest Consecutive Sequence II.java](https://github.com/awangdev/LintCode/blob/master/Java/Binary%20Tree%20Longest%20Consecutive%20Sequence%20II.java)**      Level: Medium
      

找到binary tree 里的最长 consecutive sequence. Sequence可以递增递减, Sequence顺序可以回溯parent.

#### DFS
- Similar to Binary Tree Longest Consecutive Sequence I
- 只不过可以递增递减, 还有连接上parent的方向.
- 对于任何一个节点, 都可能: 
- 1. 自己跟两个child链接, 成为一个sequence
- 2. 左边孩子, 右边孩子各自是一个consecutive sequence, 但是不跟root相连
- main function 一开始就divide成这三份, 然后dfs
- dfs take diff == 1, diff == -1, 来做递增递减的校对.
- dfs rules:
- 1. if node == null, leaf depth = 0
- 2. if not consecutive, reset the depth = 0 (same for both left child, and right child)
- 3. compare the leftDepth && rightDepth to find the maximum
- 4. diff is the same in the same dfs loop to maintain consistant increase/decrease

##### 注意
- dfs的结果很可能是0, 如果没有任何结果, 那么上一层的caller depth = dfs() + 1 = 1
- 那么回归到root, dfs的结果很可能就是1.
- 可能会问: 那么在tree里面的partial sequence (不连接到root)的被忽略了?
- 这里 `longestConsecutive(root.left)` 就很重要了
- 这一步特地忽略掉了root, 然后走下去一层: 因为是recursive, 所以还会继续divde && conquer
- 最后, 任何一层的孩子都会被照顾到.



---

**1. [Path Sum III.java](https://github.com/awangdev/LintCode/blob/master/Java/Path%20Sum%20III.java)**      Level: Easy
      

count所有存在的 path sum == target sum. 可以从任意点开始. 但是只能parent -> child .

#### DFS
- 对所给的input sum 做减法, 知道 sum 达到一个目标值截止
- 因为可以从任意点开始, 所以当sum达标时候, 需要继续recursive, 从而找到所有情况 (有正负数, sum可能继续增加/减少)
- 经典的 helper dfs recursive + self recursive
- 1. helper dfs recursive 处理包括root的情况
- 2. self recursive 来引领  skip root的情况.

#### 特点
- 与 `Binary Tree Longest Consecutive Sequence II` 在recursive的做法上很相似: 
- 利用dfs做包括root的recursive computation
- 利用这个function自己, 做不包括root的recursive computation



---




 
 
 
## Combination (4)
**0. [Combinations.java](https://github.com/awangdev/LintCode/blob/master/Java/Combinations.java)**      Level: Medium
      

Given two integers n and k, return all possible combinations of k numbers out of 1 ... n.

#### DFS, Backtracking
- for loop, recursive (dfs).
- 每个item用一次, 下一个level dfs(index + 1)
- Combination DFS. 画个图想想. 每次从1~n里面pick一个数字i
- 因为下一层不能重新回去 [0~i]选，所以下一层recursive要从i+1开始选。



---

**1. [Combination Sum.java](https://github.com/awangdev/LintCode/blob/master/Java/Combination%20Sum.java)**      Level: Medium
      

给一串数字candidates (no duplicates), 和一个target. 

找到所有unique的 组合(combination) int[], 要求每个combination的和 = target.

注意: 同一个candidate integer, 可以用任意多次.


#### DFS, Backtracking
- 考虑input: 没有duplicate, 不需要sort
- 考虑重复使用的规则: 可以重复使用, 那么for loop里面dfs的时候, 使用curr index
- the result is trivial, save success list into result.

##### Combination DFS 思想
- 在每个index上面都要面临: pick/not pick的选择
- 每次pick以后, 就生成一条新的routine, from this index
- 下一个level的dfs从这个index开始, 对后面(或者当下/if allow index reuse) 进行同样的 pick/not pick 的选择
- 注意1: 每个level dfs 里面, for loop 里会有 end condition: 就不必要dfs下去了.
- 注意2: Backtracking在success case && dfs case 后都要做, 因为backtrack 是为了之前上一层dfs.




---

**2. [Combination Sum II.java](https://github.com/awangdev/LintCode/blob/master/Java/Combination%20Sum%20II.java)**      Level: Medium
      

给一串数字candidates (can have duplicates), 和一个target. 

找到所有unique的 组合(combination) int[], 要求每个combination的和 = target.

注意: 同一个candidate integer, 只可以用一次.

#### DFS, Backtracking
- when the input has duplicates, and want to skip redundant items? 
- 1. sort. 2. in for loop, skip same neighbor.
- 考虑input: 有duplicate, 必须sort
- 考虑重复使用的规则: 不可以重复使用
- 1. for loop里面dfs的时候, 使用curr index + 1
- 2. for loop里面, 同一个level, 同一个数字, 不能重复使用: `(i > index && candidates[i] == candidates[i - 1]) continue`
- 因为在同一个level里面重复的数字在下一个dfs level里面是会被考虑到的, 这里必须skip (这个就记住吧)
- the result is trivial, save success list into result.




---

**3. [Combination Sum III.java](https://github.com/awangdev/LintCode/blob/master/Java/Combination%20Sum%20III.java)**      Level: Medium
      

给一个integer k, 和一个target n. 

从positive数字[1 ~ 9], 找到所有unique的 组合(combination) int[], size = k, 要求每个combination的和 = n.

(隐藏条件, 需要clarify): 同一个candidate integer [1 ~ 9], 只可以用一次.

#### DFS, Backtracking
- 跟Combination Sum I, II 没什么太大区别, 只不过, 一定要用k个数字, 也就是一个for loop里面的特别条件
- 考虑input: 没有重复数字 [1 ~ 9]
- 考虑candidate重复利用: 不可以重复利用, next level dfs 时候, curr index + 1
- the result is trivial, save success list into result.



---




 
 
 
## Sort (11)
**0. [Wiggle Sort.java](https://github.com/awangdev/LintCode/blob/master/Java/Wiggle%20Sort.java)**      Level: Medium
      

方法1:
排序, nLog(n). 然后把直线上坡变成层叠山峰, 需要每隔几个(题目中是每隔2位)就做个swap 造成高低不平.
Note: 每隔山峰之间是相互没有关系的, 所以每次只要操心 [i], [i-1]两个位置就好了.

方法2:
O(n)
看好奇数偶数位的规律, 然后根据题目给出的规律, 跑一遍, 每次只关注两个位置: 把不合适的[i], [i-1]调换位置就好了.

方法3:
跟法2一样, 只是更巧妙一点罢了:
第一遍想太多. 其实做一个fall-through就能把问题解决，原因是因为：
这样的fall-through每次在乎两个element，可以一口气搞定，无关乎再之前的elements。
特别的一点：flag来巧妙的掌控山峰和低谷的变化。又是神奇的一幕啊！
这样子的奇观，见过就要知道了，没见过的时候有点摸不着头脑。



---

**1. [Intersection of Two Arrays II.java](https://github.com/awangdev/LintCode/blob/master/Java/Intersection%20of%20Two%20Arrays%20II.java)**      Level: Easy
      

方法1:
用HashMap: 存一个nums1, 再拿nums2 check against map. 时间/空间:O(n)

方法2:
Binary search? 需要array sorted. 否则时间O(nlogn)不值得.
[没做完, 有错]



---

**2. [Valid Anagram.java](https://github.com/awangdev/LintCode/blob/master/Java/Valid%20Anagram.java)**      Level: Easy
      

HashMap



---

**3. [Meeting Rooms.java](https://github.com/awangdev/LintCode/blob/master/Java/Meeting%20Rooms.java)**      Level: Easy
      

- 注意接头点要考虑所有开会结会的情况，不要恰巧漏掉相接的点
- 开会的是超人。瞬间移动接上下一个会议

#### 方法1:
找是否有overlap. priorityQueue 按照start time排序好以后, 比较current和peek: current.end > peek.start?

#### 方法2: Sweep line
- class Point{pos, flag}, PriorityQueue排序。计算count
- 跟 Number of Airplanes in the Sky 是一个类型的题目





---

**4. [Number of Airplane in the sky.java](https://github.com/awangdev/LintCode/blob/master/Java/Number%20of%20Airplane%20in%20the%20sky.java)**      Level: Medium
      

#### Sweep Line
- 把Interval拆分成数轴上的Point 
- 起飞mark 1   
- 降落mark -1     
- 用PriorityQueue排序， loop through queue, 计算(起飞+降落)值可能有的max。

#### 注意
- 同时起飞和降落，就是 1 - 1 = 0. 所以在while loop里面有第二个while loop，    
- 当坐标x重合时，在这里做完所有x点的加减，然后再比较 max。     
- 这避免了错误多count，或者少count



---

**5. [Meeting Rooms II.java](https://github.com/awangdev/LintCode/blob/master/Java/Meeting%20Rooms%20II.java)**      Level: Medium
      

给一串数字pair, 代表会议的开始/结束时间. 找同时又多少个会议发生(需要多少件房间)

#### 方法1
- PriorityQueue + 一个Class来解决.Ｏ(nlogn)
- 跟 Number of Airpline in the sky是同一道题

#### 方法2: 尝试了一下用一个sorted Array + HashMap
也还行，但是handle edge的时候,HashMap 要小心，因为相同时间start和end的map key 就会重复了。



---

**6. [Insertion Sort List.java](https://github.com/awangdev/LintCode/blob/master/Java/Insertion%20Sort%20List.java)**      Level: Medium
      

input一串数字, 需要出sorted output. 每次insert一个数字时, 都要放到正确的sorted的位置

每次insertion的时候, 都从input里面减掉这个数字

#### Linked List
- 把list里面每个元素都拿出来，scan and insert一遍
- Time O(n^2), worst case, 每次放入n个数字里面的element, 刚好都是最大的
- 所以每次要traverse n nodes, 然后走n次

##### 思考方法
- 如果已经有个sorted list, insert一个element进去。怎么做？
- while 里面每个元素都小于 curr, keep going
- 一旦curr在某个点小了，加进去当下这个空隙。



---

**7. [Largest Number.java](https://github.com/awangdev/LintCode/blob/master/Java/Largest%20Number.java)**      Level: Medium
      

给一串数字, 非负数, 把所有数字串联起来, 组成最大数字.

因为结果很大, 所以用string表示 

#### Sort, Comparator
- 考虑 more significant spot 应该拿到更大的值
- 如果sort number,  comparator 会比较难写: 每个digit的weight不同, 要分别讨论个位数和多位数.
- goal: 让较大的组合数排在前面, 让较小的组合数排在后面
- 不如: 组合两种情况, 用String比较一下大小 (也可以用 integer来比较组合数, 但是为保险不超Integer.MAX_VALUE, 这里比较String)
- String.compareTo() 是按照 lexicographically, 字典顺序排列的
- 利用compareTo, 来倒序排列 string, 刚好就得到我们要的结果.
- O(nlogn), 排序



---

**8. [Merge Intervals.java](https://github.com/awangdev/LintCode/blob/master/Java/Merge%20Intervals.java)**      Level: Medium
      

给一串int[Interval]. 把所以Interval merge起来.

#### Sweep Line
- O(nlogn)         
- 扫描线+Count无敌手。注意start end把interval给合起来。   
- count==0的时候，就是每次start end双数抵消的时候，就应该是一个interval的开头/结尾。写个例子就知道了。   
- 空间：O(2n) -> O(n)   
- 时间,priorityqueue: O(nlogn)   
- 记得怎么写comparator. New way: new PriorityQueue<>(Comparator.comparing(p -> p.val));
- 在 LeetCode里面，Sweep Line比方法2要快很多.

#### Sort Interval 
- Collections.sort() on interval.start之后，试着跑一遍，按照merge的需求，把需要merge的地方续好，然后减掉多余的interval就好。
- (不知为何LeetCode把Merge Interval, Insert Interval 标为Hard)
- Collections.sort(..., new comparator): sort by Interval.start.

- 画两个相连的Interval， prev, curr:
- prev只有 prev.end覆盖了 curr.start， 才需要merge. 那么比较一下, marege.     
- 记得如果merge, 一定要list.remove(i), 并且i--， 因为改变了List的大小。
- 若没有重合，就继续iteration: prev = curr. move on.

#### Sort Intervals and append end logically
- Sort intervals: O(nlogn)
- 找到结尾 interval, 满足条件就可以save
- 如果不到return的条件, 就继续延伸 interval.end



---

**9. [QuickSort.java](https://github.com/awangdev/LintCode/blob/master/Java/QuickSort.java)**      Level: Medium
      

implement quick sort.

#### Quick Sort
- 首先partition. 返还一个partition的那个中间点的位置: 这个时候, 所有小于nums[partitionIndex] 都应该在 partitionIndex左边
- 然后劈开两半
- 前后各自 quick sort, recursively
- 注意：在partition里面, 比较的时候nums[start] < pivot, nums[end]>pivot, 如果写成了 <= 会 stack overflow.
- Time O(nlogn), Space: O(1)



---

**10. [MergeSort.java](https://github.com/awangdev/LintCode/blob/master/Java/MergeSort.java)**      Level: Medium
      

#### Merge Sort
- Divide and conquer, recursively
- 先从中间分段, merge sort 左边 (dfs), merge sort 右边
- 最后merge起来
- merge的时候因为是做int[], 所以没办法必须要O(n) space
- Time O(nlogn), Space O(n)



---




 
 
 
## Tree (38)
**0. [Unique Binary Search Tree.java](https://github.com/awangdev/LintCode/blob/master/Java/Unique%20Binary%20Search%20Tree.java)**      Level: Medium
      

Not quite clear.
根据左右分割而总结出了原理, 每次分割, 左右两边都会有一定数量的permutation, 总体上的情况数量当然是相乘.
然后每一个不同的分割点都加一遍:
f(n) = f(0)*f(n-1) + f(1)*f(n-2) + ... + f(n-2)*f(1) + f(n-1)*f(0)

然后把数学公式转换成DP的方程, 有点玄学的意思啊! 不好想.



---

**1. [Trim a Binary Search Tree.java](https://github.com/awangdev/LintCode/blob/master/Java/Trim%20a%20Binary%20Search%20Tree.java)**      Level: Easy
      

方法1:
适合复习BST. 用DFS对待每个node. 注意BST的特征: 所有left nodes都小于当下node, 所有right nodes都大于当下node.

根据题意用[L,R]切割.如果node.val<L, 直接连node带左边全丢掉, return node.right. 处理R也是一样.
分制是, DFS leftNode, rightNode. 然后接在node.left, node.right.

方法2: 用迭代, 还没有写.



---

**2. [Binary Search Tree Iterator.java](https://github.com/awangdev/LintCode/blob/master/Java/Binary%20Search%20Tree%20Iterator.java)**      Level: Medium
      

画一下, BST in order traversal. 用stack记录最小值, 放在top. O(h) space.
每次消耗TreeNode, 都看看rightNode(其实就是下一个最小的candidate), 并且一条龙stack叠上rightNode所有的left子孙.

Previous Notes:
用O(h)空间的做法：

理解binary search tree inorder traversal的规律：
   先找left.left.left ....left 到底，这里是加进stack.
   然后考虑parent,然后再right.

例如这题：
   stack里面top，也就是tree最左下角的node先考虑,取名rst.
   其实这个rst拿出来以后, 它也同时是最底层left null的parent，算考虑过了最底层的parent。
   最后就考虑最底层的parent.right, 也就是rst.right.

注意:
   next()其实有个while loop, 很可能是O(h).题目要求average O(1),所以也是okay的.


用O(1)空间的做法：不存stack, 时刻update current为最小值。

找下一个最小值,如果current有right child：   
   和用stack时的iteration类似,那么再找一遍current.right的left-most child,就是最小值了。
   
如果current没有right child:    
    那么就要找current node的右上parent, search in BinarySearchTree from root.

注意：
   一定要确保找到的parent满足parent.left == current.
   反而言之，如果current是parent的 right child, 那么下一轮就会重新process parent。
   但是有错:binary search tree里面parent是小于right child的，也就是在之前一步肯定visit过，如此便会死循环。




---

**3. [Same Tree.java](https://github.com/awangdev/LintCode/blob/master/Java/Same%20Tree.java)**      Level: Easy
      

给两个 binary tree, 看两个tree是否identical.

#### DFS
- DFS. 确定leaf条件, && with all dfs(sub1, sub2).
- 这里无论如何都要走过所有的node, 所以dfs更加合适, 好写.

#### BFS
- 两个queue存每个tree的所有current level node. Check equality, check queue size.
- Populate next level by nodes at current level.



---

**4. [Convert Sorted Array to Binary Search Tree.java](https://github.com/awangdev/LintCode/blob/master/Java/Convert%20Sorted%20Array%20to%20Binary%20Search%20Tree.java)**      Level: Easy
      

如题

#### DFS
- Binary Search Tree特点: 左边的node都比右边的node小. 
- 如果要height相差<1, 必须左右sub tree均分. 做DFS(num, start, end)
- 在每一个level, 找到中间点, 然后分割2办, 继续dfs
- Divide and Conquer



---

**5. [Construct Binary Tree from Inorder and Preorder Traversal.java](https://github.com/awangdev/LintCode/blob/master/Java/Construct%20Binary%20Tree%20from%20Inorder%20and%20Preorder%20Traversal.java)**      Level: Medium
      

如题

#### DFS
- 和Construct from Inorder && Postorder 想法一样。
- 写出Preorder和Inorder的字母例子，发现Preorder的开头总是这Level的root。依此写helper,注意处理index。
- 跟Convert Sorted Array to Binary Tree类似, 找到对应的index, 然后:
- node.left = dfs(...), node.right = dfs(...)
- Divide and Conquer



---

**6. [Balanced Binary Tree.java](https://github.com/awangdev/LintCode/blob/master/Java/Balanced%20Binary%20Tree.java)**      Level: Medium
      

给一个binary tree, 看是否是height-balanced

#### DFS
- DFS using depth marker: 每个depth都存一下。然后如果有不符合条件的，存为-1.
- 一旦有 <0 或者差值大于1， 就全部返回Integer.MIN_VALUE. Integer.MIN_VALUE比较极端, 确保结果的正确性。
- 最后比较返回结果是不是<0. 是<0，那就false.
- Traverse 整个tree, O(n)


#### DFS, maxDepth function
- Same concept as in 1, but cost more traversal efforts.



---

**7. [Populating Next Right Pointers in Each Node.java](https://github.com/awangdev/LintCode/blob/master/Java/Populating%20Next%20Right%20Pointers%20in%20Each%20Node.java)**      Level: Medium
      

给一个特殊的binary tree, treeNode里面有一个 next pointer.

写一个function, 把所有node都更同level的node 连在一起. 最右边的node.next = NULL

#### DFS
- 题目要求DFS. 想清楚了如何在DFS level把几种情况都考虑了, 写起来很简单.
- 对于一个root来说, 只有几个点可以顾忌到: root.left, root.right, root.next. 
- 想办法把这三个方向的点, 能连起来的都连起来:
- 1. node.left.next = node.right
- 2. If node.next != null, link node.right.next = node.next.left;
- 然后在dfs(root.left), dfs(root.right)

#### BFS
- 不和题意，用了queue space，与Input成正比。太大。
- BFS over Tree。 用Queue 和 queue.size()，老规矩。   
- process每层queue时, 注意把next pointer加上去就好. 



---

**8. [Validate Binary Search Tree.java](https://github.com/awangdev/LintCode/blob/master/Java/Validate%20Binary%20Search%20Tree.java)**      Level: Medium
      

如题, 验证是否是BST.

#### DFS
- 查看每个parent-child关系: leftchild < root < rightChild
- 方法: 把root.val 传下来作为 max 或者 min, 然后检查children

##### Note: 
- min/max需要时long type. 
- 如果题目真的给node.val = Integer.MAX_VALUE, 我们需要能够与之比较, long就可以.



---

**9. [Maximum Binary Tree.java](https://github.com/awangdev/LintCode/blob/master/Java/Maximum%20Binary%20Tree.java)**      Level: Medium
      

给一串数字, 做一个 maximum binary tree: 最顶上的root最大; 左child也是一个max tree, 右child也必须是max tree.

#### Monotonous Stack
- 用到bottom->top递减的stack: 最底下的root维持成最大的element.
- 过程当中, 一旦遇到currNode.val > stack.peek(), 就意味着需要把这个currNode放在 stack的底层位置.
- 也就是说, 遇到这个条件, process, pop()所有 currNode.val > stack.peek(), 最后把currNode加进去.

- maxTree题目本身的要求是: 大的在最中间, 左右两边的subTree也要是maxTree:
- Monotonous Stack在这里帮助 keep/track of max value, 但是left/right tree的logic是MaxTree独有的.
- left/right node的assignment是根据题目要求: 中间最大值分开后, 左边的是左边subTree, 右边的作为右边subTree.

#### Previous notes
- Should memorize MaxTree. 依次类推，会做Min-Tree, Expression Tree
- Stack里，最大的值在下面。利用此性质，有这样几个step:

##### Step1
- 把所有小于curr node的，全Pop出来, while loop, keep it going.    
- 最后pop出的这个小于Curr的node：它同时也是stack里面pop出来小于curr的最大的一个，最接近curr大小。（因为这个stack最大值靠下面）    
- 把这个最大的小于curr的node放在curr.left.    

##### Step2   
- 那么，接下去stack里面的一定是大于curr：   
- 那就变成curr的left parent. set stack.peek().right = curr.

##### Step3   
- 结尾：stack底部一定是最大的那个，也就是max tree的头。





---

**10. [Binary Tree Inorder Traversal.java](https://github.com/awangdev/LintCode/blob/master/Java/Binary%20Tree%20Inorder%20Traversal.java)**      Level: Easy
      

Inorder traverse Binary Tree

#### Recursive
- 在自己的基础上recursive, 不用helper function
- Divide and Conquer, with helper(dfs) method
- O(n) time, no extra space

#### Iterative: Stack
- Add left nodes all the way   
- Print curr   
- Move to right, add right if possible
- O(n) time, O(h) space
  
注意stack.pop()在加完left-most child 的后，一定要curr = curr.right.

若不右移, 很可能发生窘境:
curr下一轮还是去找自己的left-most child，不断重复curr and curr.left, 会infinite loop, 永远在左边上下上下。

#### HashMap
? How?



---

**11. [Binary Tree Postorder Traversal.java](https://github.com/awangdev/LintCode/blob/master/Java/Binary%20Tree%20Postorder%20Traversal.java)**      Level: Medium
      

如题, POST-ORDER traversal.

LeetCode给了hard, 应该是觉得stack的做法比较难想到.

#### Recursive
trivial, 先加left recursively, 再加right recursively, 然后组成头部.

#### Stack
- 双stack的思想, 需要在图纸上画一画
- 原本需要的顺序是: 先leftChild, rightChild, currNode.
- 营造一个stack, reversely process: 先currNode, 再rightChild, 再leftChild
- 这样出来的结果是reverse的, 那么翻转一下就可以了.
- v1做的时候用了stack1, stack2, 因为根据这个双stack的思想而来
- v2简化, 可以放在一个stack里面, 每次record result 的时候: rst.add(0, item);

##### 利用stack的特点
- 每次加element进stack的时候, 想要在 bottom/后process的, 先加
- 想要下一轮立刻process的, 最后push进stack.

##### 注意
这些binary tree traversal的题目.常常有多个做法:recursive or iterative



---

**12. [Closest Binary Search Tree Value.java](https://github.com/awangdev/LintCode/blob/master/Java/Closest%20Binary%20Search%20Tree%20Value.java)**      Level: Easy
      

给一个BST, 和一个double target, 走位找到最接近的number.

#### Recursive
- when less than curr val, consider left
- when greater than curr val, consider right
- dfs到底, 然后每一层比较, 再return

#### Binary Search
- 记录找到过的closest
- Binary Search, 根据current node走位,
- 找到 node.val == target, 或者走位走完, return closest



---

**13. [Count Complete Tree Nodes.java](https://github.com/awangdev/LintCode/blob/master/Java/Count%20Complete%20Tree%20Nodes.java)**      Level: Medium
      

Complete Tree就是说, 最后一个level可能是缺node的(不是说最右下角缺node, 别忘了!)

#### DFS + Optimization
- 每次看最左left depth和最右leaf depth 是不是一样, 如果一样, 直接 2 ^ h - 1就好
- 不一样的话, 再DFS

##### Trick
- 直接DFS会timeout, O(n), 其实可以optimize
- to pass the test with O(h^2), 位运算: Math.pow(2, h) = 2 << (h - 1). 神奇!
- 2 << 1就是把所有bits往左移动一位, 也就是 * 2 

#### Iteratively
- See details in comments inline. 要对tree非常理解
- binary tree one child tree nodes # = 2 ^ h - 1; 所以一个child tree + root = 2 ^ h



---

**14. [Binary Tree Preorder Traversal.java](https://github.com/awangdev/LintCode/blob/master/Java/Binary%20Tree%20Preorder%20Traversal.java)**      Level: Easy
      

#### Recursive
- 加root, left, then right. Obvious
- Divide and conquer
- 其实也不需要helper function

#### Iterative
- 先加root, 然后push上需要末尾process的在stack垫底(root.right), 然后push root.left
- Stack: push curr, push right, push left.   



---

**15. [Complete Binary Tree.java](https://github.com/awangdev/LintCode/blob/master/Java/Complete%20Binary%20Tree.java)**      Level: Easy
      

A complete binary tree is a binary tree in which every level, except possibly the last,

is completely filled, and all nodes are as far left as possible

#### BFS
- 当出现了第一次有 null children的node的时候, 说明到了leaf level, mark flag = true;
- 自此以后，queue再不该有node再有child; queue后面出现的node的left/right child应该都是null
- 否则就是有问题, return false;




---

**16. [House Robber III.java](https://github.com/awangdev/LintCode/blob/master/Java/House%20Robber%20III.java)**      Level: Medium
      

Houses被arrange成了binary tree, 规则还是一样, 连续相连的房子不能同时抄.

求Binary Tree neighbor max 能抄多少.

#### DFS
- 判断当下的node是否被采用，用一个boolean来表示. 
- 如果curr node被采用，那么下面的child一定不能被采用.
- 如果curr node不被采用，那么下面的children有可能被采用，但也可能略过，所以这里用Math.max() 比较一下两种可能有的dfs结果。
- dfs重复计算:每个root都有4种dive in的可能性, 假设level高度是h, 那么时间O(4^(h)), where h = logN, 也就是O(n^2)

#### DP, DFS
- 并不是单纯的DP, 是在发现DFS很费劲后, 想能不能代替一些重复计算?
- 基本思想是dfs解法一致: 取root找最大值, 或者不取root找最大值
- 在root上DFS, 不在dfs进入前分叉; 每一个level按照状态来存相应的值: dp[0] root not picked, dp[1] root picked.
- Optimization: DP里面, 一口气找leftDP[]会dfs到最底层, 然后自下向上做计算
- 这个过程里面, 因为没有在外面给dfs()分叉, 计算就不会重叠, 再也不用回去visit most-left-leaf了, 算过一遍就完事.
- 然而, 普通没有dp的dfs, 在算完visited的情况下的dfs, 还要重新dfs一遍!visited的情况.
- Space O(h), time O(n), 或者说是O(2^h), where h = log(n)

#### DP 特点
- 不为状态而分叉dfs
- 把不同状态model成dp
- 每一个dfs都return一个based on status的 dp array.
- 等于一次性dfs计算到底, 然后back track, 计算顶部的每一层.
- DP 并不一定要是以n为base的. 也可以是局部的去memorize状态->value.



---

**17. [Invert Binary Tree.java](https://github.com/awangdev/LintCode/blob/master/Java/Invert%20Binary%20Tree.java)**      Level: Easy
      

#### DFS
- 简单处理swap
- recursively swap children

#### BFS
- BFS with Queue
- 每次process一个node, swap children; 然后把child加进queue里面
- 直到queue process完



---

**18. [Maximum Depth of Binary Tree.java](https://github.com/awangdev/LintCode/blob/master/Java/Maximum%20Depth%20of%20Binary%20Tree.java)**      Level: Easy
      

给一个binary tree, 找最深depth

#### DFS
- 这里要走过所有的node, 所以dfs非常合适
- Divide and conquer. 
- 维持一个最大值: Math.max(maxDepth(root.left), maxDepth(root.right)) + 1;
- 注意check root == null



---

**19. [Minimum Depth of Binary Tree.java](https://github.com/awangdev/LintCode/blob/master/Java/Minimum%20Depth%20of%20Binary%20Tree.java)**      Level: Easy
      

#### DFS
- Divide and Conquery一个最小值. 
- 注意处理Leaf的null: null leaf 出现的时候, 就忽略这个leaf, 直接return算有leaf
- 另一种count的方法: 用Integer.MAX_VALUE代替 null leaf，这样可以避免错误counting. (不能直接recursive)
- 这个无论如何都要走所有node, 所以dfs应该比较适合.

#### BFS
- 还没做



---

**20. [Symmetric Tree.java](https://github.com/awangdev/LintCode/blob/master/Java/Symmetric%20Tree.java)**      Level: Easy
      

检查tree是否symmetric

注意Symmetric Binary Tree的例子和定义: 是镜面一样的对称. 并不是说左右两个sub-tree相等。

#### DFS
- Recursively check symmetrically相对应的Node.  
- 每个node的children都和镜面另外一边相对的node的children刚好成镜面反射位置。

#### Stack
- stack1: 左手边sub-tree先加left, 再加right child; 
- stack2: 右手边sub-tree先加right child, 再加left child。   
- process时，若symmetric，所有stack里面出来的node会一一对应。



---

**21. [Tweaked Identical Binary Tree.java](https://github.com/awangdev/LintCode/blob/master/Java/Tweaked%20Identical%20Binary%20Tree.java)**      Level: Easy
      

检查binary tree是否 identical. 

特点: subtree如果是有旋转的, 只要tree node value相等, 就可以算是identical

#### DFS
- 在DFS的基础上, 比对左左,左右,右左,右右



---

**22. [Merge Two Binary Trees.java](https://github.com/awangdev/LintCode/blob/master/Java/Merge%20Two%20Binary%20Trees.java)**      Level: Easy
      

#### DFS
- 基础binary tree traversal. 注意对null child的判断



---

**23. [Subtree.java](https://github.com/awangdev/LintCode/blob/master/Java/Subtree.java)**      Level: Easy
      

给一个binary tree s, 和一个binary tree t, 检查t是不是s的subtree.

#### DFS
- 跟 identical binary tree的写法很像
- 只有 current s.val = t.val 的时候才需要compare same tree.
- 其他情况, 继续recursively isSubtree
- 注意：即使找到T1 == T2, 但很可能只是数字相同（这里不是binary search tree!!）, 而children不同
- 所以同时要继续recursively isSubtree(T1.left, T2) ...etc.



---

**24. [Lowest Common Ancestor of a Binary Tree.java](https://github.com/awangdev/LintCode/blob/master/Java/Lowest%20Common%20Ancestor%20of%20a%20Binary%20Tree.java)**      Level: Medium
      

给一个Binary Tree root, 以及两个node p, q. 找 p 和 q 的 lowest common ancestor

#### DFS
- 因为是 binary tree, 所以直接盲目搜索搜索path不efficient. 巧用DFS来找每一个node的common ancestor
- 当root == null或者 p q 任何一个在findLCA底部被找到了(root== A || root == B)，那么就return 这个root.     
- 三种情况:
- 1. A,B都找到，那么这个level的node就是其中一层的ancestor: 其实，最先recursively return到的那个，就是最底的LCA parent.   
- 2. A 或者 B 找到，那就还没有公共parent, return 非null得那个。   
- 3. A B 都null, 那就找错了没有呗, return null
- Worst case, visit all nodes to find p q at last level, last two leaves: time/space O(n)



---

**25. [Lowest Common Ancestor II.java](https://github.com/awangdev/LintCode/blob/master/Java/Lowest%20Common%20Ancestor%20II.java)**      Level: Easy
      

给一个Binary Tree root, 以及两个node A, B. 特点: node里面存了parent pointer. 找 lowest common ancestor


#### Hash Set
- 这个题有个奇葩的地方, 每个node还有一个parent, 所以可以自底向上.
- save visited in hashset. 第一个duplicate, 就是A B 的 lowest common ancestor

#### Save in lists
- 自底向上。利用parent往root方向返回
- 把所有parent存下来, 然后在两个list里面找最后一个 common node

#### 注意
- 无法从root去直接搜target node 而做成两个list. 因为根本不是Binary Search Tree！




---

**26. [Lowest Common Ancestor of a Binary Search Tree.java](https://github.com/awangdev/LintCode/blob/master/Java/Lowest%20Common%20Ancestor%20of%20a%20Binary%20Search%20Tree.java)**      Level: Medium
      

给 binary search tree root, q node, p node. 找到p q 的lowest common ancestor

#### Find path with BST
- 利用 BST 的性质，可以直接搜到target node，而做成两个长度不一定相等的list
- 然后很简单找到LCA 

#### DFS
- Brutly寻找p和q的common ancestor, 然后recursively drive left/right
- 非常巧妙, 但是也比较局限; 稍微变条件, 就很难recursive.
- 几种情况:
- 1. one of p, q 在leaf, 那么此时的root其实就是lowest common ancestor
- 2. 如果p, q 在root的左右两边, 这就是分叉口, 那么root就是lowest common ancestor
- 3. 如果p,q 在root的同一边 (左,右), 那么继续dfs



---

**27. [Binary Tree Level Order Traversal.java](https://github.com/awangdev/LintCode/blob/master/Java/Binary%20Tree%20Level%20Order%20Traversal.java)**      Level: Medium
      

如题.

#### BFS
- 最普通,Non-recursive: BFS, queue, 用个queue.size()来end for loop:换行。   
- 或者用两个queue. 当常规queue empty，把backup queue贴上去

#### DFS
- 每个level都应该有个ArrayList. 那么用一个int level来查看：是否每一层都有了相应的ArrayList。   
- 如果没有，就加上一层。    
- 之后每次都通过DFS在相应的level上面加数字。




---

**28. [Binary Tree Level Order Traversal II.java](https://github.com/awangdev/LintCode/blob/master/Java/Binary%20Tree%20Level%20Order%20Traversal%20II.java)**      Level: Medium
      

如题, 但是output要倒序.

#### BFS
- 跟Binary Tree Level Order Traversal一样,只不过存result一直存在存在0位.


#### DFS
- 根据level来append每个list
- rst里面add(0,...)每次都add在list开头



---

**29. [Binary Tree Longest Consecutive Sequence II.java](https://github.com/awangdev/LintCode/blob/master/Java/Binary%20Tree%20Longest%20Consecutive%20Sequence%20II.java)**      Level: Medium
      

找到binary tree 里的最长 consecutive sequence. Sequence可以递增递减, Sequence顺序可以回溯parent.

#### DFS
- Similar to Binary Tree Longest Consecutive Sequence I
- 只不过可以递增递减, 还有连接上parent的方向.
- 对于任何一个节点, 都可能: 
- 1. 自己跟两个child链接, 成为一个sequence
- 2. 左边孩子, 右边孩子各自是一个consecutive sequence, 但是不跟root相连
- main function 一开始就divide成这三份, 然后dfs
- dfs take diff == 1, diff == -1, 来做递增递减的校对.
- dfs rules:
- 1. if node == null, leaf depth = 0
- 2. if not consecutive, reset the depth = 0 (same for both left child, and right child)
- 3. compare the leftDepth && rightDepth to find the maximum
- 4. diff is the same in the same dfs loop to maintain consistant increase/decrease

##### 注意
- dfs的结果很可能是0, 如果没有任何结果, 那么上一层的caller depth = dfs() + 1 = 1
- 那么回归到root, dfs的结果很可能就是1.
- 可能会问: 那么在tree里面的partial sequence (不连接到root)的被忽略了?
- 这里 `longestConsecutive(root.left)` 就很重要了
- 这一步特地忽略掉了root, 然后走下去一层: 因为是recursive, 所以还会继续divde && conquer
- 最后, 任何一层的孩子都会被照顾到.



---

**30. [Binary Tree Maximum Path Sum.java](https://github.com/awangdev/LintCode/blob/master/Java/Binary%20Tree%20Maximum%20Path%20Sum.java)**      Level: Hard
      

找max path sum,  可以从任意treeNode 到任意 treeNode.

#### DFS, PathSum object
- that just solves everything


---

**31. [Path Sum.java](https://github.com/awangdev/LintCode/blob/master/Java/Path%20Sum.java)**      Level: Easy
      

给一个inputSum, 然后dfs, 找到是否有一条path, 得出的path sum 跟 inputSum 一样.

#### DFS
- 确定好结尾的条件: is leaf && val == sum
- 每一层减掉node.val, 然后dfs.
- 写一写: root == null => false 对parent nodes的影响. 这里发现没影响, 所以可以简化成用1个functionDFS.




---

**32. [Path Sum II.java](https://github.com/awangdev/LintCode/blob/master/Java/Path%20Sum%20II.java)**      Level: Easy
      

给一个inputSum, 然后dfs, 找到所有path, 满足: path sum 跟 inputSum 一样.

#### DFS, Backtracking
- 用remaining sum 来检测是否满足 input path sum 条件
- 满足的时候add to result list
- 两种backtracking:
- 1. backtrack 当下node, 加进list, 然后dfs. dfs结束后删掉之前加进去的元素. 非常clean.
- 2. backtrack 下一个dfs level增加的value. dfs return 之后, 删掉list里面的末尾元素: 但是删掉的dfs余下的value.
- 第一种backtrack更加好掌握.

#### Previous Notes:
- Binary Tree的一个基本题: 找到所有满足条件的path
- 遍历到底，比较sum vs. target
- 注意divide的情况。要把遍历的例子写写



---

**33. [Path Sum III.java](https://github.com/awangdev/LintCode/blob/master/Java/Path%20Sum%20III.java)**      Level: Easy
      

count所有存在的 path sum == target sum. 可以从任意点开始. 但是只能parent -> child .

#### DFS
- 对所给的input sum 做减法, 知道 sum 达到一个目标值截止
- 因为可以从任意点开始, 所以当sum达标时候, 需要继续recursive, 从而找到所有情况 (有正负数, sum可能继续增加/减少)
- 经典的 helper dfs recursive + self recursive
- 1. helper dfs recursive 处理包括root的情况
- 2. self recursive 来引领  skip root的情况.

#### 特点
- 与 `Binary Tree Longest Consecutive Sequence II` 在recursive的做法上很相似: 
- 利用dfs做包括root的recursive computation
- 利用这个function自己, 做不包括root的recursive computation



---

**34. [Path Sum IV.java](https://github.com/awangdev/LintCode/blob/master/Java/Path%20Sum%20IV.java)**      Level: Medium
      

给一串3-digit 的数组. 每个数字的表达一个TreeNode, 3 digit分别代表: depth.position.value

这串数字已经从小到大排列. 求: 所有可能的 root->leaf path 的所有可能的 path sum 总和. 

#### DFS, Hash Map
- 因为前两个digit可以locate一个node, 所以可以把前两个digit作为key, 定位node.
- 特点: 比如考虑root, 有 n 个leaf, 就会加 n 遍root, 因为有 n 个 unique path嘛.
- 对于每一个node也是一样: 只要有child, 到这个node位置的以上path sum 就要被重加一次.
- format: depth.position.value. (on same level, position may not be continuous)
- approach: map each number into: <depth.position, value>, and dfs. 
- Start from dfs(map, rootKey, sum):
- 1. add node value to sum
- 2. compute potential child.
- 3. check child existence, if exist, add sum to result (for both left/right child). Check existence using the map.
= 4. also, if child exist, dfs into next level



---

**35. [Binary Tree Right Side View.java](https://github.com/awangdev/LintCode/blob/master/Java/Binary%20Tree%20Right%20Side%20View.java)**      Level: Medium
      

给一个binary tree, 从右边看过来, return all visible nodes

#### BFS
- 最右:即level traversal每一行的最末尾.   
- BFS, queue 来存每一行的内容, save end node into list

#### DFS
- Use Map<Level, Integer> 来存每一个level的结果
- dfs(node.right), 然后 dfs(node.left)



---

**36. [Binary Tree Maximum Path Sum II.java](https://github.com/awangdev/LintCode/blob/master/Java/Binary%20Tree%20Maximum%20Path%20Sum%20II.java)**      Level: Medium
      

找到从max path sum from root. 条件: 至少有一个node.

#### DFS
- 比Binary Tree Maximum Path Sum I 简单许多. 因为条件给的更多：at least 1 node + have to start from root
- root一定用到
- 3种情况: curr node, curr+left, curr+right
- 因为一定包括root, 说以从 `dfs(root, sum=0)` 开始, 每个level先加root, sum += root.val



---

**37. [Binary Tree Longest Consecutive Sequence.java](https://github.com/awangdev/LintCode/blob/master/Java/Binary%20Tree%20Longest%20Consecutive%20Sequence.java)**      Level: Medium
      

找到binary tree 里的最长 consecutive sequence.

#### DFS
- Divide and Conquer. dfs
- 分开 看左边/右边
- 如果左边满足连续递增的规则, dfs (depth + 1), 如果不满足规则, dfs(depth = 1)
- 右边也是一样
- 对结果跟max作比较, return



---




 
 
 
## Trie (8)
**0. [Maximum XOR of Two Numbers in an Array.java](https://github.com/awangdev/LintCode/blob/master/Java/Maximum%20XOR%20of%20Two%20Numbers%20in%20an%20Array.java)**      Level: Medium
      

比较难想到. 利用到XOR性质A^B=C, then A=B^C.
1. 枚举可能的A, 2. 然后一个个猜.

1. 枚举A: 因为求MAX肯定是找leading-1最多的数字, 那么枚举A从(1000000...000)开始, 
每次多一位取1或者0
2. 因为枚举A的时候是按照每个bit来, 那么B和C也要以同样数位出现.
这里吧B和C变成了prefix的形式, 放在了set里面. 
跟2sum用hashmap的思想类似, 每次用枚举的 A^B=C, 看看结果C是否已经在set里面. 
如果在, 证明枚举的A可能被B^C得出, 那么就找到了一种情况.

还用到一些技巧: 
mask = (1 << i); // i位mask
mask = mask | (1 << i); // prefix mask



---

**1. [Implement Trie.java](https://github.com/awangdev/LintCode/blob/master/Java/Implement%20Trie.java)**      Level: Medium
      

Implement Tire, 也即是 Prefix Tree. 做三个function: insert, search, startWith

#### Trie
- HashMap构建Trie. Trie三个Method:
- 1. Inset: 加 word   
- 2. Search: 找word    
- 3. StartWith: 找prefix    

##### 特点
- 只有两条children的是binary tree. 那么多个children就是Trie
- 那么没有left/right pointer怎么找孩子？   
- 用HashMap，以child的label为Key，value就是child node。 HashMap走位   

##### 其他
- node里的char在这是optional. 只要在每个TrieNode里面用map存储向下分布的children就好了.  
- 另外有种题目，比如是跟其他种类的search相关，在结尾要return whole string，就可以在node里存一个up-to-this-point的String。

##### Previous Note
- 如果是遇到一个一个字查询的题，可以考虑一下。
- 构建TrieNode的时候要注意：如何找孩子？如果是个map的话，其实就挺好走位的。
- 而且，每个node里面的 char 或者string有时候用处不大，
- 可以为空。但是有些题目，比如在结尾要return一些什么String，就可以在end string那边存一个真的String。





---

**2. [Add and Search Word.java](https://github.com/awangdev/LintCode/blob/master/Java/Add%20and%20Search%20Word.java)**      Level: Medium
      

Trie结构, prefix tree的变形： '.'可以代替任何字符，那么就要iterate这个node所有的children.

节点里面有char, isEnd, HashMap<Character, TrieNode>   
Build trie = Insert word:没node就加，有node就移动。   
Search word:没有node就报错. 到结尾return true   

这题因为'.'可以代替任何possible的字符，没一种都是一个新的path，所以recursive做比较好些。    
(iterative就要queue了,麻烦点)



---

**3. [Word Search II.java](https://github.com/awangdev/LintCode/blob/master/Java/Word%20Search%20II.java)**      Level: Hard
      

给一串words, 还有一个2D character matrix. 找到所有可以形成的words. 条件: 2D matrix 只可以相邻走位.

#### Trie, DFS
- 相比之前的implementation, 有一些地方可以优化:
- 1. Backtracking时候, 在board[][] 上面mark就可以, 不需要开一个visited[][]
- 2. 不需要implement trie的所有方程, 用不到: 这里只需要insert.
- 普通的trie题目会让你search a word, 但是这里是用一个board, 看board的每一个字母能不能走出个Word.
- 也就是: 这里的search是自己手动写, 不是传统的trie search() funcombination
- 3. TrieNode里面存在 end的时候存string word, 表示到底. 用完了 word = null, 刚好截断重复查找的问题.

##### 关于Trie
- Build Trie with target words: insert, search, startWith.    
- 依然要对board matrix做DFS。
- no for loop on words. 直接对board DFS:   
- 每一层,都会有个up-to-this-point的string. 在Trie里面check它是不是存在。以此判断。   
- 若不存在，就不必继续DFS下去了。
- Trie solution time complexity, much better:      
- build Trie:   n * wordMaxLength
- search: boardWidth * boardHeight * (4^wordMaxLength + wordMaxLength[Trie Search])


#### Regular DFS
- for loop on words: inside, do board DFS based on each word.     
- Time cpmplexity: word[].length * boardWidth * boardHeight * (4^wordMaxLength)

#### Previous Notes
- Big improvement: use boolean visited on TrieNode!     
- 不要用rst.contains(...), 因为这个是O(n) 在leetcode还是会timeout（lintcode竟然可以pass）!    
- 在Trie search() method 里面，凡是visit过的，mark一下。  





---

**4. [Word Squares.java](https://github.com/awangdev/LintCode/blob/master/Java/Word%20Squares.java)**      Level: Hard
      

可以开Trie class, 里面用到TrieNode. 开Trie(words) 可以直接initalize with for loop
TrieNode 里面可以有一个 List<String> startWith: 记录可以到达这个点的所有string: 有点像树形, ancestor形状的存储.

神操作:
根据square的性质, 如果选中了list of words, 设定 int prefixIndex = list.size().
取出list里面的所有word[prefixedIndex], 并且加在一起, 就是下一个word candidate的 prefix.

形象一点:
list = ["ball", "area"];
prefixIndex = list.size(); ball[prefixIndex] = 'l'; area[prefixIndex] = 'e';
//then
candidatePrefix = ball[prefixIndex] + area[prefixIndex] = "le";
这里就可以用到Trie的那个 findByPrefix function, 在每个点, 都存有所有这个点能产生的candidate.
这时, 试一试所有candidate: dfs

能想到这种倒转的结构来存prefix candidates 在 Trie里面, 这个想法非常值得思考.



---

**5. [Palindrome Pairs.java](https://github.com/awangdev/LintCode/blob/master/Java/Palindrome%20Pairs.java)**      Level: Hard
      

Obvious的做法是全部试一遍, 判断, 变成 O(n^2) * O(m) = O(mn^2). O(m): isPalindrome() time.

当然不行了, 那就看是O(nlogN), 还是O(n)?

#### 方法1: Hash Table + Palindrome的性质. 复合型.
O(mn)

##### 思路
- 每一个word, 都可以拆分成 front + mid + end. 如果这个word + 其他word可以组成palindrome,那就是说
- 砍掉 (mid+end), front.reverse() 应该存在 words[] 里面.
- 砍掉 (front+mid), end.reverse() 应该存在 words[] 里面.
- 我们用HashMap存所有的<word, index>, 然后reverse, 找配对就好.

##### Corner case
- 如果有 empty string "", 那么它跟任何一个palindrome word, 都可以配对, 并且根据位置前后变换, 凑成2份 distinct indexes.
- 这样就有了那个 `if (reverseEnd.equals("")) {...}` 的logic.
- 注意: 虽然在处理砍头/砍尾的两个 for loop里面都在根据 empty string 重复记录, 
  但因为 "" 自己本身不能作为起点, 所以overall只会在被其他palindrome配对时记录一次.


#### 方法2: Trie
还要做一下那.



---

**6. [K Edit Distance.java](https://github.com/awangdev/LintCode/blob/master/Java/K%20Edit%20Distance.java)**      Level: Hard
      

给一串String, target string, int k. 找string array里面所有的candidate: 变化K次, 能变成target.

#### Trie
TODO

#### Double Sequence DP
- Edit Distance的follow up.
- 其实就是改一下 minEditDistance的function, 带入K作比较罢了.
- 写起来跟Edit Distance 的主要逻辑是一模一样的.
- 但是LintCode 86% test case 时候timeout. 
- Time O(mnh), where h = words.length, 如果 n ~ m, Time 就几乎是 O(n^2), 太慢.



---

**7. [Longest Word in Dictionary.java](https://github.com/awangdev/LintCode/blob/master/Java/Longest%20Word%20in%20Dictionary.java)**      Level: Easy
      

#### Sort, HashSet
- 先排序, 排序以后才能逐个看是否partial string已经存在
- 用 set.contains(substring(0, n - 1)) 来查看上一步的 substring 是否存在
- 如果找到, 因为已经按照字母表排序, 找到的这个肯定是这个长度里面最符合的解答.
- 然后brutally找下一个更大的.
- Sort O(n log n), O(n) set space

#### Trie
- 可以先sort words Array: 1. 长 string 排在前; 2. 相等length, 按照dictionary order 排序
- 全部放入Trie. Trie.insert()
- 针对sorted words array, 从最长的开始找 Trie.startWith.
- 一旦找到, 就是符合题意的, 直接return.
- 注意: startWith 必须每一个node都是 isEnd, 才满足'逐个字母拼出' 的条件.
- Time: build Trie O(mn) + sort:O(nlogn) => O(nlogn)
- Space: O(mn)

#### 
- 按大小排序 -> 从最大的开始做contains()的比较 -> 结果再按照字母表顺序(lexicographically) sort一下.
- 但是Collections.sort()了两次, 而且再list.contains(), 比较慢




---




 
 
 
## BST (18)
**0. [Convert Binary Search Tree to Doubly Linked List.java](https://github.com/awangdev/LintCode/blob/master/Java/Convert%20Binary%20Search%20Tree%20to%20Doubly%20Linked%20List.java)**      Level: Medium
      

会iterative traverse Binary Search Tree就好（Stack && handle left-dig-down）, 然后create Doubly-ListNode 时候注意就好.

注意inorder traversal在check right node的事后，    
不论right == null or != null, 每次都要强行move to right.    

如果不node = node.right,     
很可能发生窘境：       
node alays = stack.top(), 然后stack.top()一直是一开始把left 全部遍历的内容。所以就会infinite loop, 永远在左边上下上下。      



---

**1. [Inorder Successor in Binary Search Tree.java](https://github.com/awangdev/LintCode/blob/master/Java/Inorder%20Successor%20in%20Binary%20Search%20Tree.java)**      Level: Medium
      

画inorder图，发现规律.每个node的后继node(successor)有几种情况:   
1. node.right 是个leaf到底了。那么就return.   
2. set rightNode = node.right， 但发现rightNode has a lot left children to leaf.   
3. 比如, node.right == null， 也就是node自己是leaf，要回头看山顶找Inorder traversal规则里的下一个。   
	发现：其实就是每层都把路过的curr node放在stack里，最上面的，就是当下改return的那个successor:) Done.



---

**2. [Insert Node in a Binary Search Tree .java](https://github.com/awangdev/LintCode/blob/master/Java/Insert%20Node%20in%20a%20Binary%20Search%20Tree%20.java)**      Level: Easy
      

往Binary Search Tree里面加东西，一定会找到一个合适的leaf加上去。

那么：就是说someNode.left or someNode.right是null时，就是insert node的地方。

找到那个someNode就按照正常的Binary Search Tree规律。



---

**3. [Kth Smallest Element in a BST.java](https://github.com/awangdev/LintCode/blob/master/Java/Kth%20Smallest%20Element%20in%20a%20BST.java)**      Level: Medium
      

很容想到Inorder-binary-search-tree Traversal
Recursive 不难，然后稍微优化一下，确保rst.size() == k 时候，就可以return了。
Iterative 稍微难想点：先把最左边的add， pop() stack， 加上右边（如果存在）； 下一个轮回，如果又左孩子，又是一顿加。



---

**4. [Minimum Absolute Difference in BST.java](https://github.com/awangdev/LintCode/blob/master/Java/Minimum%20Absolute%20Difference%20in%20BST.java)**      Level: Easy
      

BST: inorder-traversal: 先left node(adding to stack till left leav), 再process stack.peek (mid node), 再 add rightNode && dive to rightNode.left leaf



---

**5. [Peeking Iterator.java](https://github.com/awangdev/LintCode/blob/master/Java/Peeking%20Iterator.java)**      Level: Medium
      

再一次理解错题意. peek() 就是头顶，但是不一定是最大值啊。总是把PEEK想成了最大值，然后用2 STACK做了最大值的cache，练的一手好双stack，可惜错了。

回到原题，其实不难。找一个cache来存next()的值，然后每次next()里面维护这个cache就好。



---

**6. [Remove Node in Binary Search Tree.java](https://github.com/awangdev/LintCode/blob/master/Java/Remove%20Node%20in%20Binary%20Search%20Tree.java)**      Level: Hard
      

方法1: Brutle一点。找到target和target的parent.    
把target remove时，把target的children nodes 重新排列组成新的BST: inorder traversal, build tree based on inorder traversal list.

方法2: 分析规律,先找到target和parent, 然后根据性质，把target remove时，移动children nodes, 保证还是BST。



---

**7. [Search Range in Binary Search Tree .java](https://github.com/awangdev/LintCode/blob/master/Java/Search%20Range%20in%20Binary%20Search%20Tree%20.java)**      Level: Medium
      

等于遍历了所有k1<= x <= k2的x node。

如果是用Binary Search Tree搜索，那么一般是if (...) else {...}，也就是一条路走到底，直到找到target.

这里, 把 left/right/match的情况全部cover了，然后把k1,k2的边框限制好，中间就全部遍历了。



---

**8. [Unique Binary Search Tree II.java](https://github.com/awangdev/LintCode/blob/master/Java/Unique%20Binary%20Search%20Tree%20II.java)**      Level: Medium
      



---

**9. [Zigzag Iterator.java](https://github.com/awangdev/LintCode/blob/master/Java/Zigzag%20Iterator.java)**      Level: Medium
      

这个题目相对简单. 做的时候我先考虑起来k条怎么办. 那么用个map把index和每个listmark一下就好了。
每次next(), 相应的list的头拿下来就好。
然后就跑圈呗，每次刷一个list头。不难。只要把几个variable维护清楚就行。


---

**10. [Unique Binary Search Tree.java](https://github.com/awangdev/LintCode/blob/master/Java/Unique%20Binary%20Search%20Tree.java)**      Level: Medium
      

Not quite clear.
根据左右分割而总结出了原理, 每次分割, 左右两边都会有一定数量的permutation, 总体上的情况数量当然是相乘.
然后每一个不同的分割点都加一遍:
f(n) = f(0)*f(n-1) + f(1)*f(n-2) + ... + f(n-2)*f(1) + f(n-1)*f(0)

然后把数学公式转换成DP的方程, 有点玄学的意思啊! 不好想.



---

**11. [Trim a Binary Search Tree.java](https://github.com/awangdev/LintCode/blob/master/Java/Trim%20a%20Binary%20Search%20Tree.java)**      Level: Easy
      

方法1:
适合复习BST. 用DFS对待每个node. 注意BST的特征: 所有left nodes都小于当下node, 所有right nodes都大于当下node.

根据题意用[L,R]切割.如果node.val<L, 直接连node带左边全丢掉, return node.right. 处理R也是一样.
分制是, DFS leftNode, rightNode. 然后接在node.left, node.right.

方法2: 用迭代, 还没有写.



---

**12. [Binary Search Tree Iterator.java](https://github.com/awangdev/LintCode/blob/master/Java/Binary%20Search%20Tree%20Iterator.java)**      Level: Medium
      

画一下, BST in order traversal. 用stack记录最小值, 放在top. O(h) space.
每次消耗TreeNode, 都看看rightNode(其实就是下一个最小的candidate), 并且一条龙stack叠上rightNode所有的left子孙.

Previous Notes:
用O(h)空间的做法：

理解binary search tree inorder traversal的规律：
   先找left.left.left ....left 到底，这里是加进stack.
   然后考虑parent,然后再right.

例如这题：
   stack里面top，也就是tree最左下角的node先考虑,取名rst.
   其实这个rst拿出来以后, 它也同时是最底层left null的parent，算考虑过了最底层的parent。
   最后就考虑最底层的parent.right, 也就是rst.right.

注意:
   next()其实有个while loop, 很可能是O(h).题目要求average O(1),所以也是okay的.


用O(1)空间的做法：不存stack, 时刻update current为最小值。

找下一个最小值,如果current有right child：   
   和用stack时的iteration类似,那么再找一遍current.right的left-most child,就是最小值了。
   
如果current没有right child:    
    那么就要找current node的右上parent, search in BinarySearchTree from root.

注意：
   一定要确保找到的parent满足parent.left == current.
   反而言之，如果current是parent的 right child, 那么下一轮就会重新process parent。
   但是有错:binary search tree里面parent是小于right child的，也就是在之前一步肯定visit过，如此便会死循环。




---

**13. [Validate Binary Search Tree.java](https://github.com/awangdev/LintCode/blob/master/Java/Validate%20Binary%20Search%20Tree.java)**      Level: Medium
      

如题, 验证是否是BST.

#### DFS
- 查看每个parent-child关系: leftchild < root < rightChild
- 方法: 把root.val 传下来作为 max 或者 min, 然后检查children

##### Note: 
- min/max需要时long type. 
- 如果题目真的给node.val = Integer.MAX_VALUE, 我们需要能够与之比较, long就可以.



---

**14. [Convert Sorted List to Binary Search Tree.java](https://github.com/awangdev/LintCode/blob/master/Java/Convert%20Sorted%20List%20to%20Binary%20Search%20Tree.java)**      Level: Medium
      

如题, 把一个sorted singly linked list 转换成一个 height balanced BST

#### DFS
- Divide and Conquer   
- 找到mid node
- 然后分割两半, 分别dfs做各自两个subtree: node.left,node.right
- 用长度来定位mid, 每次找中间点做root, 然后前半段, 后半段分别dfs with length.
- 用快慢pointer 找到mid. Better: 不用traverse entire linked list

#### Details
- slowPointer = node;
- fastPointer = node.next;
- 然后把root = mid.next     
- 然后开始sortedListToBST(mid.next.next); //后半段    
- mid.next = null;//非常重要，要把后面拍过序的断掉    
- sortedListToBST(head); //从头开始的前半段     
- 最后root.left, root.right merge一下。   



---

**15. [Closest Binary Search Tree Value.java](https://github.com/awangdev/LintCode/blob/master/Java/Closest%20Binary%20Search%20Tree%20Value.java)**      Level: Easy
      

给一个BST, 和一个double target, 走位找到最接近的number.

#### Recursive
- when less than curr val, consider left
- when greater than curr val, consider right
- dfs到底, 然后每一层比较, 再return

#### Binary Search
- 记录找到过的closest
- Binary Search, 根据current node走位,
- 找到 node.val == target, 或者走位走完, return closest



---

**16. [Contains Duplicate III.java](https://github.com/awangdev/LintCode/blob/master/Java/Contains%20Duplicate%20III.java)**      Level: Medium
      

给一个unsorted array, 问, 是否有两个element, value相差最大为t,  而两个element的index 相差最大为k.

Note: 虽然题目名字是Contains Duplicate, 但其实要找的两个element不是duplicate, 而是Math.abs(value1 - value2) <= t.

#### TreeSet
- TreeSet还是一个set, 我们用来装已经visit过得item
- 如果window大小超过K, 那么把nums[i - k - 1] 去掉, 并且加上新的element
- 这里有个公式推算: (Math.abs(A-B) <= t) =>>>>> (-t <= A - B <= t) =>>>>>> A >= B - t, A <= B + t
- 也就是说, 如果对于 B = nums[i], 来说, 能找到一个target A, 满足上面的公式, 那么就可以 return true.
- Time O(nLogk), treeSet的大小不会超过k,  而 treeSet.ceiling(), treeSet.add(), treeSet.remove() 都是 O(logK)
- Space O(k)

#### Note
- 与Contains Duplicate II 类似概念. TreeSet有BST 因此可以直接用, 而不用自己构建BST
- 简化题目里面的重要条件 Math.abs(A-B) <= t 而推断出 A >= B - t, A <= B + t
- 并且需要需要用 TreeSet.ceiling(x): return number greater or equal to x. 这个用法要记住吧, 没别的捷径.



---

**17. [Lowest Common Ancestor of a Binary Search Tree.java](https://github.com/awangdev/LintCode/blob/master/Java/Lowest%20Common%20Ancestor%20of%20a%20Binary%20Search%20Tree.java)**      Level: Medium
      

给 binary search tree root, q node, p node. 找到p q 的lowest common ancestor

#### Find path with BST
- 利用 BST 的性质，可以直接搜到target node，而做成两个长度不一定相等的list
- 然后很简单找到LCA 

#### DFS
- Brutly寻找p和q的common ancestor, 然后recursively drive left/right
- 非常巧妙, 但是也比较局限; 稍微变条件, 就很难recursive.
- 几种情况:
- 1. one of p, q 在leaf, 那么此时的root其实就是lowest common ancestor
- 2. 如果p, q 在root的左右两边, 这就是分叉口, 那么root就是lowest common ancestor
- 3. 如果p,q 在root的同一边 (左,右), 那么继续dfs



---




 
 
 
## Permutation (1)
**0. [Shuffle an Array.java](https://github.com/awangdev/LintCode/blob/master/Java/Shuffle%20an%20Array.java)**      Level: Medium
      

像shuffle music 一样, 做一套shuffle array的functions: 

shuffle() 给出random的permutation

reset() 给出最初的nums

#### Permutation
- Permutation 实际上就是在list/array/... 上面给元素换位置
- 硬换位置, 每次换的位置不同, 用random来找到要换的index
- 维持同一个random seed
- O(n)

##### Note
- compute all permutations 太慢, 不可行.



---




 
 
 
## Partition DP (5)
**0. [Perfect Squares.java](https://github.com/awangdev/LintCode/blob/master/Java/Perfect%20Squares.java)**      Level: Medium
      

给一个数字n, 找到这个数字 最少能用多少个 平方数组成. 

平方数比如: 1, 4, 9, 16 ... etc

#### Partition DP
- 遇到最值, 想到DP.
- 看到分割字眼, 想到分割型 DP. 
- 思考, 如果 j * j = 9, 那么 j = 3 就是最少的一步; 但是如果是10呢? 就会分割成1 + 9 = 1 + j * j 
- 考虑最后的数字: 要是12割个1出来, 剩下11怎么考虑? 割个4出来,剩下8怎么考虑?
- partion的方式: 在考虑dp[i - x]的时候,  x 不是1, 而是 x = j*j.
- 就变成了dp = Min{dp[i - j^2] + 1}

#### 时间复杂度
- 乍一看是O(n*sqrt(n)). 实际也是. 但如何推导?
- 考虑上限: 把小的数字变成大的 推导上限; 考虑下限: 把数字整合归小, 找到下限.
- 考虑sqrt(1) + sqrt(2) + ....sqrt(n):找这个的upper bound and lower bound.
- 最后发现它的两边是 A*n*sqrt(n) <= actual time complexity <= B*n*sqrt(n)
- 那么就是O(n*sqrt(n))啦

#### Previous Notes
- 一开始没clue.看了一下提示
- １.　第一步想到了，从数学角度，可能是从最大的perfect square number开始算起。
- ２.　然后想法到了dp， 假设最后一步用了最大的maxSqrNum, 那么就在剩下的 dp[i - maxSqrNum^2] +１　不就好了？
- ３.　做了，发现有个问题．．．最后一步选不选maxSqrNum?  比如12就是个例子。
- 然后就根据提示，想到BFS。顺的。 把1～maxSqrNum 都试一试。找个最小的。
- 看我把12拆分的那个example. 那很形象的就是BFS了。
- 面试时候，如果拆分到这个阶段不确定，那跟面试官陶瓷一下，说不定也就提示BFS了。



---

**1. [Copy Books.java](https://github.com/awangdev/LintCode/blob/master/Java/Copy%20Books.java)**      Level: Hard
      

给一串书pages[i], k个人, pages[i] 代表每本书的页数. k个人从不同的点同时开始抄书. 

问, 最快什么时候可以抄完?

#### Partition DP
- 第一步, 理解题目要求的问题: 前k个人copy完n本书, 找到最少的用时; 也可以翻译成, n本书, 让k个人来copy, 也就是分割成k段.
- 最后需要求出 dp[n][k]. 开: int[n+1][k+1]. 
- 在[0 ~ n - 1]本书里, 最后一个人可以选择copy 1 本, 2 本....n本, 每一种切割的方法的结果都不一样
- 木桶原理, 因为K个人同时开始, 最坏的情况决定结果
- dp[n][k] = Math.min(Math.max(dp[j][k - 1], sum[j+1, n-1]), loop over i, k, j)
- Time: O(kn^2), space O(nk)

##### Init
- Init: dp[0][0] = 0, 0个人0本书
- Integer.MAX_VALUE的运用:
- 当 i = 1, k = 1, 表达式: dp[i][k] = Math.min(dp[i][k], Math.max(dp[j][k - 1], sum));
- 唯一可行的情况就只有一种: i=0, k=0, 刚好 0 个人 copy 0 本书, dp[0][0] = 0.
- 其他情况, i = 1, k = 0, 0 个人读 1本书, 不可能发生: 所以用Integer.MAX_VALUE来冲破 Math.max, 维持荒谬值.
- 当 i=0, k=0 的情况被讨论时候, 上面的方程式才会按照实际情况计算出 dp[i][k]
- 这道题的init是非常重要而tricky的

##### 计算顺序
- k个人, 需要一个for loop; 
- k个人, 从copy1本书开始, 2, 3, ... n-1,所以 i=[1, n], 需要第二个for loop
- 在每一个i上, 切割的方式可以有[0 ~ i] 中, 我们要计算每一种的worst time

##### 滚动数组
- [k] 只有和 [k - 1] 相关
- Space: O(n)

#### Binary Search
- 根据: 每个人花的多少时间(time)来做binary search: 每个人花多久时间, 可以在K个人之内, 用最少的时间完成?
- time variable的范围不是index, 也不是page大小. 而是[minPage, pageSum]
- validation 的时候注意3种情况: 人够用 k>=0, 人不够所以结尾减成k<0, 还有一种是time(每个人最多花的时间)小于当下的页面, return -1
- O(nLogM). n = pages.length; m = sum of pages.




---

**2. [Decode Ways.java](https://github.com/awangdev/LintCode/blob/master/Java/Decode%20Ways.java)**      Level: Medium
      

给出一串数字, 要翻译(decode)成英文字母. [1 ~ 26] 对应相对的英文字母. 求有多少种方法可以decode.

#### Partition DP
- 确定末尾的2种状态: single letter or combos. 然后计算出单个letter的情况, 和双数的情况
- 定义dp[i] = 前i个digits最多有多少种decode的方法. new dp[n + 1].
- 加法原理: 把不同的情况, single-digit, double-digit 的情况加起来
- note: calculate number from characters, need to - '0' to get the correct integer mapping.
- 注意: check value != '0', 因为'0' 不在条件之中(A-Z)




---

**3. [Decode Ways II.java](https://github.com/awangdev/LintCode/blob/master/Java/Decode%20Ways%20II.java)**      Level: Hard
      

给出一串数字, 要翻译(decode)成英文字母. [1 ~ 26] 对应相对的英文字母. 求有多少种方法可以decode.

其中字符可能是 "*", 可以代表 [1 - 9]

#### DP
- 跟decode way I 一样, 加法原理, 切割点时: 当下是取了 1 digit 还是 2 digits 来decode
- 定义dp[i] = 前i个digits最多有多少种decode的方法. new dp[n + 1].
- 不同的情况是: 每一个partition里面, 如果有"*", 就会在自身延伸出很多不同的可能
- 那么: dp[i] = dp[i - 1] * (#variations of ss[i]) + dp[i - 2] * (#variations of ss[i,i+1])

##### 特点
- 枚举的能力: 具体分析 '*' 出现的位置, 枚举出数字, 基本功. 注意!!题目说 * in [1, 9].   (如果 0 ~ 9 会更难一些)
- 理解取MOD的原因: 数字太大, 取mod来给最终结果: 其实在 10^9 + 7 这么大的 mod 下, 大部分例子是能通过的.
- 枚举好以后, 其实这个题目的写法和思考过程都不难




---

**4. [Palindrome Partitioning II.java](https://github.com/awangdev/LintCode/blob/master/Java/Palindrome%20Partitioning%20II.java)**      Level: Hard
      

给一个String s, 找出最少用多少cut, 使致 切割出的每一个substring, 都是palindrome

#### Partition DP
- Find minimum cut: 分割型DP
- dp[i]: 最少cut多少刀, 使得前 i 长度的string, 割出来都是palindrome
- 最终要得到 dp[n], 所以 int[n + 1]
- 移动切刀, 看在哪里切, index j in [0 ~ i]
- 考虑[j, i - 1] 是否是回文串, 如果是, 那么: dp[i]= min(dp[i], d[j] + 1).
- note: 估计遍历 j 的时候, 反过来遍历也可以.

#### 计算Palindrome的优化
- 利用palindrome的性质, 可以算出 boolean palindrome[i, j]的情况. 
- 找一个任意mid point:
- 1. 假设palindrome是奇数长度, 那么 mid 是单独的字符, 而两边的字符 [mid-1], [mid+1] 应该完全相等.
- 2. 假设palindrome是偶数长度, 那么 [mid] 和 [mid + 1] 这样位置的字符应该相等.
- 这样做出来 palindrome[i, j]: 从字符 i 到 字符 j 的 substring 是否是 palindrome
- 这样就给我们的问题合理降维, 目前是time: O(n^2). 
- 不然求一次palindrome, 就是n, 会变成O(n^3)

#### Previous Notes
- Double for loop 检查每种substring string (i~j). 若i,j相邻或者同点，那么肯定isPal；否则，i,j之间的（i+1, j-1）一定得isPal。
- 看上去，在检查i,j的时候，中间按的（i+1, j-1）怎么可能先知道？ 其实不然..在j慢慢长大的时候，所有的0~j的substring都检查过。所以isPal[i+1][j-1]一定是已经知道结果的。
- okay.那么假如以上任意一种情况成立，也就是说isPal[i][j] == true。那就要判断，切到第一层循环参数j的末尾点时，有多少种切法？
- 想法很顺：我们naturally会想到，把i之前的cut加上i~j之间发生的不就好了。
- 反正现在j不变，现在就看吧i定在哪里，cut[i - 1]是否更小/最小； 再在cut[i-1]基础上+1就完了。
- 当然，如果i==0, 而 i~j又是isPal,那没啥好谈的，不必切，0刀。
- 最终，刷到cut[s.length() - 1] 也就是最后一点。 return的理所应当。




---




 
 
 
## Interval DP (4)
**0. [Longest Palindromic Subsequence.java](https://github.com/awangdev/LintCode/blob/master/Java/Longest%20Palindromic%20Subsequence.java)**      Level: Medium
      

#### Interval DP
- 用[i][j]表示区间的首尾
- 考虑3个情况: 砍头, 砍尾, 砍头并砍尾 (考虑首尾关系)
- Iteration一定是以i ~ j 之间的len来看的. 
- len = j - i + 1; 那么反推, 如果len已知, j = len + i -1;
- 注意考虑len == 1, len == 2是的特殊情况.

#### Memoization
- 同样的方式model dp[i][j]: range [i, j] 之间的  max palindromic length
- 三种情况: 
- 1. 首尾match 继而 dfs[i+1, j-1]
- 2. 首尾不match,dfs[i+1,j] 
- 3. 首尾不match,dfs[i,j-1] 
- 注意: init dp[i][j]=-1, dfs的时候查dp[i][j] 是否算过



---

**1. [Scramble String.java](https://github.com/awangdev/LintCode/blob/master/Java/Scramble%20String.java)**      Level: Hard
      

- 给两个string S, T. 检验他们是不是scramble string.
- scramble string 定义: string可以被分拆成binary tree的形式, 也就是切割成substring;
- 旋转了不是leaf的node之后, 形成新的substring, 这就是原来string的 scramble.


#### Interval DP 区间型
- 降维打击, 分割, 按照长度来dp.
- dp[i][j][k]: 数组S从index i 开始, T从index j 开始, 长度为k的子串, 是否为scramble string

##### Break down
- 一切两半以后, 看两种情况: , 或者不rotate这两半. 对于这些substring, 各自验证他们是否scramble.
- 不rotate分割的两半: S[part1] 对应  T[part1] && S[part2] 对应  T[part2]. 
- rotate分割的两半: S[part1] 对应  T[part2] && S[part2] 对应  T[part1]. 

##### Initialization
- len == 1的时候, 其实无法旋转, 也就是看S,T的相对应的index是否字符相等.
- initialization非常非常重要. 很神奇, 这个initailization 打好了DP的基础, 后面一蹴而就, 用数学表达式就算出了结果.
- input s1, s2 在整个题目的主要内容里面, 几乎没有用到, 只是用在initialization时候.
- More details, 看解答



---

**2. [Coins in a Line III.java](https://github.com/awangdev/LintCode/blob/master/Java/Coins%20in%20a%20Line%20III.java)**      Level: Hard
      

还是2个人拿n个coin, coin可以有不同的value. 

只不过这次选手可以从任意的一头拿, 而不限制从一头拿. 算先手会不会赢?

#### Memoization + Search
- 跟Coins in a Line II 一样, MaxiMin的思想: 找到我的劣势中的最大值
- dp[i][j] 代表在[i,j]区间上 选手最多能取的value 总和
- 同样, sum[i][j]表示[i] 到 [j]间的value总和
- 对手的最差情况, 也就是先手的最好情况:
- dp[i][j] = sum[i][j] - Math.min(dp[i][j - 1], dp[i + 1][j]);
- 这里需要search, 画出tree可以看明白是如何根据取前后而分段的.

#### 博弈 + 区间DP
- 因为是看区间[i,j]的情况, 所以可以想到是区间 DP
- 这个方法需要复习, 跟数学表达式的推断相关联: S(x) = - S(y) + m. 参考下面的公式推导.
- dp[i][j]表示 从index(i) 到 index(j), 先手可以拿到的最大值与对手的数字差. 也就是S(x).
- 其中一个S(x) = dp[i][j] = a[i] - dp[i + 1][j]
- m 取在开头, m 取在末尾的两种情况:
- dp[i][j] = max{a[i] - dp[i + 1][j], a[j] - dp[i][j - 1]}
- len = 1, 积分就是values[i]
- 最后判断 dp[0][n] >= 0, 最大数字和之差大于0, 就赢.
- 时间/空间 O(n^2)

##### 公式推导
- S(x) = X - Y, 找最大数字和之差, 这里X和Y是选手X的总分, 选手Y的总分. 
- 对于选手X而言: 如果S(x)最大值大于0, 就是赢了; 如果最大值都小于0, 就一定是输了. 
- 选手Y: S(y)来表示 对于Y,  最大数字和之差. S(y) = Y - X
- 根据S(x) 来看, 如果从 数字和X里面, 拿出一个数字 m, 也就是 X = m + Xwithout(m)
- S(x) = m + Xwithout(m) - Y = m + (Xwithout(m) - Y). 
- 如果我们从全局里面索性去掉m, 那么 S(y'') = Y - Xwithout(m)
- 那么推算下来: S(x) = m + (Xwithout(m) - Y) = m - (Y - Xwithout(m)) = m - S(y'')
- 在这个问题里面, 我们model X 和 Y的时候, 其实都是 dp[i][j], 而区别在于先手/后手.
- 将公式套用, 某一个S(x) = a[i] - dp[i + 1][j],  也就是m=a[i], 而 S(y'') = dp[i + 1][j]

##### 注意
- 如果考虑计算先手[i, j]之间的最大值, 然后可能还需要两个数组, 最后用于比较先手和opponent的得分大小 => 那么就要多开维.
- 我们这里考虑的数字差, 刚好让人不需要计算先手的得分总值, 非常巧妙.
- Trick: 利用差值公式, 推导有点难想到.

##### 区间型动态规划
- 找出[i, j]区间内的性质: dp[i][j]下标表示区间范围 [i, j]
- 子问题: 砍头, 砍尾, 砍头砍尾
- loop应该基于区间的length
- template: 考虑len = 1, len = 2; 设定i的时候一定是 i <= n - len; 设定j的时候, j = len + i - 1;




---

**3. [Burst Balloons.java](https://github.com/awangdev/LintCode/blob/master/Java/Burst%20Balloons.java)**      Level: Hard
      

一排球, 每个球有value, 每次扎破一个, 就会积分: 左*中间*右 的值. 求, 怎么扎, 最大值?

TODO: Need more thoughts on why using dp[n + 2][n + 2] for memoization, but dp[n][n] for interval DP.

#### Interval DP
- 因为数组规律会变, 所以很难找'第一个burst的球'. 反之, 想哪一个是最后burst?
- 最后burst的那个变成一堵墙: 分开两边, 分开考虑, 加法原理; 最后再把中间的加上.
- dp[i][j] represent max value on range [i, j)
- Need to calculate dp[i][j] incrementally, starting from range size == 3 ---> n
- Use k to divide the range [i, j) and conquer each side.

##### Interval DP 三把斧:
- 中间劈开
- 砍断首或尾
- Range区间作为iteration的根本

##### Print the calculation process
- use pi[i][j] and print recursively.
- Print k, using pi[i][j]: max value taken at k

#### Memoization
- 其实会做之后挺好想的一个DP
- dp[i][j] =  balloons i~j 之间的 max. 
- 然后找哪个点开始burst? 设为x。
- For loop 所有的点作为x， 去burst。
- 每次burst都切成了三份：左边可以recusive 求左边剩下的部分的最大值 + 中间3项相乘 + 右边递归下去求最大值。
- Note: 这个是Memoization, 而不纯是DP
- 因为recursive了，其实还是搜索，但是memorize了求过的值，节省了Processing




---




 
 
 
## Heap (6)
**0. [Kth Smallest Number in Sorted Matrix.java](https://github.com/awangdev/LintCode/blob/master/Java/Kth%20Smallest%20Number%20in%20Sorted%20Matrix.java)**      Level: Medium
      

方法1:
和Merge K sorted Array/ List 类似：使用PriorityQueue。

因为Array的element无法直接找到next,所以用一个class Node 存value, x,y positions.

方法2:
Binary Search
https://leetcode.com/problems/kth-smallest-element-in-a-sorted-matrix/discuss/85182/my-solution-using-binary-search-in-c


变型: Kth Largest in N Arrays


---

**1. [Trapping Rain Water II.java](https://github.com/awangdev/LintCode/blob/master/Java/Trapping%20Rain%20Water%20II.java)**      Level: Hard
      

用PriorityQueue把选中的height排序。为走位，create class Cell (x,y, height).

#### 注意几个理论
1. 从matrix四周开始考虑，发现matrix能Hold住的水，取决于height低的block。
2. 必须从外围开始考虑，因为水是被包裹在里面，外面至少需要现有一层。

以上两点就促使我们用min-heap: 也就是natural order的PriorityQueue<Cell>.

#### 具体步骤
1. process的时候，画个图也可以搞清楚: 就是四个方向都走走，用curr cell的高度减去周围cell的高度.
   若大于零，那么周围的cell就有积水。
2. 每个visited的cell都要mark. 
3. 根据4个方向的走位, 创建新cell 加进queue里面. 因为做的是缩小一圈的新围墙, height = Math.max(cell.h, neighbor.h);

再多一句解释: 和trapping water I 想法一样。刚刚从外围，只是能加到跟外围cell高度一致的水平面。往里面，很可能cell高度变化。   
这里要附上curr cell 和 move-to cell的最大高度。

#### 为什么想到用Heap (min-heap - priorityQueue)
- 要找到bucket的最短板
- 每次需要最先处理最短的那条 (on top)


#### 为什么从外向里遍历
- 木桶理论, 包水, 是从外面包住里面
- 洋葱剥皮, 用完丢掉



---

**2. [Data Stream Median.java](https://github.com/awangdev/LintCode/blob/master/Java/Data%20Stream%20Median.java)**      Level: Hard
      

#### 原理
- 把Input stream想成向上的山坡. 山坡中间那点，自然就是median.
- 前半段，作为maxHeap,关注点是PriorityQueue的峰点，也就是实际上的median.   
- 后半段，作为minHeap,正常的PriorityQueue。 开头是最小的。

#### 注意
- 这里要首先定好, 哪一个queue是多存一个element的. 这里选maxHeap: maxHeap.size() == minHeap.size() + 1 || minHeap.size()
- 必须先维护maxHeap里面有个元素, 否则null了会在比较大小时出问题.



---

**3. [Sliding Window Median.java](https://github.com/awangdev/LintCode/blob/master/Java/Sliding%20Window%20Median.java)**      Level: Hard
      

Median还是用min-heap 和 max-heap. Time(logN)
加/减: prioirtyQueue, log(n)
findMedian: O(1)

#### 思想
- 加一个数, 减一个数。
- 加减时看好，是从前面的maxheap里面抽，还是从后面的minHeap里面抽。
- 抽完balance一下

#### 注意
用maxHeap, minHeap时候, 习惯选择让maxHeap多一个数字:
左边的maxHeap总有 x+1或者x个数字
后边minHeap应该一直有x个数字



---

**4. [Meeting Rooms II.java](https://github.com/awangdev/LintCode/blob/master/Java/Meeting%20Rooms%20II.java)**      Level: Medium
      

给一串数字pair, 代表会议的开始/结束时间. 找同时又多少个会议发生(需要多少件房间)

#### 方法1
- PriorityQueue + 一个Class来解决.Ｏ(nlogn)
- 跟 Number of Airpline in the sky是同一道题

#### 方法2: 尝试了一下用一个sorted Array + HashMap
也还行，但是handle edge的时候,HashMap 要小心，因为相同时间start和end的map key 就会重复了。



---

**5. [Building Outline.java](https://github.com/awangdev/LintCode/blob/master/Java/Building%20Outline.java)**      Level: Review
      

又叫做skyline. 用Sweep Line做的O(nLogN), 但是貌似还有很多做法: segement tree, hashheap, treeSet?

#### 方法1: Sweep Line, Time O(nLogN), Space O(n)
original reference http://codechen.blogspot.com/2015/06/leetcode-skyline-problem.html?_sm_au_=isVmHvFmFs40TWRt

sweep line:
- 把所有点分出来， 每个点有index x, 再加上一个height.         
- 在这个list上排序，根据index和height. 注意用负数标记building start point height, 这样保证start在end 之前
- 用负数的height标记start: 在priority queue里面同一个x-pos比较 startPoint.height, endPoint.height 的时候, 因为end height是整数, 所以compare时会自动把start point放在end point前面
- 当然了, 如果两个 start point比较, 第二个point的负数超大的话(也就是height很高), 就会顺理compare return正数, 成章形成倒位
- 在processs时候用max-heap (reversed priorityqueue)，再iterate heightPoints 来存最大的height . 遇到peek,就是一个合理的解    
- heightQueue里面加一个0, 用来在结尾的时候做closure

#### 方法2: Segment Tree
REVIEW

Binary Indexed Tree?

HashHeap?



---




 
 
 
## Linked List (20)
**0. [Intersection of Two Linked Lists.java](https://github.com/awangdev/LintCode/blob/master/Java/Intersection%20of%20Two%20Linked%20Lists.java)**      Level: Easy
      
1525664839

给两个 linked list, 问从哪个node开始, 两个 linked list 开始有重复?

#### Basics
- 长短list，找重合点
- 长度不同的话，切掉长的list那个的extra length
- 那么起点一样后，重合点就会同时到达
- Time O(n) * 2, constant space



---

**1. [Add Two Numbers.java](https://github.com/awangdev/LintCode/blob/master/Java/Add%20Two%20Numbers.java)**      Level: Medium
      

LinkedList都已经反转好了，直接做.
遍历两个l1,l2把carry-on处理好，每次生成一个新node，最后检查carry-on.

跟Add Binary的理解方式一模一样.

注意:
Linked List 没有天然size.
用DummyNode(-1).next来hold住结果.




---

**2. [Add Two Numbers II.java](https://github.com/awangdev/LintCode/blob/master/Java/Add%20Two%20Numbers%20II.java)**      Level: Medium
      

Singly-linked list需要reverse, 用stack.
最终结果要恢复成input list 那样的sequence方向, 用stack一个个pop()刚好就可以做到.

加法都一样:
   1. sum = carry
   2. carry = sum / 10
   3. sum = sum % 10;



---

**3. [Convert Sorted List to Binary Search Tree.java](https://github.com/awangdev/LintCode/blob/master/Java/Convert%20Sorted%20List%20to%20Binary%20Search%20Tree.java)**      Level: Medium
      

如题, 把一个sorted singly linked list 转换成一个 height balanced BST

#### DFS
- Divide and Conquer   
- 找到mid node
- 然后分割两半, 分别dfs做各自两个subtree: node.left,node.right
- 用长度来定位mid, 每次找中间点做root, 然后前半段, 后半段分别dfs with length.
- 用快慢pointer 找到mid. Better: 不用traverse entire linked list

#### Details
- slowPointer = node;
- fastPointer = node.next;
- 然后把root = mid.next     
- 然后开始sortedListToBST(mid.next.next); //后半段    
- mid.next = null;//非常重要，要把后面拍过序的断掉    
- sortedListToBST(head); //从头开始的前半段     
- 最后root.left, root.right merge一下。   



---

**4. [Linked List Cycle.java](https://github.com/awangdev/LintCode/blob/master/Java/Linked%20List%20Cycle.java)**      Level: Easy
      

O(1) sapce: 用快慢指针。一个跑.next, 一个跑.next.next。 总有一次，fast会因为cycle而追上slow。
那个时候其实slow.val = fast.val.

O(n) space: 用HashMap，一直add elements.  如果有重复，那么很显然是有Cycle


---

**5. [Remove Nth Node From End of List.java](https://github.com/awangdev/LintCode/blob/master/Java/Remove%20Nth%20Node%20From%20End%20of%20List.java)**      Level: Medium
      

O(n), one pace, no extra space
找到窗口, 然后平移, 最后pre 和 head之间 skip一个node就好.



---

**6. [Linked List Cycle II.java](https://github.com/awangdev/LintCode/blob/master/Java/Linked%20List%20Cycle%20II.java)**      Level: Medium
      

方法1:
快慢指针, O(1)space.

确认有cycle后, 其实是数学问题:
当head == slow.next时候， head就是cycle starting point.
也就是说，当slow 移动到了那个回溯点，slow.next那个点就刚好是head的那个点...

证明:
1. 假设慢指针走t步, 快指针走快一倍, 也就是2t.
2. 我们假设cycle的长度是Y, 而进入cycle之前的长度为X.
3. 假设慢指针走了m圈cycle, 而快指针走了n圈cycle之后, 两个pointer相遇.
4. 最终在Y cycle里面的K点相遇, 也就是两个指针都在这最后一圈里面走了K 步.
=> 
那么:
t = X + mY + K
2t = X + nY + K
整合公式:
X + K = (n - 2m)Y
这里的m和n不过是整数的跑圈数, 也就是说X和K加在一起, 总归是结束cycle. X 和 K 互补
=> 结论: 当slow/fast 指针在K点相遇后, 再走X步, 就到了cycle的起点, 也就是题目要求的起点.

方法2:
HashMap, O(n) space


---

**7. [Swap Nodes in Pairs.java](https://github.com/awangdev/LintCode/blob/master/Java/Swap%20Nodes%20in%20Pairs.java)**      Level: Medium
      

#### enumurate 
基本原理, 写出来, 然后连线:
pre -> A -> B -> C -> ...
需要一个虚拟 preNode做起始node, 不然无法把后面的node换到开头.

#### 注意
用dummy = pre作为head前一格.
用 `pre.next == null && pre.next.next` 来check是否为NULL.
pre.next.next 保证了至少有一次swap.



---

**8. [Delete Node in a Linked List.java](https://github.com/awangdev/LintCode/blob/master/Java/Delete%20Node%20in%20a%20Linked%20List.java)**      Level: Easy
      

Given Singlely linked list, 删除一个任意node (不能是head node)

#### Basic
- update node.val
- Link curr.next to curr.next.next



---

**9. [Insertion Sort List.java](https://github.com/awangdev/LintCode/blob/master/Java/Insertion%20Sort%20List.java)**      Level: Medium
      

input一串数字, 需要出sorted output. 每次insert一个数字时, 都要放到正确的sorted的位置

每次insertion的时候, 都从input里面减掉这个数字

#### Linked List
- 把list里面每个元素都拿出来，scan and insert一遍
- Time O(n^2), worst case, 每次放入n个数字里面的element, 刚好都是最大的
- 所以每次要traverse n nodes, 然后走n次

##### 思考方法
- 如果已经有个sorted list, insert一个element进去。怎么做？
- while 里面每个元素都小于 curr, keep going
- 一旦curr在某个点小了，加进去当下这个空隙。



---

**10. [Middle of Linked List.java](https://github.com/awangdev/LintCode/blob/master/Java/Middle%20of%20Linked%20List.java)**      Level: Easy
      

找Linked List的中间node

- 快慢指针
- 不在乎slow是不是到底，因为fast肯定先到。
- 确保fast, fast.next不是Null就好



---

**11. [Remove Linked List Elements.java](https://github.com/awangdev/LintCode/blob/master/Java/Remove%20Linked%20List%20Elements.java)**      Level: Easy
      

从linked list 里面去掉所有的 target

#### Basics
- 如果match: node.next = head.next;
- 如果不match, node 和 head 一起移动



---

**12. [Palindrome Linked List.java](https://github.com/awangdev/LintCode/blob/master/Java/Palindrome%20Linked%20List.java)**      Level: Easy
      

#### Reverse Linked List
- Palindrome概念很简单, 但是要在Linkde List random access坐标, 是很难得: 所以需要把一半 ListNode 翻转
- reverse linked list: 遍历接开头
- 用快慢指正找到mid point
- Time O(n), 而且不需要用额外的空间(只是调换半个list的内部顺序), 所以空间O(1)

#### Previous Note
- Palindrome都是要两边回溯相等
- linkedlist不能reverse iterating， 那么就reverse the list, 从中间开花作比较。



---

**13. [Reverse Linked List.java](https://github.com/awangdev/LintCode/blob/master/Java/Reverse%20Linked%20List.java)**      Level: Easy
      

#### Reverse List
- Linked List的基本操作: 每次insert在开头
- 用head来循环所有node
- 不需要额外空间
- Time O(n), Space O(1)



---

**14. [Reverse Linked List II .java](https://github.com/awangdev/LintCode/blob/master/Java/Reverse%20Linked%20List%20II%20.java)**      Level: Medium
      

reverse 一个 linked list 中  [m ~ n] 的一部分.

#### Reverse linked list
- 在基本的reverse linked list 上面 多了一层: 找到front node,  接下来的 [m ~ n] node 需要被reverse
- 只需要reverse中间的部分.
- Reverse的时候: 用一个dummyNode, 这道题里面, 其实就用 nodeFront, 那么 dummy.next 就是整个reversed list.

##### 注意
- 一定要Mark开头的那个mth node, 最后用它接上 剩下node tail. 不然后面的node会断掉

#### Previous notes
- 遍历到M前，
- 存一下那个点，
- 从M开始， for loop， reverse [m~n]。 然后把三段链接在一起。




---

**15. [Merge Two Sorted Lists.java](https://github.com/awangdev/LintCode/blob/master/Java/Merge%20Two%20Sorted%20Lists.java)**      Level: Easy
      

如题

#### Basics
- 小的放前。每次比head大小 
- while过后，把没完的list一口气接上。   
- 一开始建一个node用来跑路, 每次都存node.next = xxx。存一个dummy。用来return dummy.next.



---

**16. [LRU Cache.java](https://github.com/awangdev/LintCode/blob/master/Java/LRU%20Cache.java)**      Level: Hard
      

#### Double Linked List
- 用了一个特别的双向的ListNode，有了head和tail，这样就大大加快了速度。     
- 主要加快的就是那个‘更新排位’的过程，找到item hashmap O(1), 做减法换位也都是O(1)
- Overall O(1)

##### 巧妙点
- 1. head和tail特别巧妙：除掉头和尾，和加上头和尾，就都特别快。    
- 2. 用双向的pointer: pre和next, 当需要除掉任何一个node的时候，只要知道要除掉哪一个，     
- 直接把node.pre和node.next耐心连起来就好了，node就自然而然的断开不要了。     
- 一旦知道怎么解决了，就不是很特别，并不是难写的算法:    
- moveToHead()    
- insertHead()    
- remove()      

#### O(n) 检查重复
- timeout method, 天真的来了一个O(n) 的解法，结果果然timeout.     
- 一个map<key,value>存数值。一个queue<key>来存排位。     
- 每次有更新，就把最新的放在末尾；每次超过capaticity,就把大头干掉。很简单嘛，但是跑起来太久，失败了。     




---

**17. [Remove Duplicates from Sorted List.java](https://github.com/awangdev/LintCode/blob/master/Java/Remove%20Duplicates%20from%20Sorted%20List.java)**      Level: Easy
      

从Linked list 里面摘掉重复元素, 只留下unique元素.

#### Linked List
- sorted list, 重复元素都在一起
- 知道如何构建Linked List.
- 一点遇到重复元素: node.val == node.next.val, 就去掉.
- 用一个dummy node 来跑路
- 注意:
- 只有当没有重复的时候, 才node = node.next; 
- 有重复的时候, 当后面第三个元素被提上来之后, 还是可能跟当下元素重复, 所以不能前移node.
- ex: A -> A -> A
- while loop 里面check node 和 node.next 比较好, 这样ending position会非常清晰



---

**18. [Remove Duplicates from Sorted List II.java](https://github.com/awangdev/LintCode/blob/master/Java/Remove%20Duplicates%20from%20Sorted%20List%20II.java)**      Level: Medium
      

从Linked list 里面摘掉重复元素: 只要重复过, 全部都删掉; 重复出现过得元素一个不留.

#### Linked List
- sorted list, 重复元素都在一起
- 运用 dummyHead: 如果要去掉所有重复元素, 就要有个dummyHead作为局外人在开头牵线
- 只要发现一个 node.val == node.next.val, 就记下这个duplicated val, move forward, 过掉所有重复过的元素
- 思想:
- 用第二个 inner while loop, 把所有的重复元素都处理干净, 然后再move forward
- 优点: outter while loop 不需要考虑太多case, 在inner loop 都把主要的business logic 解决了.

##### 注意DummyHead 的使用
- 当我们有了DummyHead 作为Linked List 的局外线头, 其实可以选择每次遇到duplicate, 就把更加后面的元素 强行assign 给 dummyHead.next 
- 下面还尝试过一种做法: 但是需要考虑的edge case 太多了: 不断移动node, 知道不重复, assign prev.next = node. 
- 这样的做法比较直白, 但是需要考虑很多edge case, 而且并没有很好利用到 dummy head, 注意规避.

##### Previous Note
- 斩草除根。
- 多个node，check node.next ?= node.next.next




---

**19. [Rotate List.java](https://github.com/awangdev/LintCode/blob/master/Java/Rotate%20List.java)**      Level: Medium
      

给一个single linked list, 右移k steps. k non-negative.

#### Linked List basics
- 记得用dummy.next来存head.
- 特殊: 这里k可能大于list总长. 写一写linked node 移动的步数, 然后 k = k % n.
- 找到newTail, newHead, 然后利用dummy, 换位子



---




 
 
 
## Stack (20)
**0. [Binary Search Tree Iterator.java](https://github.com/awangdev/LintCode/blob/master/Java/Binary%20Search%20Tree%20Iterator.java)**      Level: Medium
      

画一下, BST in order traversal. 用stack记录最小值, 放在top. O(h) space.
每次消耗TreeNode, 都看看rightNode(其实就是下一个最小的candidate), 并且一条龙stack叠上rightNode所有的left子孙.

Previous Notes:
用O(h)空间的做法：

理解binary search tree inorder traversal的规律：
   先找left.left.left ....left 到底，这里是加进stack.
   然后考虑parent,然后再right.

例如这题：
   stack里面top，也就是tree最左下角的node先考虑,取名rst.
   其实这个rst拿出来以后, 它也同时是最底层left null的parent，算考虑过了最底层的parent。
   最后就考虑最底层的parent.right, 也就是rst.right.

注意:
   next()其实有个while loop, 很可能是O(h).题目要求average O(1),所以也是okay的.


用O(1)空间的做法：不存stack, 时刻update current为最小值。

找下一个最小值,如果current有right child：   
   和用stack时的iteration类似,那么再找一遍current.right的left-most child,就是最小值了。
   
如果current没有right child:    
    那么就要找current node的右上parent, search in BinarySearchTree from root.

注意：
   一定要确保找到的parent满足parent.left == current.
   反而言之，如果current是parent的 right child, 那么下一轮就会重新process parent。
   但是有错:binary search tree里面parent是小于right child的，也就是在之前一步肯定visit过，如此便会死循环。




---

**1. [Flatten Nested List Iterator.java](https://github.com/awangdev/LintCode/blob/master/Java/Flatten%20Nested%20List%20Iterator.java)**      Level: Medium
      

方法1: 用queue, 把需要的item全部打出来
方法2: 用stack, 把需要的item先存一行, 每次打开子序列时候, 全部加回stack.



---

**2. [Trapping Rain Water.java](https://github.com/awangdev/LintCode/blob/master/Java/Trapping%20Rain%20Water.java)**      Level: Hard
      

这道题目的方法比较多.
#### 方法1
Array, 维持一个左手最高墙array, 右手最高强array.
对于每个index而言, vertically 能存放的最大水柱, 就是靠左右最高墙决定的:
min(leftHighestWall, rightHighestWall) - currHeight.

#### 方法2
方法1上面的优化, two pointer, 还是找左边最高和右边最高. O(1) space.
利用到了方法3里面的想法一样: 整个structure是被中间的最高bar 二分天下:
左边按照maxLeft来计算, 右边按照maxRight来计算.

#### 方法3
2 Pointers， 双面夹击:
1. 找中间最高bar的index    
2. 两面往中心扫：每次加上（topBarIndex - currIndex）* (elevation from previous index).也就是每次加一个横条。    
3. 每次还要减去block自身的height

#### 方法4
主要想法和方法3一致: 在山坡下坡的基础上, 一直用stack堆积bottom. 
最后遇到上升之前, 此时bottom可以用来跟stack之前堆积的所有下坡index做比较, 算跟他们高度相差的积水.
用了stack记录下坡, 然后用个while loop一挖到底的想法非常棒.




---

**3. [Min Stack.java](https://github.com/awangdev/LintCode/blob/master/Java/Min%20Stack.java)**      Level: Easy
      

双Stack：一个正常stack，另一个minStack存当下level最小值. 注意维护minStack的变化

另外. 如果要maxStack，也是类似做法



---

**4. [Implement Queue using Stacks.java](https://github.com/awangdev/LintCode/blob/master/Java/Implement%20Queue%20using%20Stacks.java)**      Level: Easy
      

#### 双Stack
画图, 知道最后maintain的stack是那个 reverseStack: pop(), peek(), empty() 都在这个stack上, 无需变换.
push()里面做stack和reverseStack的来回倾倒.
相比老的code, 在PUSH里面做倾倒, 更容易读.

#### Previous notes
双Stack. 一个是等于是queue，一个是backfillStack.
Tricky: 是在pop()和peek()的时候backfill, 并且要等到stack用完再backfill.
写一下例子就知道，如果提早backfill，stack.peek()就不是queue的head了.




---

**5. [Expression Expand.java](https://github.com/awangdev/LintCode/blob/master/Java/Expression%20Expand.java)**      Level: Medium
      

给一个expression string. 里面包括数字, 字母, 括号. 其中数字代表括号里面的内容重复几次.

括号里面可以是String, 也可能是expression.

目的: 把expression展开成一个正常的String.

#### DFS
- 与Stack时需要考虑的一些function类似. 特别之处: **检查[ ]的结尾**
- 因为DFS时候, 括号里的substring会被保留着进入下一个level, 所以我们在base level要keep track of substring.
- 用int paren 来track 括号的开合, 当paren再次==0的时候 找到closure ']'

#### Stack
- Stack存 [ ] 里面的内容, detect 括号开头结尾: 结尾时process inner string
- 有很多需要注意的细节才能做对:
- Stack<Object> 也可以用, 每个地方要注意 cast. 存进去的需要是Object: String, Integer
- 几个 type check: instanceof String, Character.isDigit(x), Integer.valueOf(int num)
- 出结果时候, 不能轻易 sb.reverse().toString(): sb.reverse() 翻转了整个连在一起的string, 错.
- 用另一个Stack<String>作为buffer, 先把stack里面的内容倒出来 (pure), 但是每个item里面顺序不变.
- 最后再从buffer里面倒进StringBuffer.




---

**6. [Largest Rectangle in Histogram.java](https://github.com/awangdev/LintCode/blob/master/Java/Largest%20Rectangle%20in%20Histogram.java)**      Level: Hard
      

给n个bar,组成柱状图histogram. 求在这一排柱状图里面可以找到的面积最大的长方形.

思考: 找长方形面积, 无非是找两个index, 然后底边长度 * height.

#### Monotonous Stack
- 重点是根据找Histogram里面rectangle的性质, 维持一个单调递增的Stack
- 在loop over indexes的时候:
- 如果高度>= previous peek(), 那么对于那个peek, 就意味着, 往下走, 一直走高嘛, 之前的peek总可以继续抄底
- 什么时候不能抄底了呢? 就是有一个下降趋势的时候
- 这时候并不是calculate所有前面的peek, 而是考虑 大于 current height的之前所有的peek.
- 把这些peek到 current height 前一格的rectangle全部找出来: stack.pop()
- 这个stack.pop()的过程里面, 其实没有算上 current height, 因为需要留到下一轮, 把current index加进stack 再说
- 为什么用stack? 因为需要知道连续递增的peek, stack.peek() O(1), 好用
  而其实不用stack, 也可以用其他方式记录所有height, 只不过要 O(n)去找peek不方便

#### 知识点
- 理解monotonous stack 是如何被维护的
- 维护monotonous stack 是题目需要, 而不是stack本身性质, 是一种借助 stack.peek() O(1)的巧妙用法.




---

**7. [Maximum Binary Tree.java](https://github.com/awangdev/LintCode/blob/master/Java/Maximum%20Binary%20Tree.java)**      Level: Medium
      

给一串数字, 做一个 maximum binary tree: 最顶上的root最大; 左child也是一个max tree, 右child也必须是max tree.

#### Monotonous Stack
- 用到bottom->top递减的stack: 最底下的root维持成最大的element.
- 过程当中, 一旦遇到currNode.val > stack.peek(), 就意味着需要把这个currNode放在 stack的底层位置.
- 也就是说, 遇到这个条件, process, pop()所有 currNode.val > stack.peek(), 最后把currNode加进去.

- maxTree题目本身的要求是: 大的在最中间, 左右两边的subTree也要是maxTree:
- Monotonous Stack在这里帮助 keep/track of max value, 但是left/right tree的logic是MaxTree独有的.
- left/right node的assignment是根据题目要求: 中间最大值分开后, 左边的是左边subTree, 右边的作为右边subTree.

#### Previous notes
- Should memorize MaxTree. 依次类推，会做Min-Tree, Expression Tree
- Stack里，最大的值在下面。利用此性质，有这样几个step:

##### Step1
- 把所有小于curr node的，全Pop出来, while loop, keep it going.    
- 最后pop出的这个小于Curr的node：它同时也是stack里面pop出来小于curr的最大的一个，最接近curr大小。（因为这个stack最大值靠下面）    
- 把这个最大的小于curr的node放在curr.left.    

##### Step2   
- 那么，接下去stack里面的一定是大于curr：   
- 那就变成curr的left parent. set stack.peek().right = curr.

##### Step3   
- 结尾：stack底部一定是最大的那个，也就是max tree的头。





---

**8. [Maximal Rectangle.java](https://github.com/awangdev/LintCode/blob/master/Java/Maximal%20Rectangle.java)**      Level: Hard
      

#### 方法1: monotonous stack
分解开来, 其实是'Largest Rectangle in Histogram', 只不过这里要自己model heights.
一个2D array里面的rectangle, 最终也是用height * width做出来的.
巧妙在于, 把每一行当做底边, 算出这个底边, 到顶部的height: 
- 如果底边上的一个value==0, 那么算作没有height(以这个底边做rectangle, value==0的位置是空中楼阁, 不能用)
- 如果底边上的value==1, 那么就把上面的height加下来, 做成histogram

如果看具体实例, 有些row似乎是白算的, 但是没有办法, 这是一个搜索的过程, 最终会比较出最优解.

#### 方法2: DP
Coordinate DP?



---

**9. [Binary Tree Inorder Traversal.java](https://github.com/awangdev/LintCode/blob/master/Java/Binary%20Tree%20Inorder%20Traversal.java)**      Level: Easy
      

Inorder traverse Binary Tree

#### Recursive
- 在自己的基础上recursive, 不用helper function
- Divide and Conquer, with helper(dfs) method
- O(n) time, no extra space

#### Iterative: Stack
- Add left nodes all the way   
- Print curr   
- Move to right, add right if possible
- O(n) time, O(h) space
  
注意stack.pop()在加完left-most child 的后，一定要curr = curr.right.

若不右移, 很可能发生窘境:
curr下一轮还是去找自己的left-most child，不断重复curr and curr.left, 会infinite loop, 永远在左边上下上下。

#### HashMap
? How?



---

**10. [Binary Tree Postorder Traversal.java](https://github.com/awangdev/LintCode/blob/master/Java/Binary%20Tree%20Postorder%20Traversal.java)**      Level: Medium
      

如题, POST-ORDER traversal.

LeetCode给了hard, 应该是觉得stack的做法比较难想到.

#### Recursive
trivial, 先加left recursively, 再加right recursively, 然后组成头部.

#### Stack
- 双stack的思想, 需要在图纸上画一画
- 原本需要的顺序是: 先leftChild, rightChild, currNode.
- 营造一个stack, reversely process: 先currNode, 再rightChild, 再leftChild
- 这样出来的结果是reverse的, 那么翻转一下就可以了.
- v1做的时候用了stack1, stack2, 因为根据这个双stack的思想而来
- v2简化, 可以放在一个stack里面, 每次record result 的时候: rst.add(0, item);

##### 利用stack的特点
- 每次加element进stack的时候, 想要在 bottom/后process的, 先加
- 想要下一轮立刻process的, 最后push进stack.

##### 注意
这些binary tree traversal的题目.常常有多个做法:recursive or iterative



---

**11. [Binary Tree Preorder Traversal.java](https://github.com/awangdev/LintCode/blob/master/Java/Binary%20Tree%20Preorder%20Traversal.java)**      Level: Easy
      

#### Recursive
- 加root, left, then right. Obvious
- Divide and conquer
- 其实也不需要helper function

#### Iterative
- 先加root, 然后push上需要末尾process的在stack垫底(root.right), 然后push root.left
- Stack: push curr, push right, push left.   



---

**12. [Expression Tree Build.java](https://github.com/awangdev/LintCode/blob/master/Java/Expression%20Tree%20Build.java)**      Level: Hard
      

给一串字符, 表示的是 公式 expression. 把公式变成expression tree

#### Monotonous Stack
- 和Max-tree一样，https://leetcode.com/problems/maximum-binary-tree
- 用到bottom->top递增的stack: 最底下的root维持成最小的element.
- 这个题目是Min-tree， 头上最小，Logic 和max-tree如出一辙   
- Space: O(n) 
- Time on average: O(n).

#### 特点
- TreeNode: 用一个并不是最终结果的TreeNode, 存weight, 用来排序
- 用base weight的概念权衡同一个层面的 符号, 数字 顺序
- 每一个character都是一个节点, 都有自己的weight. 用一个TreeNode来存weight value, 利用用weight来判断: 
- 1. (while loop) 如果node.val <= stack.peek().nodeValue, 把当前stack.peek() 变成 left child. 
- 2. (if condition) 如果stack有残余, 把当前node变成 stack.peek().rightChild 




---

**13. [Expression Evaluation.java](https://github.com/awangdev/LintCode/blob/master/Java/Expression%20Evaluation.java)**      Level: Hard
      

给一个公式 expression, array of strings, 然后evaluate expression 结果.

#### DFS on Expression Tree
- 计算 expression 的值: 1. 建造 expression tree. 2. DFS计算结果
- Expression Tree: Minimum Binary Tree (https://lintcode.com/en/problem/expression-tree-build/)
- build好Min Tree以后，做PostTraversal. 
- Divde and Conquer: 先recursively找到 left和right的大小， 然后evaluate中间的符号
- Time, Space O(n), n = # expression nodes

### Note
- 1. Handle数字时，若left&&right Child全Null,那必定是我们weight最大的数字node了。   
- 2. 若有个child是null,那就return另外一个node。    
- 3. prevent Integer overflow　during operation:过程中用个Long，最后结局在cast back to int.



---

**14. [Convert Expression to Polish Notation.java](https://github.com/awangdev/LintCode/blob/master/Java/Convert%20Expression%20to%20Polish%20Notation.java)**      Level: Hard
      

给一串字符, 用来表示公式expression. 把这个expression转换成 Polish Notation (PN).

#### Expression Tree
- Expression Tree: Minimum Binary Tree (https://lintcode.com/en/problem/expression-tree-build/)
- 根据题意做出Expression Tree出来以后: 来个Pre-order-traversal 就能记录下 Polish Notation
- 本题没有给'ExpressionTreeNode', 所以把TreeNode就当做成我们需要的node, 里面扩展成有left/right child就可以了.
- Note: label需要是String. 虽然 Operator是长度为1的char, 但是数字可为多位



---

**15. [Convert Expression to Reverse Polish Notation.java](https://github.com/awangdev/LintCode/blob/master/Java/Convert%20Expression%20to%20Reverse%20Polish%20Notation.java)**      Level: Hard
      

给一串字符, 用来表示公式expression. 把这个expression转换成 Reverse Polish Notation (RPN).

#### Expression Tree
- Expression Tree: Minimum Binary Tree (https://lintcode.com/en/problem/expression-tree-build/)
- 根据题意做出Expression Tree出来以后: 来个Post-order-traversal 就能记录下 Reverse Polish Notation
- 本题没有给'ExpressionTreeNode', 所以把TreeNode就当做成我们需要的node, 里面扩展成有left/right child就可以了.



---

**16. [Evaluate Reverse Polish Notation.java](https://github.com/awangdev/LintCode/blob/master/Java/Evaluate%20Reverse%20Polish%20Notation.java)**      Level: Medium
      

给一个 RPN string list, 根据这个list, 计算结果.

#### Stack
- stack 里面 存数字
- 每次遇到operator, 都拿前2个数字计算
- 计算结果存回到stack里面, 方便下一轮使用.
- Time,Space O(n)




---

**17. [Implement Stack using Queues.java](https://github.com/awangdev/LintCode/blob/master/Java/Implement%20Stack%20using%20Queues.java)**      Level: Easy
      

如题.

#### Queue, 倒水
- 两个Queue,交互倒水
- 用一个Temp做swap

##### 做法1
- 逻辑在push里面:
- 1. x 放q2。
- 2. q1全部offer/append到q2.
- 3. 用一个Temp做swap q1, q2.
- q1的头，就一直是最后加进去的值.


##### 做法2
- 逻辑在top()/pop()里, 每次换水，查看末尾项.




---

**18. [Implement Stack.java](https://github.com/awangdev/LintCode/blob/master/Java/Implement%20Stack.java)**      Level: Easy
      

随便用一个data structure, implement stack.

#### Stack, 先入, 后出
- ArrayList: return/remove ArrayList的末尾项。
- 2 Queues



---

**19. [Basic Calculator.java](https://github.com/awangdev/LintCode/blob/master/Java/Basic%20Calculator.java)**      Level: Hard
      

给一个expression String, 要evaluate这个expression的值.

Expression string 里面包括 +, -, 整数, 开合括号, 还有space.

#### Expression Tree
- Expression Tree是一个 weight-based的 min-tree 
- 基于 运算符号 + 数字的 tree: 数字永远在leaf, 然后符号是tree node,  括号不出现在tree里面
- 用 monotonuous stack 来构建这个tree

##### Thinking points
- Understand Expression Tree
- Use stack to build the expression tree + understand the weight system
- Use post-order traversal to evaluate the tree
- 注意, input里面的数字不会是single digit, 所以需要一个buffer存number string
- 整个题目的做法, 可以参照 `Expression Evaluation`



---




 
 
 
## Binary Indexed Tree (1)
**0. [Building Outline.java](https://github.com/awangdev/LintCode/blob/master/Java/Building%20Outline.java)**      Level: Review
      

又叫做skyline. 用Sweep Line做的O(nLogN), 但是貌似还有很多做法: segement tree, hashheap, treeSet?

#### 方法1: Sweep Line, Time O(nLogN), Space O(n)
original reference http://codechen.blogspot.com/2015/06/leetcode-skyline-problem.html?_sm_au_=isVmHvFmFs40TWRt

sweep line:
- 把所有点分出来， 每个点有index x, 再加上一个height.         
- 在这个list上排序，根据index和height. 注意用负数标记building start point height, 这样保证start在end 之前
- 用负数的height标记start: 在priority queue里面同一个x-pos比较 startPoint.height, endPoint.height 的时候, 因为end height是整数, 所以compare时会自动把start point放在end point前面
- 当然了, 如果两个 start point比较, 第二个point的负数超大的话(也就是height很高), 就会顺理compare return正数, 成章形成倒位
- 在processs时候用max-heap (reversed priorityqueue)，再iterate heightPoints 来存最大的height . 遇到peek,就是一个合理的解    
- heightQueue里面加一个0, 用来在结尾的时候做closure

#### 方法2: Segment Tree
REVIEW

Binary Indexed Tree?

HashHeap?



---




 
 
 
## Graph (5)
**0. [Clone Graph.java](https://github.com/awangdev/LintCode/blob/master/Java/Clone%20Graph.java)**      Level: Medium
      

给一个graph node, 每个node有list of neighbors. 复制整个graph, return new head node.

#### 思想
- Use HashMap to mark cloned nodes.    
- 先能复制多少Node复制多少. 然后把neighbor 加上

#### DFS
- copy the node
- Mark 'added' using map(old, new)
- for loop on the each one of the neighbors: map copy, record in map, and further dfs
- once dfs completes, add newNeighbor as neighbor of the new node (get to it via map)
- 主要思想是: 一旦复制过了, 不必要重新复制

#### BFS
_ Copy the root node, then copy all the neighbors. 
_ Mark copied node in map.
_ Use queue to contain the newly added neighbors. Need to work on them in the future.

#### Note
initialize map with (node, newNode)



---

**1. [Graph Valid Tree.java](https://github.com/awangdev/LintCode/blob/master/Java/Graph%20Valid%20Tree.java)**      Level: Review
      

M 

给一个数字n代表n nodes, marked from 1 ~ n, 和一串undirected edge int[][]. 检查这些edge是否能合成一个 valid tree

#### Union Find
- 复习Union-Find的另外一个种形式, track union size
- 题目类型：查找2个元素是不是在一个union里面。如果不在，false. 如果在，那就合并成一个set,共享parent.   
- 存储的关键都是：元素相对的index上存着他的root parent.    
- 注意: 结尾要检查, 是否只剩下1个union: Tree必须连接到所有给出的node.
- 另一个union-find, 用hashmap的:
- http://www.lintcode.com/en/problem/find-the-weak-connected-component-in-the-directed-graph/

#### DFS
- (还没做, 可以写一写)
- 检查: 1. 是否有cycle, 2. 是否所有的node全部链接起来

#### BFS
- (还没做, 可以写一写)
- 也是检查: 1. 是否有cycle, 2. 是否所有的node全部链接起来



---

**2. [Course Schedule.java](https://github.com/awangdev/LintCode/blob/master/Java/Course%20Schedule.java)**      Level: Medium
      

- 一堆课用int[2] pair 来表示. [1, 0] 表示要上课1的话, 必须先把课0上了. 
- 每一个数字都是一个ndoe, 题目问是否能把所有的课排了
- input是 numOfCourses, 还有这个prerequisites [[]]

#### Topological Sort
- 给一个graph of nodes
- 至关重要: 用`List[] edges; edges[i] = new ArrayList<>();` 来表示graph: 就是每个node, to all its neighbors
- 目标是根据edge 的 direction, 把这个graph 里面的 node sort 一个list
- 如果有cycle, 这个item就不会被放在最后的list 里面. 
- 比如: 如果两个课互相是dependency, 就变成了cyclic dependency, 这样不好.


#### BFS
- Kahn algorithem:
- 先build一个graph map: <node, list of nodes >; or `List[] edges; edges[i] = new ArrayList<>();`
- count in-degree: inDegree就是每个node上面, 有多少个走进来的edge?
- 那些没有 in-coming-edge的, indegree 其实就 等于 0, 那么他们就应该在final result list里面
- 对这些 indegree == 0 的 nodes BFS, add to queue.
- 模拟visit每个ndoe, 如果visit过了, 这个node上的 indegree--, 然后如果最终 indegree == 0, 这个node就成功进入final list.

##### Indegree 原理
- Note: 如果有cycle, indegree是不会变成0的, 它也无法进入最终list. 
- indegree是周围的node到我这里的次数count. 
- 如果周围所有node的连线, 都意义切除后, 我的indegree还不等于0, 那么肯定有某些node间接地有重复连线, 也就是有cycle

#### DFS
- 这道题没有要求作出final list, 相对简单, 只要visit每个nodes, 最后确认没有cycle就好了
- 用 visited int[] 来确认是否有cycle. 1 代表 paretNode visited, -1 代表在DFS上一行的标记
- 如果遇到-1, 说明这个node在上一级或者以上的同一个dfs path里面已经走过, 那么证明有cycle, return false.
- 走完一个node的所有neighbor, 都没有fail, 那么backtracking, set visited[i] = 1
- 真的topo sort会在DFS的底端, 把record放进一个stack, 最后reverse, 就是真的sort order.

#### Notes:
- 还有 List[] arrayOfList = new ArrayList[]; 这样的操作啊, 代替了map<integer, integerList>

#### Previous notes
有点绕，但是做过一次就明白一点。    
是topological sort的题目。一般都是给有dependency的东西排序。    

最终都会到一个sink node， 再不会有向后的dependency, 在那个点截止。    
我就已这样子的点为map的key, 然后value是以这个node为prerequisite的 list of courses.    

画个图的话，prerequisite都是指向那个sink node， 然后我们在组成map的时候，都是从sink node 发散回来到dependent nodes.    

在DFS里面，我们是反向的， 然后，最先完全visited的那个node, 肯定是最左边的node了，它被mark的seq也是最高的。    

而我们的sink node，当它所有的支线都visit完了，seq肯定都已经减到最小了，也就是0，它就是第一个被visit的。   


最终结果：
每个有pre-requisit的node都trace上去（自底向上），并且都没有发现cycle.也就说明schedule可以用了。



---

**3. [Course Schedule II.java](https://github.com/awangdev/LintCode/blob/master/Java/Course%20Schedule%20II.java)**      Level: Medium
      

- 一堆课用int[2] pair 来表示. [1, 0] 表示要上课1的话, 必须先把课0上了. 
- 每一个数字都是一个ndoe, 题目求这个最后排好的课的list
- 如果排不好, 就给个空就好
- input是 numOfCourses, 还有这个prerequisites [[]]
- 做法跟Course Schedule I 非常像, 可以参考.

#### Topological Sort, Indegree, BFS
- 用`List[] edges; edges[i] = new ArrayList<>();` 来表示graph: 就是每个node, to all its neighbors
- 每个没有 inDegree==0 node, 都是可以加进 final list里面的. 比如一开始找到的那些 inDegree = 0的 node
- 注意, 如果 prerequisites = [], 那么就是说这些课都independent, 开个int[0 ~ n-1]的数组并赋值就好.
- 如果有cycle, 严格意义上就做不了topological sort, 也无法涵盖所有nodes,  那么return [ ]

#### DFS
- 根据 Course Schedule 里面的DFS 修改
- 维持visited int[]全局变量
- 维持sortedList int[] 全局变量, 注意加进去的时候是 add(0, node) 加在开头这样
- 每次到一个node的children全部DFS走完之后, 就可以把他加进final list里面
- 如果有cycle, 也就是dfs return false的时候, 这个题目判定排课失败, return new int[] { }



---

**4. [Alien Dictionary.java](https://github.com/awangdev/LintCode/blob/master/Java/Alien%20Dictionary.java)**      Level: Hard
      

给一个 array of strings: 假如这个array是按照一个新的字母排序表(alien dictionary)排出来的, 需要找到这个字母排序.

有可能有多重排序的方法, 给出一种就可以.

#### Graph
- 本质: 上下两行string, 相对应的相同的index上, 如果字母不同, 就说明排在第一行的字母在字母表里更领先
- 把 string array 变成topological sort的 graph: `map<char, list<char>>`
- 也可以`List[26] edges` (Course Schedule problem)
- Build edges: find char diff between two row, and store the order indication into graph
- 注意: indegree 永远是反向的 (跟 node to neighbors 相反的方式建立)

#### BFS
- topological sort 本身很好写, 但是要在题目中先了解到字母排序的本质
- 其实上面这个排序的本质很好想, 但是把它具体化成构建graph的代码, 会稍微有点难想到
- 算indegree, 然后用 BFS 来找到那些 inDegree == 0的 node
- 最先inDegree == 0的node, 就排在字母表前面.
- 下面的解法, 用了Graph: map<Character, List<Character>>, 而不是 List[26], 其实更加试用超过26个字母的dictionary.

#### DFS
- 跟BFS建立 grpah 的过程一模一样
- DFS的不同在于: 用visited map 来标记走过的地方
- 走到leaf的时候, add to result: 但因为走到了底才add, 最终的顺序应该颠倒 (或者, sb.insert(0, x) 直接用颠倒的顺序add)



---




 
 
 
## Brainteaser (1)
**0. [Nim Game.java](https://github.com/awangdev/LintCode/blob/master/Java/Nim%20Game.java)**      Level: Easy
      

#### Brainteaser
- 著名Nim游戏
- 写一些，发现n=4,5,6,7,8...etc之后的情况有规律性: 谁先手拿到4就输了.
- 最终很简单n%4!=0就可以了,  time, space O(1)

#### DP
- 正规地找规律做, 就跟 coins in a line 一样, 按照先手后手来做
- 可以rolling array 优化空间
- Time O(n), 当然啦, 这个题目这样会timeout, 可以使用brainteaser的做法写出结果.



---




 
 
 
## Union Find (8)
**0. [Connecting Graph.java](https://github.com/awangdev/LintCode/blob/master/Java/Connecting%20Graph.java)**      Level: Medium
      

没有跑过这个程序, 是一个UnionFind的简单实现.
Document了每个环节的计算原理/思想.



---

**1. [Connecting Graph II.java](https://github.com/awangdev/LintCode/blob/master/Java/Connecting%20Graph%20II.java)**      Level: Medium
      

Lint还不能跑, 全部按照题意和答案document的.



---

**2. [Connecting Graph III.java](https://github.com/awangdev/LintCode/blob/master/Java/Connecting%20Graph%20III.java)**      Level: Medium
      

还是UnionFind的变形, 这次是算有剩下多少个union. 其实非常简单, 维持一个全局变量count:
一开始count=n, 因为全是散装elements;  每次union, count--.



---

**3. [Number of Islands.java](https://github.com/awangdev/LintCode/blob/master/Java/Number%20of%20Islands.java)**      Level: Medium
      

给一个2Dmatrix, 里面是1和0, 找#of island.


#### DFS
- top level 有一个 double for loop, 查看每一个点.
- 每当遇到1, count+1, 然后DFS helper function 把每个跟这个当下island 相关的都Mark成 '0'
- 这样确保每个visited 过得island都被清扫干净

#### Union Find
- 可以用union-find， 就像Number of island II 一样。
- 只不过这个不Return list, 而只是# of islands
- 记住UnionFind的模板和几个变化(Connecting Graph I, II, III), 最后归总的代码写起来就比较简单.



---

**4. [Number of Islands II.java](https://github.com/awangdev/LintCode/blob/master/Java/Number%20of%20Islands%20II.java)**      Level: Hard
      

方法1: 
用int[] father 的unionFind, 需要转换2D position into 1D index.
count的加减, 都放在了UnionFind自己的function里面, 方便tracking, 给几个helper function就对了.
这样比较clean
Time: O(k * log(mn))

方法2: 
用HashMap的Union-find.

把board转换成1D array， 就可以用union-find来判断了。 判断时，是在四个方向各走一步，判断是否是同一个Land.
每走一次operator，都会count++. 若发现是同一个island, count--

Side Note:
Proof of UnionFind log(n) time: 
https://en.wikipedia.org/wiki/Proof_of_O(log*n)_time_complexity_of_union%E2%80%93find




---

**5. [Graph Valid Tree.java](https://github.com/awangdev/LintCode/blob/master/Java/Graph%20Valid%20Tree.java)**      Level: Review
      

M 

给一个数字n代表n nodes, marked from 1 ~ n, 和一串undirected edge int[][]. 检查这些edge是否能合成一个 valid tree

#### Union Find
- 复习Union-Find的另外一个种形式, track union size
- 题目类型：查找2个元素是不是在一个union里面。如果不在，false. 如果在，那就合并成一个set,共享parent.   
- 存储的关键都是：元素相对的index上存着他的root parent.    
- 注意: 结尾要检查, 是否只剩下1个union: Tree必须连接到所有给出的node.
- 另一个union-find, 用hashmap的:
- http://www.lintcode.com/en/problem/find-the-weak-connected-component-in-the-directed-graph/

#### DFS
- (还没做, 可以写一写)
- 检查: 1. 是否有cycle, 2. 是否所有的node全部链接起来

#### BFS
- (还没做, 可以写一写)
- 也是检查: 1. 是否有cycle, 2. 是否所有的node全部链接起来



---

**6. [Surrounded Regions.java](https://github.com/awangdev/LintCode/blob/master/Java/Surrounded%20Regions.java)**      Level: Review
      

给一个2D board, 里面是 'X' 和 'O'. 把所有被X包围的area都涂成'X'. 

从四个边的edge出发, 像感染僵尸病毒一样扩散, 把靠边的node全部mark, 然后将还是'O'的改成X, 最后回复marks -> 'O'

#### Union Find
- UnionFind里面这次用到了一个rank的概念, 需要review. rank[] 也就是在tracking每一个node所在union的size.
- 目的是: always并到大的union里面
- note: 将2D coordinate (x,y) 转换成1D: index = x * n + y

#### DFS
- TODO

#### BFS
- TODO




---

**7. [Longest Consecutive Sequence.java](https://github.com/awangdev/LintCode/blob/master/Java/Longest%20Consecutive%20Sequence.java)**      Level: Hard
      

给一串数字, unsorted, 找这串数字里面的连续元素序列长度 (consecutive序列, 是数字连续, 并不是说要按照原order)

#### HashSet
- 要想看连续元素, 必须要num++, num--这样搜索
- 1. 需要O(1)找到元素
- 2. 需要简单快速找到 num - 1, num + 1.
- 如果用min,max开array, 耗费空间
- 用HashSet来存, 用set.contains() 来查找 num - 1, num + 1 存在与否
- for loop. O(n) 
- 里面的while loop 一般不会有O(n); 一旦O(n), 也意味着set 清零, for loop也不会有更多 inner while 的衍生.
- overall O(n) 时间复杂度


#### Union Find
- 最终是要把相连的元素算一下总长, 其实也就是把元素group起来, 相连的group在一起, 于是想到UnionFind
- 这里用到了一个`int[] size` 来帮助处理 `合并的时候parent是哪个`的问题: 永远往group大的union里去
- main function 里面, 有一个map来track, 每个元素, 只处理1遍.
- union的内容: current number - 1, current number + 1
- https://www.jianshu.com/p/e6b955ca208f

##### 特点
- Union Find 在index上做好像更加容易
- 其他union find function: `boolean connected(a,b){return find(a) == find(b)}`



---




 
 
 
## Sweep Line (5)
**0. [Meeting Rooms.java](https://github.com/awangdev/LintCode/blob/master/Java/Meeting%20Rooms.java)**      Level: Easy
      

- 注意接头点要考虑所有开会结会的情况，不要恰巧漏掉相接的点
- 开会的是超人。瞬间移动接上下一个会议

#### 方法1:
找是否有overlap. priorityQueue 按照start time排序好以后, 比较current和peek: current.end > peek.start?

#### 方法2: Sweep line
- class Point{pos, flag}, PriorityQueue排序。计算count
- 跟 Number of Airplanes in the Sky 是一个类型的题目





---

**1. [Number of Airplane in the sky.java](https://github.com/awangdev/LintCode/blob/master/Java/Number%20of%20Airplane%20in%20the%20sky.java)**      Level: Medium
      

#### Sweep Line
- 把Interval拆分成数轴上的Point 
- 起飞mark 1   
- 降落mark -1     
- 用PriorityQueue排序， loop through queue, 计算(起飞+降落)值可能有的max。

#### 注意
- 同时起飞和降落，就是 1 - 1 = 0. 所以在while loop里面有第二个while loop，    
- 当坐标x重合时，在这里做完所有x点的加减，然后再比较 max。     
- 这避免了错误多count，或者少count



---

**2. [Meeting Rooms II.java](https://github.com/awangdev/LintCode/blob/master/Java/Meeting%20Rooms%20II.java)**      Level: Medium
      

给一串数字pair, 代表会议的开始/结束时间. 找同时又多少个会议发生(需要多少件房间)

#### 方法1
- PriorityQueue + 一个Class来解决.Ｏ(nlogn)
- 跟 Number of Airpline in the sky是同一道题

#### 方法2: 尝试了一下用一个sorted Array + HashMap
也还行，但是handle edge的时候,HashMap 要小心，因为相同时间start和end的map key 就会重复了。



---

**3. [Building Outline.java](https://github.com/awangdev/LintCode/blob/master/Java/Building%20Outline.java)**      Level: Review
      

又叫做skyline. 用Sweep Line做的O(nLogN), 但是貌似还有很多做法: segement tree, hashheap, treeSet?

#### 方法1: Sweep Line, Time O(nLogN), Space O(n)
original reference http://codechen.blogspot.com/2015/06/leetcode-skyline-problem.html?_sm_au_=isVmHvFmFs40TWRt

sweep line:
- 把所有点分出来， 每个点有index x, 再加上一个height.         
- 在这个list上排序，根据index和height. 注意用负数标记building start point height, 这样保证start在end 之前
- 用负数的height标记start: 在priority queue里面同一个x-pos比较 startPoint.height, endPoint.height 的时候, 因为end height是整数, 所以compare时会自动把start point放在end point前面
- 当然了, 如果两个 start point比较, 第二个point的负数超大的话(也就是height很高), 就会顺理compare return正数, 成章形成倒位
- 在processs时候用max-heap (reversed priorityqueue)，再iterate heightPoints 来存最大的height . 遇到peek,就是一个合理的解    
- heightQueue里面加一个0, 用来在结尾的时候做closure

#### 方法2: Segment Tree
REVIEW

Binary Indexed Tree?

HashHeap?



---

**4. [Merge Intervals.java](https://github.com/awangdev/LintCode/blob/master/Java/Merge%20Intervals.java)**      Level: Medium
      

给一串int[Interval]. 把所以Interval merge起来.

#### Sweep Line
- O(nlogn)         
- 扫描线+Count无敌手。注意start end把interval给合起来。   
- count==0的时候，就是每次start end双数抵消的时候，就应该是一个interval的开头/结尾。写个例子就知道了。   
- 空间：O(2n) -> O(n)   
- 时间,priorityqueue: O(nlogn)   
- 记得怎么写comparator. New way: new PriorityQueue<>(Comparator.comparing(p -> p.val));
- 在 LeetCode里面，Sweep Line比方法2要快很多.

#### Sort Interval 
- Collections.sort() on interval.start之后，试着跑一遍，按照merge的需求，把需要merge的地方续好，然后减掉多余的interval就好。
- (不知为何LeetCode把Merge Interval, Insert Interval 标为Hard)
- Collections.sort(..., new comparator): sort by Interval.start.

- 画两个相连的Interval， prev, curr:
- prev只有 prev.end覆盖了 curr.start， 才需要merge. 那么比较一下, marege.     
- 记得如果merge, 一定要list.remove(i), 并且i--， 因为改变了List的大小。
- 若没有重合，就继续iteration: prev = curr. move on.

#### Sort Intervals and append end logically
- Sort intervals: O(nlogn)
- 找到结尾 interval, 满足条件就可以save
- 如果不到return的条件, 就继续延伸 interval.end



---




 
 
 
## Interval (1)
**0. [Number of Airplane in the sky.java](https://github.com/awangdev/LintCode/blob/master/Java/Number%20of%20Airplane%20in%20the%20sky.java)**      Level: Medium
      

#### Sweep Line
- 把Interval拆分成数轴上的Point 
- 起飞mark 1   
- 降落mark -1     
- 用PriorityQueue排序， loop through queue, 计算(起飞+降落)值可能有的max。

#### 注意
- 同时起飞和降落，就是 1 - 1 = 0. 所以在while loop里面有第二个while loop，    
- 当坐标x重合时，在这里做完所有x点的加减，然后再比较 max。     
- 这避免了错误多count，或者少count



---




 
 
 
## Sequence DP (14)
**0. [Coin Change.java](https://github.com/awangdev/LintCode/blob/master/Java/Coin%20Change.java)**      Level: Medium
      

给一串不同数额的coins, 和total amount to spent. 求 最少 用多少个coin可以组合到这个amount. 每种coins个数不限量.

#### DP
- 找对方程dp[x], 积累到amount x最少用多少个coin: #coin是value, index是 [0~x].
- 子问题的关系是: 如果用了一个coin, 那么就应该是f[x - coinValue]那个位置的#coins + 1

##### initialization
- 处理边界, 一开始0index的时候, 用value0. 
- 中间利用Integer.MAX_VALUE来作比较, initialize dp[x]
- 注意, 一旦 Integer.MAX_VALUE + 1 就会变成负数. 这种情况会在coin=0的时候发生.

##### Optimization
- 方法1: 直接用Integer.MAX_VALUE
- 方法2: 用-1, 稍微简洁一点, 每次比较dp[i]和 dp[i - coin] + 1, 然后save. 不必要做多次min比较.

#### Memoization
- dp[i] 依然表示: min # of coints to make amount i
- initialize dp[i] = Integer.MAX_VALUE
- 先选最后一步(遍历coins),  然后dfs做同样的操作
- 记录dp[amount] 如果已经给过value, 不要重复计算, 直接return.
- 但是这道题没必要强行做memoization, 普通DP的状态和方程相对来说很好找到



---

**1. [Longest Increasing Subsequence.java](https://github.com/awangdev/LintCode/blob/master/Java/Longest%20Increasing%20Subsequence.java)**      Level: Medium
      

无序数组, 找最长的上升(不需要连续)数组 的长度. 先做O(n^2), 然后可否O(nLogN)?

#### DP, double for loop, O(n^2)
- 考虑nums[i]结尾的时候, 在[0, i) 里count有多少小于nums[i]
- 对于所有 i in [0, n), 最常的increasing序列有多少length?
- max需要在全局维护: nums是无序的, nums[i]也可能是一个很小的值, 所以末尾dp[i]并不是全局的max, 而只是对于nums[i]的max.
- 正因此, 每个nums[i]都要和每个nums[j] 作比较, j < i.
- dp[i] = Maht.max(dp[i], dp[j] + 1); j = [0 , i - 1]
- 时间复杂度  O(n^2)


#### O(nLogN)
- 维持一个list of increasing sequence
- 这个list其实是一个base-line, 记录着最低的increasing sequence.
- 当我们go through all nums的时候, 如果刚好都是上升, 直接append
- 如果不上升, 应该去list里面, 找到最小的那个刚好大于new num的数字, 把它换成num
- 这样就完成了baseline. 举个例子, 比如替换的刚好是在list最后一个element, 等于就是把peak下降了, 那么后面其他的数字就可能继续上升.
- '维护baseline就是一个递增的数列' 的证明, 还没有仔细想.



---

**2. [Climbing Stairs.java](https://github.com/awangdev/LintCode/blob/master/Java/Climbing%20Stairs.java)**      Level: Easy
      

#### Recursive + Memoization
- 递归很好写, 但是重复计算, timeout. time: O(2^n)
- O(2^n): each n can spawn 2 dfs child, at next level, it will keep spawn. Total 2^n nodes will spawn.
- 用全局变量int[] memo 帮助减少重复计算
- O(n) time, space

#### DP
- 最后一步被前两种走法决定: dp[i] = dp[i - 1] + dp[i - 2]
- 基础sequence DP, int[] dp = int[n + 1];
- DP[]存的是以 1-based index的状态
- 需要知道dp[n] 的状态, 但是最大坐标是[n-1], 所以int[n+1]
- dp[0]往往是有特殊状态的
- O(n) space, time

#### 序列DP, 滚动数组
- [i] only associates with [i-2], [i-1].
- %2
- O(1) space



---

**3. [Coin Change 2.java](https://github.com/awangdev/LintCode/blob/master/Java/Coin%20Change%202.java)**      Level: Medium
      

给串数字, target amount, 求总共多少种方式可以reach the amount.

#### DP
- O(MN): M, total target amount; N: size of coins
- 状态: dp[i]: sum of ways that coins can add up to i.
- Function: dp[j] += dp[j - coins[i]];
- Init: dp[0] = 1 for ease of calculation; other dp[i] = 0 by default
- note: 避免重复count, 所以 j = coins[i] as start
- 注意 coins 可能需要放在for loop 外面, 而主导换coin的流程. 
- 类似于: 网格dp, unique path 里面的2种走法: 从上到下, 从左到右



---

**4. [Paint House.java](https://github.com/awangdev/LintCode/blob/master/Java/Paint%20House.java)**      Level: Easy
      

要paint n个房子, 还有 nx3的cost[][]. 求最少用多少cost paint 所有房子.

#### Sequence DP
- 求知道dp[n]的min cost, 但是不知道最后一个房子选什么颜色
- 那么就遍历最后一个房子(i - 1)的颜色
- 选中最后一个房子的颜色同时, 来选择 (i - 2)的颜色, 来找出最低的cost
- 考虑DP最后一个位置的情况. 发现给出了一些特殊条件, 需要附带在DP[i]上,
- 那么就定义二维数组

#### Rolling Array
- 观察发现 index[i] 只跟 [i-1] 相关, 所以2位就足够, %2


---

**5. [House Robber.java](https://github.com/awangdev/LintCode/blob/master/Java/House%20Robber.java)**      Level: Easy
      

搜刮房子, 相邻的不能碰. 每个房子里有value, 求max.

#### Sequence DP
- 看最后结尾状态的前一个或前两个的情况，再综合考虑当下的
- 思考的适合搞清楚当下的和之前的情况的关系
- Sequence DP, new dp[n + 1];

#### Rolling Array
- [i]'只和前两个位子 [i-1], [i - 2]'相关
- 用%2来标记 [i], [i - 1], [i - 2]三个位置.
- 其他滚动时惯用curr/prev来表示坐标, 这里%2虽然抽象, 但是更加实用.




---

**6. [House Robber II.java](https://github.com/awangdev/LintCode/blob/master/Java/House%20Robber%20II.java)**      Level: Medium
      

和House Robber I 类似, 搜刮房子, 相邻不能动. 特点是: 现在nums排成了圈, 首尾相连.

#### Sequence DP
- 根据dp[i-1]是否被rob来讨论dp[i]: dp[i] = Math.max(dp[i-1], dp[i - 2] + nums[i - 1]);
- 特别的是，末尾的last house 和 first house相连. 这里就需要分别讨论两种情况: 第一个房子被搜刮, 或者第一个房子没被搜刮
- be careful with edge case nums = [0], only with 1 element.

#### 两个状态
- 是否搜刮了第一个房子, 分出两个branch, 可以看做两种状态.
- 可以考虑用两个DP array; 也可以加一dp维度, 补充这个状态.
- 连个维度表示的是2种状态(1st house being robbed or not); 这两种状态是平行世界的两种状态, 互不相关.

#### Rolling array
与House Robber I一样, 可以用%2 来操作rolling array



---

**7. [Paint House II.java](https://github.com/awangdev/LintCode/blob/master/Java/Paint%20House%20II.java)**      Level: Hard
      

一排n个房子, 每个房子可涂成k种颜色, 涂每个房子的价钱不一样, 用costs[][]表示. 

costs[0][1]表示涂了index是0的房子, 用了color 1.

规则: 相邻的两个房子不能使同一种颜色

求: 最少的cost 

#### DP
- 先考虑单纯地用dp[i]表示涂前 i 个房子的最小cost
- 但是 dp[i] 和 dp[i-1] 两个index选什么颜色会互相影响, 难讨论, 于是加状态: 序列DP被加了状态变成2D. 
- 考虑最后位, 而前一位i-1又被i位的颜色限制, 于是在考虑 min dp[i] 时候, 又多了一层iteration.
- 做dp[i][j]: # cost for 前 i 个房子, 所以要先pick (i-1) 房子的cost, 然后在找出 (i-2)房子的cost
- K种颜色 => O(NK^2)
- 如果不优化, 跟Paint House I 几乎是一模一样的代码


#### 注意
- 序列型dp[i]表示'前i-1个'的结果. 所以dp最好设定为 int[n + 1] size. 
- 然而, 颜色在这里是状态, 所以保留在 j: [ 0~k)
- [[8]] 这样的edge case. 跑不进for loop, 所以特殊handle.

#### Optimization
- O(NK)
- 如果已知每次都要从cost里面选两个不同的最小cost,那么先把最小两个挑出来, 就不必有第三个for loop 找 min
- 每次在数列里面找: 除去自己之外的最小值, 利用最小值/次小值的思想
- 维持2个最值: 最小值/次小值. 
- 计算的时候, 如果除掉的不是最小值的index, 就给出最小值; 如果除掉的是最小值的index, 就给出次小值.
- Every loop: 1. calculate the two min vlaues for each i; 2. calcualte dp[i][j]
- 如何想到优化: 把表达式写出来, 然后看哪里可以优化



---

**8. [Best Time to Buy and Sell Stock I.java](https://github.com/awangdev/LintCode/blob/master/Java/Best%20Time%20to%20Buy%20and%20Sell%20Stock%20I.java)**      Level: Easy
      

给个array of stock prices, 限制能交易(买/买)一轮, 问如何找到最大profit.

#### 理解意思是关键
- 每天都就交易价格，n天只让买卖一次，那就找个最低价买进，找个最高价卖出
- 记录每天最小值Min是多少. O(n)
- 每天都算和当下的Min买卖，profit最大多少.

#### DP
- Find min value for first i items, new dp[n + 1].
- 然后用当天的price做减法算max profit.
- Time, Space: O(n)
- 更进一步, 用一个min来表示min[i], 因为计算中只需要当下的min.

#### Rolling array
- index i only depend on [i - 2]
- Space O(n)

#### Brutle Failed
- 每天都试着买进，然后之后的每一天尝试卖出. double for loop, O(n^2). timeout.
- 其中很多都是没必要的计算：[7, 1, 5, 3, 6, 4]。 if we know buyin with 1 is cheapest, we don't need to buyin at 5, 3, 6, 4 later on; we'll only sell on higher prices.



---

**9. [Best Time to Buy and Sell Stock II.java](https://github.com/awangdev/LintCode/blob/master/Java/Best%20Time%20to%20Buy%20and%20Sell%20Stock%20II.java)**      Level: Easy
      

和Stock I 的区别：可以买卖多次，求总和的最大盈利.

#### 几种其他不同的思路:
- Greedy, 每次有相邻的diff符合profit条件, 就卖了, 最后把所有的diff加在一起. 计算delta, 其实简单粗暴, 也还不错.
- 如下, 从低谷找peek, sell.
- DP. (old dp solution BuyOn[], SellOn[])
- DFS计算所有(timeout).Improvement on DFS -> DP -> calculate sellOn[i] and buyOn[i], and then return buyOn[i]. 有点难想, 但是代码简单, 也是O(n)

#### Greedy
- 画图, 因为可以无限买卖, 所以只要有上升, 就卖
- 所有卖掉的, 平移加起来, 其实就是overall best profit
- O(n)

#### 找涨幅最大的区间，买卖：
- 找到低谷，买进:peek = start + 1 时候，就是每次往前走一步;若没有上涨趋势，继续往低谷前进。
- 涨到峰顶，卖出:一旦有上涨趋势，进一个while loop，涨到底, 再加个profit.
- profit += prices[peek - 1] - prices[start]; 挺特别的。
- 当没有上涨趋势时候，peek-1也就是start, 所以这里刚好profit += 0.

#### DP
- 想知道前i天的最大profit, 那么用sequence DP
- 当天的是否能卖, 取决于昨天是否买进, 也就是昨天买了或者卖了的状态: 加状态, 2D DP
- 如果今天是卖的状态, 那么昨天: 要么买进了, 今天 +price 卖出; 要么昨天刚卖, 今天不可能再卖, profit等同.
- 如果今天是买的状态, 那么昨天: 要么卖掉了, 今天 -price 买入; 要么昨天刚卖, 今天不可能再买, profit等同.

#### Rolling Array
- [i] 和 [i - 1] 相关联, roll




---

**10. [Best Time to Buy and Sell Stock III .java](https://github.com/awangdev/LintCode/blob/master/Java/Best%20Time%20to%20Buy%20and%20Sell%20Stock%20III%20.java)**      Level: Hard
      

比stock II 多了一个限制：只有2次卖出机会.

#### DP加状态
- 只卖2次, 把买卖分割成5个状态模块.
- 在状态index 0, 2, 4: 没有持有股票. 1. 一直在此状态, max profit不变; 2. 刚卖掉, dp[i][前状态] + profit
- 在状态index 1, 3: 持有股票. 1. 一直在此状态, daily profit. 2. 刚刚买进, 状态改变, 但是没有profit yet: dp[i][前状态]

##### Partial profit
- 把每天的partial profit (diff)加在一起, 最终的overall profit是一样的. 唯一更好的是, 不需要记录中间买入的时间点.
- 什么时候会积累profit呢? 
- 1. 原本就持有股票的, 如果毫无动作, 那么状态不变, 积累profit diff. 
- 2. 卖出了股票, 状态改变, 积累profit diff.
- 注意: 只有在状态index: 0, 2, 4, 也就是卖掉股票的时候, 猜可以积累profit

##### Rolling Array
- [i] 只有和 [i-1] 打交道, reduce space
- O(1) space, O(n) time

#### 找峰头
- 找峰头；然后往下再找一个峰头。
- 怎么样在才能Optimize两次巅峰呢？从两边同时开始找Max！（棒棒的想法）
- leftProfit是从左往右，每个i点上的最大Profit。
- rightProfit是从i点开始到结尾，每个点上的最大profit.
- 那么在i点上，就是leftProfit，和右边rightProfit的分割点。在i点，leftProfit+rightProfit相加，找最大值。
- 三个O(n),还是O(n)



---

**11. [Best Time to Buy and Sell Stock IV.java](https://github.com/awangdev/LintCode/blob/master/Java/Best%20Time%20to%20Buy%20and%20Sell%20Stock%20IV.java)**      Level: Hard
      

有int[] price of stock, 最多做 k transactions.  求最大profit.

#### DP
- 根据StockIII, 不难发现StockIV就是把状态划分为2k+1份. 那么同样的代码, 移植.

##### 注意1: 
- 如果k很大, k>n/2, 那么长度为n的数组里面, 最多也只能n/2个transaction
- 那么题目简化为stockII, 给n数组, 无限次transaction.
- 注意, status的数量是 2k+1
- Time O(NK), Space O(2k+1) to store the status

##### 注意2: 
- 最后状态是'没有stock'的都该考虑, 做一个 for 循环比较max. 
- 当然, 来一个profit variable, 不断比较, 也是可以的.

#### 方法2
- (previous notes, 熟练第一种方法的思考就可以)
- 记得要理解：为什么 i-1天的卖了又买，可以和第 i 天的卖合成一次交易？    
- 因为每天交易的price是定的。所以卖了又买，等于没卖！这就是可以合并的原因。要对价格敏感啊少年。
- Inspired from here: http://liangjiabin.com/blog/2015/04/leetcode-best-time-to-buy-and-sell-stock.html

##### 局部最优解 vs. 全局最优解：     
- local[i][j] = max(global[i – 1][j – 1] + diff, local[i – 1][j] + diff)    
- global[i][j] = max(global[i – 1][j], local[i][j])     
- local[i][j]: 第i天，当天一定进行第j次交易的profit     
- global[i][j]: 第i天，总共进行了j次交易的profit.

- local[i][j]和global[i][j]的区别是：local[i][j]意味着在第i天一定有交易（卖出）发生。    
- 当第i天的价格高于第i-1天（即diff > 0）时，那么可以把这次交易（第i-1天买入第i天卖出）跟第i-1天的交易（卖出）合并为一次交易，即local[i][j]=local[i-1][j]+diff；    
- 当第i天的价格不高于第i-1天（即diff<=0）时，那么local[i][j]=global[i-1][j-1]+diff，而由于diff<=0，所以可写成local[i][j]=global[i-1][j-1]。    
- (Note:在我下面这个solution里面没有省去 +diff）   

- global[i][j]就是我们所求的前i天最多进行k次交易的最大收益，可分为两种情况：    
- 如果第i天没有交易（卖出），那么global[i][j]=global[i-1][j]；     
- 如果第i天有交易（卖出），那么global[i][j]=local[i][j]。    





---

**12. [Maximum Subarray.java](https://github.com/awangdev/LintCode/blob/master/Java/Maximum%20Subarray.java)**      Level: Easy
      

给一串数组, 找数组中间 subarray 数字之和的最大值

#### Sequence DP
- dp[i]: 前i个element, 包括element i 在内的 continous subsequence 的最大sum是多少?
- 因为continous sequence, 所以不满足条件的时候, 会断: track overall max,
- init dp[0] = 0; max = MIN_VALUE 因为有负数
- Time, space O(n)
- Rolling array, space O(1)

#### Divide and Conquer
- 找一个mid piont, 考虑3种情况: 只要左边, 只要右边, cross-mid
- left/rigth 的case, 直接 dfs
- corss-mid case: continuous sum max from left + continous sum max from right + mid
- continuous sum max from one direction:


---

**13. [Maximum Subarray II.java](https://github.com/awangdev/LintCode/blob/master/Java/Maximum%20Subarray%20II.java)**      Level: Medium
      

给一串数组, 找数组中间 两个不交互的 subarray 数字之和的最大值

#### DP
- 考虑两个方向的dp[i]: 包括i在内的subarray max sum. 
- dp[i] 的特点是: 如果上一个 dp[i - 1] + nums[i - 1] 小于 nums[i-1], 那么就舍弃之前, 从头再来:
- dp[i] = Math.max(dp[i - 1] + nums.get(i - 1), nums.get(i - 1));
- 缺点: 无法track全局max, 需要记录max.
- 因为我们现在要考虑从左边/右边来的所有max, 所以要记录maxLeft[] 和 maxRight[] 
- maxLeft[i]: 前i个元素的最大sum是多少 (不断递增); maxRight反之, 从右边向左边
- 最后比较maxLeft[i] + maxRight[i] 最大值
- Space, Time O(n)
- Rolling array, reduce some space, but can not reduce maxLeft/maxRight

#### preSum, minPreSum
- preSum是[0, i] 每个数字一次加起来的值
- 如果维持一个minPreSum, 就是记录[0, i]sum的最小值(因为有可能有负数)
- preSum - minPreSum 就是在 [0, i]里, subarray的最大sum值
- 把这个最大subarray sum 记录在array, left[] 里面
- right[] 是一样的道理
- enumerate一下元素的排列顺位, 最后 max = Math.max(max, left[i] + right[i + 1])



---




 
 
 
## Minimum Binary Tree (3)
**0. [Expression Tree Build.java](https://github.com/awangdev/LintCode/blob/master/Java/Expression%20Tree%20Build.java)**      Level: Hard
      

给一串字符, 表示的是 公式 expression. 把公式变成expression tree

#### Monotonous Stack
- 和Max-tree一样，https://leetcode.com/problems/maximum-binary-tree
- 用到bottom->top递增的stack: 最底下的root维持成最小的element.
- 这个题目是Min-tree， 头上最小，Logic 和max-tree如出一辙   
- Space: O(n) 
- Time on average: O(n).

#### 特点
- TreeNode: 用一个并不是最终结果的TreeNode, 存weight, 用来排序
- 用base weight的概念权衡同一个层面的 符号, 数字 顺序
- 每一个character都是一个节点, 都有自己的weight. 用一个TreeNode来存weight value, 利用用weight来判断: 
- 1. (while loop) 如果node.val <= stack.peek().nodeValue, 把当前stack.peek() 变成 left child. 
- 2. (if condition) 如果stack有残余, 把当前node变成 stack.peek().rightChild 




---

**1. [Expression Evaluation.java](https://github.com/awangdev/LintCode/blob/master/Java/Expression%20Evaluation.java)**      Level: Hard
      

给一个公式 expression, array of strings, 然后evaluate expression 结果.

#### DFS on Expression Tree
- 计算 expression 的值: 1. 建造 expression tree. 2. DFS计算结果
- Expression Tree: Minimum Binary Tree (https://lintcode.com/en/problem/expression-tree-build/)
- build好Min Tree以后，做PostTraversal. 
- Divde and Conquer: 先recursively找到 left和right的大小， 然后evaluate中间的符号
- Time, Space O(n), n = # expression nodes

### Note
- 1. Handle数字时，若left&&right Child全Null,那必定是我们weight最大的数字node了。   
- 2. 若有个child是null,那就return另外一个node。    
- 3. prevent Integer overflow　during operation:过程中用个Long，最后结局在cast back to int.



---

**2. [Basic Calculator.java](https://github.com/awangdev/LintCode/blob/master/Java/Basic%20Calculator.java)**      Level: Hard
      

给一个expression String, 要evaluate这个expression的值.

Expression string 里面包括 +, -, 整数, 开合括号, 还有space.

#### Expression Tree
- Expression Tree是一个 weight-based的 min-tree 
- 基于 运算符号 + 数字的 tree: 数字永远在leaf, 然后符号是tree node,  括号不出现在tree里面
- 用 monotonuous stack 来构建这个tree

##### Thinking points
- Understand Expression Tree
- Use stack to build the expression tree + understand the weight system
- Use post-order traversal to evaluate the tree
- 注意, input里面的数字不会是single digit, 所以需要一个buffer存number string
- 整个题目的做法, 可以参照 `Expression Evaluation`



---




 
 
 
## Bitwise DP (1)
**0. [Counting Bits.java](https://github.com/awangdev/LintCode/blob/master/Java/Counting%20Bits.java)**      Level: Medium
      

给一个数组, 算里面有多少bit 1. 

#### Bitwise DP
- 对于每一个数字, 其实很简单就能算出来: 每次 >>1, 然后 & 1 就可以count 1s. Time: 一个数字可以 >>1 O(logN) 次
- 现在要对[0 ~ num] 都计算, 也就是N个数字, 时间复杂度: O(nLogN).
- 用DP来优化, 查找过的number的1s count, 存下来在 dp[number]里面.
- 计算你顺序从 0 -> num, count过的数字就可以重复利用.
- Bit题目 用num的数值本身表示DP的状态.
- 这里, dp[i] 并不是和 dp[i-1]有逻辑关系; 而是dp[i] 和dp[i>>1], 从binary representation看出有直接关系.



---




 
 
 
## MiniMax (1)
**0. [Coins in a Line II.java](https://github.com/awangdev/LintCode/blob/master/Java/Coins%20in%20a%20Line%20II.java)**      Level: Medium
      

给一串coins, 用values[]表示; 每个coin有自己的value. 先手/后手博弈,
每次只能 按照从左到右的顺序, 拿1个或者2个棋子, 最后看谁拿的总值最大.

MiniMax的思考方法很神奇, 最后写出来的表达式很简单

#### DP, Game Theory 自考过程比较长
- 跟Coins in a line I 不一样: 每个coin的value不同.
- 用到MiniMax的思想, 这里其实是MaxiMin. Reference: http://www.cnblogs.com/grandyang/p/5864323.html
- Goal: 使得player拿到的coins value 最大化.
- 设定dp[i]: 从index i 到 index n的最大值. 所以dp[0]就是我们先手在[0 ~ n]的最大取值 
- 于此同时, 你的对手playerB也想最大化, 而你的选择又不得不被对手的选择所牵制.
- 用MaxiMin的思想, 我们假设一个当下的状态, 假想对手playerB会做什么反应(从对手角度, 如何让我输)
- 在劣势中(对手让我输的目标下)找到最大的coins value sum


##### 推算表达式
- Reference里面详细介绍了表达式如何推到出来, 简而言之:
- 如果我选了i, 那么对手就只能选(i+1), (i+2) 两个位置, 而我在对方掌控时的局面就是min(dp[i+2], dp[i+3])
- 如果我选了i和(i+1), 那么对手就只能选(i+2), (i+3) 两个位置, 而我在对方掌控时的局面就是min(dp[i+3], dp[i+4])
- 大家都是可选1个或者2个coins
- 目标是maximize上面两个最坏情况中的最好结果

##### 简化表达式
- 更加简化一点: 如果我是先手, dp[i]代表我的最大值.
- 取决于我拿了[i], 还是[i] + [i+1], 对手可能是dp[i + 1], 或者是dp[i+2]
- 其实dp[i] = Math.max(sum - dp[i + 1], sum - dp[i + 2]);
- 这里的sum[i] = [i ~ n] 的sum, 减去dp[i+1], 剩下就是dp[i]的值没错了

##### Initialization
- 这个做法是从最后往前推的, 注意initialize dp末尾的值.
- dp = new int[n + 1]; dp[n] = 0; // [n ~ n]啥也不选的时候, 为0.
- sum = new int[n + 1]; sum[n] = 0; // 啥也不选的时候, 自然等于0
- 然后记得initialize (n-1), (n-2)

##### 时间/空间
Time O(n)
Space O(n): dp[], sum[]



---




 
 
 
## Two Pointers (24)
**0. [Reverse Vowels of a String.java](https://github.com/awangdev/LintCode/blob/master/Java/Reverse%20Vowels%20of%20a%20String.java)**      Level: Easy
      

vowels: 元音字母. 要求reverse所有元音字母.

##### 方法1: two pointer.
- 前后两个指针, 在while loop里面跑.
- 注意 i<j, 一旦相遇, 就break.
- 找到合适的, 就做swap.
- StringBuffer可以 sb.setCharAt()记得用.
- O(n)
##### 方法2:
拿出所有vowels, 反过来放进去. O(n)



---

**1. [2 Sum II - Input array is sorted.java](https://github.com/awangdev/LintCode/blob/master/Java/2%20Sum%20II%20-%20Input%20array%20is%20sorted.java)**      Level: Medium
      

升序array, 找2SUM.

#### 方法1:
- 排序好的array. Two pointer移动start和end，核查sum.
- 注意sum用long.
- O(n) time

#### 方法2: Binary Search, 因为已经排好序了啊
- 定住一个valueA, 然后在剩下的里面 binary serach 找 (target - valueB)
- O(nLogN), 就不写了



---

**2. [2 Sum II.java](https://github.com/awangdev/LintCode/blob/master/Java/2%20Sum%20II.java)**      Level: Medium
      

与 2sum II - input array is sorted类似. 都是sort array, 然后two pointer.

LintCode的题. 注意找的是greater/bigger than target。

由于给定条件允许O(nLogn):   
   sort
   two pointer

while里面two pointer移动。每次如果num[left]+num[right] > target，那么其中所有num[left++]的加上num[right]都>target.   
也就是,num[right]不动，计算加入挪动left能有多少组，那就是: right-left这么多。 全部加到count上去。     
然后right--.换个right去和前面的left部分作比较。



---

**3. [3 Sum Closest.java](https://github.com/awangdev/LintCode/blob/master/Java/3%20Sum%20Closest.java)**      Level: Medium
      

3Sum 的一种简单形式, 并且都没有找index, value, 而只是找个sum罢了.

double for loop。 2Sum只能用土办法 left/right 2 pointers。 O(n^2)

注意：check closest时候用long, 以免int不够用



---

**4. [3 Sum.java](https://github.com/awangdev/LintCode/blob/master/Java/3%20Sum.java)**      Level: Medium
      

方法1:
sort array, for loop + two pointer. O(n)
处理duplicate wthin triplets: 
如果最外圈的移动点i重复, 一直顺到结尾的最后一个再用.
如果是triplet内有重复, 用完start point, 移动到结尾.

Previous notes:
注意:   
   1. 找 value triplets, 多个结果。注意，并非找index。    
   2. 要升序, 第一层for loop 从最后一个元素挑起, 保证了顺序。    
   3. 去掉duplicate: check用过的同样的数字，都跳掉。不需要用同样的数字再计算一边已有结果。

步骤:   
   1. For loop 挑个数字A.    
   2. 2Sum 出一堆2个数字的结果    
   3. Cross match 步骤1里面的A.   

时间 O(n^2), 两个nested loop

另外, 还是可以用HashMap来做2Sum。稍微短点。还是要注意handle duplicates.




---

**5. [3 Sum Smaller.java](https://github.com/awangdev/LintCode/blob/master/Java/3%20Sum%20Smaller.java)**      Level: Medium
      

一般的O(n3)肯定不行。在此基础上优化。
发现j,k满足条件时候，(k - j)就是所有 sum <target的情况了。
而一旦>target, 又因为j不能后退，只能k--，那么问题就被锁定了. 这样可以做到O(n2)



---

**6. [Intersection of Two Arrays II.java](https://github.com/awangdev/LintCode/blob/master/Java/Intersection%20of%20Two%20Arrays%20II.java)**      Level: Easy
      

方法1:
用HashMap: 存一个nums1, 再拿nums2 check against map. 时间/空间:O(n)

方法2:
Binary search? 需要array sorted. 否则时间O(nlogn)不值得.
[没做完, 有错]



---

**7. [Minimum Size Subarray Sum.java](https://github.com/awangdev/LintCode/blob/master/Java/Minimum%20Size%20Subarray%20Sum.java)**      Level: Medium
      

方法1:
2 pointer, O(n). 找subarray, start 或 end pointer，每次一格这样移动.

好的策略: 
1. 先找一个solution, 定住end. 
2. 然后移动start; 记录每个solution if occurs
3. 然后再移动end，往下找。

Note: 虽然一眼看上去是nested loop.但是分析后，发现其实就是按照end pointer移动的Loop。start每次移动一格。总体上，还是O(n)

方法2:
Double for loop, base i 每次只+1, 所以最后O(n^2)

方法3:
Binary Search, O(nLogN)
Not done yet



---

**8. [Longest Substring Without Repeating Characters.java](https://github.com/awangdev/LintCode/blob/master/Java/Longest%20Substring%20Without%20Repeating%20Characters.java)**      Level: Medium
      

方法1:
Two Pointers
双指针: 从start开始遍历, 但是第一步是while loop来推进end; 直到推不动end, 然后start++
巧妙点: 因为end是外围variable, 在start的loop上, end不会重置;[star ~ end] 中间不需要重复计算.
最终可以O(n);

Previous verison of two pointers:
用两个pointer, head和i.
注意：head很可能被退回到很早的地方，比如abbbbbba,当遇到第二个a，head竟然变成了 head = 0+1 = 1.      
当然这是不对的，所以head要确保一直增长，不回溯

方法2:
   HashMap<Char, Integer>: <character, last occurance index>
   一旦有重复, rest map.
   没有重复时候, 不断map.put(), 然后求max值

问题: 每次reset map之后就开始从新从一个最早的index计算, 最坏情况是O(n^2):
'abcdef....xyza'




---

**9. [Minimum Window Substring.java](https://github.com/awangdev/LintCode/blob/master/Java/Minimum%20Window%20Substring.java)**      Level: Hard
      

基本思想: 用个char[]存string的frequency. 然后2pointer, end走到底, 不断validate.
符合的就process as result candidate.

HashMap的做法比char[]写起来要复杂一点, 但是更generic



---

**10. [Linked List Cycle.java](https://github.com/awangdev/LintCode/blob/master/Java/Linked%20List%20Cycle.java)**      Level: Easy
      

O(1) sapce: 用快慢指针。一个跑.next, 一个跑.next.next。 总有一次，fast会因为cycle而追上slow。
那个时候其实slow.val = fast.val.

O(n) space: 用HashMap，一直add elements.  如果有重复，那么很显然是有Cycle


---

**11. [Remove Nth Node From End of List.java](https://github.com/awangdev/LintCode/blob/master/Java/Remove%20Nth%20Node%20From%20End%20of%20List.java)**      Level: Medium
      

O(n), one pace, no extra space
找到窗口, 然后平移, 最后pre 和 head之间 skip一个node就好.



---

**12. [Linked List Cycle II.java](https://github.com/awangdev/LintCode/blob/master/Java/Linked%20List%20Cycle%20II.java)**      Level: Medium
      

方法1:
快慢指针, O(1)space.

确认有cycle后, 其实是数学问题:
当head == slow.next时候， head就是cycle starting point.
也就是说，当slow 移动到了那个回溯点，slow.next那个点就刚好是head的那个点...

证明:
1. 假设慢指针走t步, 快指针走快一倍, 也就是2t.
2. 我们假设cycle的长度是Y, 而进入cycle之前的长度为X.
3. 假设慢指针走了m圈cycle, 而快指针走了n圈cycle之后, 两个pointer相遇.
4. 最终在Y cycle里面的K点相遇, 也就是两个指针都在这最后一圈里面走了K 步.
=> 
那么:
t = X + mY + K
2t = X + nY + K
整合公式:
X + K = (n - 2m)Y
这里的m和n不过是整数的跑圈数, 也就是说X和K加在一起, 总归是结束cycle. X 和 K 互补
=> 结论: 当slow/fast 指针在K点相遇后, 再走X步, 就到了cycle的起点, 也就是题目要求的起点.

方法2:
HashMap, O(n) space


---

**13. [Trapping Rain Water.java](https://github.com/awangdev/LintCode/blob/master/Java/Trapping%20Rain%20Water.java)**      Level: Hard
      

这道题目的方法比较多.
#### 方法1
Array, 维持一个左手最高墙array, 右手最高强array.
对于每个index而言, vertically 能存放的最大水柱, 就是靠左右最高墙决定的:
min(leftHighestWall, rightHighestWall) - currHeight.

#### 方法2
方法1上面的优化, two pointer, 还是找左边最高和右边最高. O(1) space.
利用到了方法3里面的想法一样: 整个structure是被中间的最高bar 二分天下:
左边按照maxLeft来计算, 右边按照maxRight来计算.

#### 方法3
2 Pointers， 双面夹击:
1. 找中间最高bar的index    
2. 两面往中心扫：每次加上（topBarIndex - currIndex）* (elevation from previous index).也就是每次加一个横条。    
3. 每次还要减去block自身的height

#### 方法4
主要想法和方法3一致: 在山坡下坡的基础上, 一直用stack堆积bottom. 
最后遇到上升之前, 此时bottom可以用来跟stack之前堆积的所有下坡index做比较, 算跟他们高度相差的积水.
用了stack记录下坡, 然后用个while loop一挖到底的想法非常棒.




---

**14. [Find the Duplicate Number.java](https://github.com/awangdev/LintCode/blob/master/Java/Find%20the%20Duplicate%20Number.java)**      Level: Medium
      

- 注意不要思维定式: 以为mid是index
- 这里mid其实是binary search on value [1, n] 的一个value.
- 再次用到validate() function

Time: O(nLogN)



---

**15. [Permutation in String.java](https://github.com/awangdev/LintCode/blob/master/Java/Permutation%20in%20String.java)**      Level: Medium
      

#### Two Pointer
- 如果做s1的permudation, 时间复杂度是O(n!) 肯定不可以
- 这里用HashTable的做法 (因为26字母, 所以用int[26]简化) 来记录window内的 character count
- 如果window内的character count 相等, 那么就是permudation
- 更进一步优化: 找两个map相互对应, 不如用一个 int[26]: s1对遇到的character做加法, s2对遇到的character做减法
- two pointer 运用在 n1, n2 的把控; 以及 s2.charAt(i - n1) 这一步



---

**16. [Implement strStr().java](https://github.com/awangdev/LintCode/blob/master/Java/Implement%20strStr().java)**      Level: Easy
      

给两个string A, B, 找一个 B 在 A 种的起始位置.

#### Two Pointer
- 找到B在A中的起始位置, 然后看一下从这个点开始的substring是否等于B就可以了
- 还挺多坑的, 这些可以帮助优化:
- 1. 当B是“”的时候，也就是能在A的其实位置找到B....index = 0.
- 2. edge condition: 如果 haystack.length() < needle.length() 的话, 必须错, return -1
- 3. 如果在某个index, A后面剩下的长度, 比B的长度短, 也是误解, return -1



---

**17. [Interleaving Positive and Negative Numbers.java](https://github.com/awangdev/LintCode/blob/master/Java/Interleaving%20Positive%20and%20Negative%20Numbers.java)**      Level: Medium
      

给一串数组 有正负数. 重新排列, 让数组里面 正数 和 负数 相隔开. 原来的order无所谓

#### Two pointer
- 需要知道正负的位置, 所以排序 O(nlogN)
- 考虑: 正数多还是负数多的问题, 举栗子就看出来端倪了
- 然后Two Pointer, swap 
- Time O(nlogn), space O(n)

#### extra space
- 用extra O(n) space, 把正负分成两个list
- 然后分别按照index填回去
- time O(n). space O(n)
- 但是就么有用到Two pointer了



---

**18. [Merge Sorted Array.java](https://github.com/awangdev/LintCode/blob/master/Java/Merge%20Sorted%20Array.java)**      Level: Easy
      

给两个排好序的数组, merge. 其中一个数组nums1有多余的位置

#### Basics
- A够长，那么可以从A的尾部开始加新元素。     
- 注意，从尾部，是大数字优先排末尾的.  



---

**19. [Palindrome Linked List.java](https://github.com/awangdev/LintCode/blob/master/Java/Palindrome%20Linked%20List.java)**      Level: Easy
      

#### Reverse Linked List
- Palindrome概念很简单, 但是要在Linkde List random access坐标, 是很难得: 所以需要把一半 ListNode 翻转
- reverse linked list: 遍历接开头
- 用快慢指正找到mid point
- Time O(n), 而且不需要用额外的空间(只是调换半个list的内部顺序), 所以空间O(1)

#### Previous Note
- Palindrome都是要两边回溯相等
- linkedlist不能reverse iterating， 那么就reverse the list, 从中间开花作比较。



---

**20. [Valid Palindrome.java](https://github.com/awangdev/LintCode/blob/master/Java/Valid%20Palindrome.java)**      Level: Easy
      

验证string是不是 palindrome. 只考虑 alphanumeric, 其他字符可以忽略

#### Check Palindrome
- 前后两个指针, 往中间移动, 查看是否字母重合

#### 过滤 alphanumeric
- 可以用 ASCII code 来手动过滤, 只要 '0' ~ '9', 'a' ~ 'z', 'A' - 'Z' 之间的
- 也可以用 regular expression: match 所有这些字母, 是 [a-zA-Z0-9]
- 那凡是不是这些字母的 match, 就是取反: "[^a-zA-Z0-9]". 测试: https://regex101.com/



---

**21. [Remove Duplicates from Sorted Array.java](https://github.com/awangdev/LintCode/blob/master/Java/Remove%20Duplicates%20from%20Sorted%20Array.java)**      Level: Easy
      

给一个sorted array, 把重复的去掉: 也就是把不重复的按照顺序贴上来, array末尾多余的位置无所谓.

return unique item 的长度.

#### Two Pointers
- sorted array, 重复元素都在一起
- Two pointers 其实也可以是一个 for loop pointer, 另一个 dynamic variable.
- track unique index
- skip duplicated items
- O(n)

#### 思考模式:
- Remove Duplicate from Array 不同于remove from linked list.
- LinkedList里面我们是最好不要动node.val的，直接把node去掉。
- 而array我们很难直接把node去掉，又不能用新array，那么就要：
- 把不重复的element一个个放到最前面。
- 这个思想跟merge two sorted array （其中一个后续非常长的array可以放下arr1,arr2） 类似。
- 就是找个不会事后mess up，不会去动得index,把满足条件的element 填进去。这样保证了in place.
- *反向思维*：remove duplicate, 实际上也是找unique elements, and insert into original array



---

**22. [Remove Duplicates from Sorted Array II.java](https://github.com/awangdev/LintCode/blob/master/Java/Remove%20Duplicates%20from%20Sorted%20Array%20II.java)**      Level: Medium
      

给一个sorted array, 把重复的去掉: 也就是把不重复的按照顺序贴上来, array末尾多余的位置无所谓.

最多可重复出元素的数量不超过2个. return unique item 的长度.

#### Two Pointers
- sorted array, 重复元素都在一起
- 跟 `Remove Duplicates from Sorted Array` 几乎一模一样, 只不过unique index现在可以 validate 2 位
- 其余一模一样, use index to track unique item; skip if duplicated for more than 2 times
- O(n) time, O(1) space
- 这里也可以真的用2个pointers 写while loop, 但是没有必要, 只是单纯地走一个for loop其实就足够.



---

**23. [Rotate List.java](https://github.com/awangdev/LintCode/blob/master/Java/Rotate%20List.java)**      Level: Medium
      

给一个single linked list, 右移k steps. k non-negative.

#### Linked List basics
- 记得用dummy.next来存head.
- 特殊: 这里k可能大于list总长. 写一写linked node 移动的步数, 然后 k = k % n.
- 找到newTail, newHead, 然后利用dummy, 换位子



---




 
 
 
## Basic Implementation (2)
**0. [Cosine Similarity.java](https://github.com/awangdev/LintCode/blob/master/Java/Cosine%20Similarity.java)**      Level: Easy
      

根据 Cosine Similarity 的公式, basic implementation



---

**1. [Count and Say.java](https://github.com/awangdev/LintCode/blob/master/Java/Count%20and%20Say.java)**      Level: Easy
      

介绍一种count数字的方法, 然后每一行读出上一行的结果, 一行一行推算. 问nth行是啥样?

#### Basic Implementation
- 主要是题意很难理解, 非常misleading, 等到看明白题目, 其实没有什么算法要求.
- Count duplicates and print



---




 
 
 
## Backpack DP (6)
**0. [Backpack VI.java](https://github.com/awangdev/LintCode/blob/master/Java/Backpack%20VI.java)**      Level: Medium
      

给一个数组nums, 全正数, 无重复数字; 找: # of 拼出m的方法.

nums 里的数字, 可以重复使用. 不同的order可以算作不同的拼法.

#### Backpack DP
- dp[i] 表示: # of ways to fill weight i
- 1维: dp[w]: fill weigth w 有多少种方法. 前面有多少种可能性, 就sum多少个:
- dp[w] = sum{dp[w - nums[i]]}, i = 0~n

##### 分析
- 拼背包时, 可以有重复item, 所以考虑'最后被放入的哪个unique item' 就没有意义了.
- 背包问题, 永远和weight分不开关系.
- 这里很像coin chagne: 考虑最后被放入的东西的value/weigth, 而不考虑是哪个.






---

**1. [Backpack.java](https://github.com/awangdev/LintCode/blob/master/Java/Backpack.java)**      Level: Medium
      

给i本书, 每本书有自己的重量 int[] A, 背包有自己的大小M, 看最多能放多少重量的书?

#### Backpack DP 1
- 简单直白的思考 dp[i][m]: 前i本书, 背包大小为M的时候, 最多能装多种的书?
- **注意**: 背包问题, 重量weight一定要是一维.
- dp[i][j] = Math.max(dp[i][j], dp[i - 1][j - A[i - 1]] + A[i - 1]);
- 每一步都track 最大值
- 最后return dp[n][m]
- 时间空间  O(mn)
- Rolling array, 空间O(m)

#### Backpack DP 2
- true/false求解, 稍微曲线救国: 重点是, 最后, 按照weight从大到小遍历, 第一个遇到true的, index就是最大值.  
- 考虑: 用i个item (可跳过地取), 是否能装到weight w?
- 需要从'可能性'的角度考虑, 不要搞成单一的最大值问题.
- 1. 背包可装的物品大小和总承重有关.
- 2. 不要去找dp[i]前i个物品的最大总重, 找的不是这个. 
    dp[i]及时找到可放的最大sum, 但是i+1可能有更好的值, 把dp[i+1]变得更大更合适.

##### 做法
- boolean[][] dp[i][j]表示: 有前i个item, 用他们可否组成size为j的背包? true/false.
- (反过来考虑了，不是想是否超过size j, 而是考虑是否能拼出exact size == j)
- **注意**: 虽然dp里面一直存在i的位置, 实际上考虑的是在i位置的时候, 看前i-1个item.

##### 多项式规律
- 1. picked A[i-1]: 就是A[i-1]被用过, weight j 应该减去A[i-1]. 那么dp[i][j]就取决于dp[i-1][j-A[i-1]]的结果.
- 2. did not pick A[i-1]: 那就是说, 没用过A[i-1], 那么dp[i][j]就取决于上一行d[i-1][j]
- dp[i][j] = dp[i - 1][j] || dp[i - 1][j - A[i - 1]]

##### 结尾
- 跑一遍dp 最下面一个row. 从末尾开始找, 最末尾的一个j (能让dp[i][j] == true)的, 就是最多能装的大小 :)   
- 时间，空间都是：O(mn)




---

**2. [Backpack II.java](https://github.com/awangdev/LintCode/blob/master/Java/Backpack%20II.java)**      Level: Medium
      

给i本书, 每本书有自己的重量 int[] A, 每本书有value int[] V

背包有自己的大小M, 看最多能放多少value的书?

#### Backpack DP
- 做了Backpack I, 这个就如出一辙, 只不过: dp存的不是max weight, 而是 value的最大值.
- 想法还是，选了A[i - 1] 或者没选A[i - 1]时候不同的value值.
- 时间空间O(mn)
- Rolling Array, 空间O(m)

#### Previous DP Solution
- 如果无法达到的w, 应该mark as impossible. 一种简单做法是mark as -1 in dp. 
- 如果有负数value, 就不能这样, 而是要开一个can[i][w]数组, 也就是backpack I 的原型.
- 这样做似乎要多一些代码, 好像并不是非常需要




---

**3. [Backpack V.java](https://github.com/awangdev/LintCode/blob/master/Java/Backpack%20V.java)**      Level: Medium
      

#### Backpack DP
- 与背包1不同: 这里不是check可能性(OR)或者最多能装的size是多少; 而是计算有多少种正好fill的可能性.
- dp[i][w]: 用前i本书, 正好fill到 w weight的可能性.
- 对于末尾, 还是两种情况:
- 1. i-1位置没有加bag
- 2. i-1位置加了bag
- 两种情况可以fill满w的情况加起来, 就是我们要的结果.
- 如常: dp[n + 1][w + 1]
- 重点: dp[0][0] 表示0本书装满weight=0的包, 这里我们必须 dp[0][0] = 1, 给后面的 dp function 做base
- Space, time: O(MN)
- Rolling array, 空间优化, 滚动数组. Space: O(M)

#### 降维打击, 终极优化
- 分析row(i-1)的规律, 发现所有row(i)的值, 都跟row(i-1)的左边element相关, 而右边element是没用的.
- 所以可以被override.
- Space: O(M), 真*一维啊!
- Time: O(MN)



---

**4. [Backpack III.java](https://github.com/awangdev/LintCode/blob/master/Java/Backpack%20III.java)**      Level: Hard
      

给n种不同的物品, int[] A weight, int[] V value, 每种物品可以用无限次

问最大多少value可以装进size是 m 的包?

#### DP
- 可以无限使用物品, 就失去了last i, last unique item的意义: 因为可以重复使用.
- 所以可以转换一个角度:
- 1. 用i **种** 物品, 拼出w, 并且满足题目条件(max value). 这里因为item i可以无限次使用, 所以考虑使用了多少次K.
- 2. K虽然可以无限, 但是也被 k*A[i]所限制: 最大不能超过背包大小.
- dp[i][w]: 前i种物品, fill weight w 的背包, 最大价值是多少.
- dp[i][w] = max {dp[i - 1][w - k*A[i-1]] + kV[i-1]}, k >= 0
- Time O(nmk)
- 如果k = 0 或者 1, 其实就是 Backpack II: 拿或者不拿

#### 优化
- 优化时间复杂度, 画图发现:
- 所计算的 (dp[i - 1][j - k*A[i - 1]] + k * V[i - 1]) 
- 其实跟同一行的 dp[i][j-A[i-1]] 那个格子, 就多出了 V[i-1]
- 所以没必要每次都 loop over k times
- 简化: dp[i][j] 其中一个可能就是: dp[i][j - A[i - 1]] + V[i - 1]
- Time O(mn)

#### 空间优化到1维数组
- 根据上一个优化的情况, 画出 2 rows 网格
- 发现 dp[i][j] 取决于: 1. dp[i - 1][j], 2. dp[i][j - A[i - 1]]
- 其中: dp[i - 1][j] 是上一轮 (i-1) 的结算结果, 一定是已经算好, ready to be used 的
- 然而, 当我们 i++,j++ 之后, 在之前 row = i - 1, col < j的格子, 全部不需要.
- 降维简化: 只需要留着 weigth 这个 dimension, 而i这个dimension 可以省略: 
- (i - 1) row 不过是需要用到之前算出的旧value: 每一轮, j = [0 ~ m], 那么dp[j]本身就有记录旧值的功能.
- 变成1个一位数组
- 降维优化的重点: 看双行的左右计算方向
- Time(mn). Space(m)



---

**5. [Combination Sum IV.java](https://github.com/awangdev/LintCode/blob/master/Java/Combination%20Sum%20IV.java)**      Level: Medium
      

给一串数字candidates (no duplicates), 和一个target. 

找到所有unique的 组合(combination) int[], 要求每个combination的和 = target.

注意: 同一个candidate integer, 可以用任意多次.

#### Backpack DP
- 计数问题, 可以想到DP. 其实就是Backpack VI.
- 从x个数字里面找candidate(可以重复用同一个数字), 来sum up to target. 找: # of ways to form the sequence.
- Backpack VI: 给一个数组nums, 全正数, 无重复数字; 找: # of 拼出m的方法
- dp[i]: # of ways to build up to target i
- consider last step: 如果上一步取的是 candidate A, 那么就该加到dp[i]:
- dp[i] += dp[i - A]
- 要找overall dp[i], 就做一个for loop: dp[i] = sum{dp[i - num]}, where for (num: nums)
- Time: O(mn). m = size of nums, n = target
- If we optimize dp for loop, 需要Sort nums. O(mlogm). will efficient 如果m是constant或者relatively small. Overall: O(n)

#### DFS, backtracking
- 尽管思考方式是对的, 但是 times out
- 可以重复使用数字的时候, 比如用1 来拼出 999, 这里用1就可以走999 dfs level, 不efficient



---




 
 
 
## Bit Manipulation (11)
**0. [Power of Two.java](https://github.com/awangdev/LintCode/blob/master/Java/Power%20of%20Two.java)**      Level: Easy
      

跟powerOfThree一样: 可以loop, check mod; 也可以用binary search找合适的数字.



---

**1. [Sum of Two Integers.java](https://github.com/awangdev/LintCode/blob/master/Java/Sum%20of%20Two%20Integers.java)**      Level: Easy
      

a^b 是: 不完全加法.
a&b 是: 所有可能的进位. a&b<<1是向左边进位的形态.

Goal: 先a^b裸加, 算出进位; 再把结果和进位裸加, 再算出这一轮的进位; 再..裸价, 算进位....直到进位数==0. 

那么就，首先记录好进位的数字：carry. 然后 a^b 不完全加法一次。然后b用来放剩下的carry, 每次移动一位，继续加，知道b循环为0为止。

在第一回 a ^ b 之后, b 的本身意义就消失. 接下去应该给parameter重新命名.
sum = a ^ b; // sum without adding carries
nextCarry = (a & b) << 1;

用其他variable name 取代 a, b 会更好理解一点.

Bit Operation    
Steps: 
   a & b: 每bit可能出现的进位数       
   a ^ b: 每bit在此次操作可能留下的值，XOR 操作         
   每次左移余数1位，然后存到b, 再去跟a做第一步。loop until b == 0    

(http://www.meetqun.com/thread-6580-1-1.html)



---

**2. [Swap Bits.java](https://github.com/awangdev/LintCode/blob/master/Java/Swap%20Bits.java)**      Level: Easy
      

简单, 但是很多知识点:
1. Hex 0xaaaaaaaa 是1010101....1010; 0x55555555 是01010101....0101
2. 可以用这两个hex取单数和负数. 如果需要取其他的pattern, 也可以做.
3. x很可能是negative number, 所以right-shift 要用logic shift, >>> 避免leading负数补位.



---

**3. [Update Bits.java](https://github.com/awangdev/LintCode/blob/master/Java/Update%20Bits.java)**      Level: Medium
      

熟悉bits的一些trick:
- ~0 = -1 = 111111...11111111 (32-bit)
- Create mask by shifting right >>>, and shifting left
- Reverse to get 0000...11110000 format mask
- & 0000 = clean up; | ABC = assign ABC



---

**4. [Maximum XOR of Two Numbers in an Array.java](https://github.com/awangdev/LintCode/blob/master/Java/Maximum%20XOR%20of%20Two%20Numbers%20in%20an%20Array.java)**      Level: Medium
      

比较难想到. 利用到XOR性质A^B=C, then A=B^C.
1. 枚举可能的A, 2. 然后一个个猜.

1. 枚举A: 因为求MAX肯定是找leading-1最多的数字, 那么枚举A从(1000000...000)开始, 
每次多一位取1或者0
2. 因为枚举A的时候是按照每个bit来, 那么B和C也要以同样数位出现.
这里吧B和C变成了prefix的形式, 放在了set里面. 
跟2sum用hashmap的思想类似, 每次用枚举的 A^B=C, 看看结果C是否已经在set里面. 
如果在, 证明枚举的A可能被B^C得出, 那么就找到了一种情况.

还用到一些技巧: 
mask = (1 << i); // i位mask
mask = mask | (1 << i); // prefix mask



---

**5. [Majority Element.java](https://github.com/awangdev/LintCode/blob/master/Java/Majority%20Element.java)**      Level: Easy
      

方法1: Vote 计数, vote++, vote--到最后剩下的就是winner. Time O(n), Space O(1)
Majority Number是指超半数. 超半数的数字, 最后都会至少有vote>=1: match current majority number，vote++；if not, vote--. 
注意：assume valid input, 是一定有一个majority number的。否则此法不成。[1,1,1,2,2,2,3]是个invalid input,结果是3，当然也错了。

方法2: HashMap count occurance. Time, Space: O(n)

方法3: Bit manipulation. 还没有做.

Related Problems:
Majority Number II，超1/3, 那么就分三份处理，countA, countB来计算最多出现的两个。

Majority Number III, 超1/k, 那么自然分k份。这里用到 HashMap。



---

**6. [Convert Integer A to Integer B.java](https://github.com/awangdev/LintCode/blob/master/Java/Convert%20Integer%20A%20to%20Integer%20B.java)**      Level: Easy
      

把Integer A 转换成 Integer B 需要改变多少bits?

#### Bit Manipulation
- a^b 显示出bit format里面有不同binary code的数位.
- 每次 (a^b)>>i 移动i位之后, 再 & 1时其实是指留下这一位的数字.
- count 
- 其实用到了 ^ 找不同的bit, >> 移位, &1 mask



---

**7. [Count 1 in Binary.java](https://github.com/awangdev/LintCode/blob/master/Java/Count%201%20in%20Binary.java)**      Level: Easy
      

count 一个 32-bit number binary format 里面有多少1

#### Bit Manipulation
- shift >> i 
- apply mask & 1

#### Convert to string O(n) space
可以把integer -> string -> char array.



---

**8. [Counting Bits.java](https://github.com/awangdev/LintCode/blob/master/Java/Counting%20Bits.java)**      Level: Medium
      

给一个数组, 算里面有多少bit 1. 

#### Bitwise DP
- 对于每一个数字, 其实很简单就能算出来: 每次 >>1, 然后 & 1 就可以count 1s. Time: 一个数字可以 >>1 O(logN) 次
- 现在要对[0 ~ num] 都计算, 也就是N个数字, 时间复杂度: O(nLogN).
- 用DP来优化, 查找过的number的1s count, 存下来在 dp[number]里面.
- 计算你顺序从 0 -> num, count过的数字就可以重复利用.
- Bit题目 用num的数值本身表示DP的状态.
- 这里, dp[i] 并不是和 dp[i-1]有逻辑关系; 而是dp[i] 和dp[i>>1], 从binary representation看出有直接关系.



---

**9. [Missing Number.java](https://github.com/awangdev/LintCode/blob/master/Java/Missing%20Number.java)**      Level: Easy
      

给一串unique数字, 数字取自 [0 ~ n], 无序, 找第一个skipped的数字.

#### Swap 
- 跟First Missing Positive 非常像, 只有一行代码的区别.
- swap 所有的数字, 到自己的correct position
- 最后一个for loop找到错位的index, 也就是缺的数字.

#### Bit Manipulation
- XOR will only retain bits that are different 1 ^ 0 = 1, but 0^0, 1^1 == 0
- Use that feature, 把所有value都和index XOR了
- 剩下的多余的数字, 其实是那个index无法被XOR消掉, 也就是那个缺的number value.
- 注意: 题目告诉数字是 [0 ~ n], 然而缺一个数字, 那么在[0 ~ n - 1] 里面, 最大的数字(不管缺没缺), 一定是 n = nums.length.

#### HastSet
- 全存, 找missing
- O(n) space, 不合题意

#### sorting
- sort, 找1st missing
- O(n log n) 太慢, 不合题意



---

**10. [Subset.java](https://github.com/awangdev/LintCode/blob/master/Java/Subset.java)**      Level: Medium
      

给一串unique integers, 找到所有可能的subset. result里面不能有重复.

#### DFS
- dfs的两种路子: 1. pick&&skip dfs, 2. for loop dfs
- 1. pick&&skip dfs: 取或者不取 + backtracking. 当level/index到底，return 一个list.
- 2. for loop dfs: for loop + backtracking. 记得：做subset的时候, 每个dfs recursive call是一种独特可能，先加进rst。
- Time&&space: subset means independent choice of either pick&&not pick. You pick n times: O(2^n), 3ms

#### Bit Manipulation
- n = nums.length, 那么在每一个index, 都是 pick / not pick: 0/1
- 考虑subset index 0/1的bit map: range 的就是 [0000...00 ~ 2^n-1]
- 每一个bitmap就能展现出一个subset的内容: all the 1 represents picked indexes
- 做法:
- 1. 找出Range
- 2. 遍历每一个bitmap candidate
- 3. 对每一个integer 的 bit representation 遍历, 如果是1, add to list
- time: O(2^n * 2^n) = O(4^n), still 3ms, fast.

#### Iterative, BFS
- Regular BFS, 注意考虑如果让one level to generate next level
- 1. 用queue来存每一次的candidate indexes
- 2. 每一次打开一层candiates, add them all to result
- 3. 并且用每一轮的candidates, populate next level, back into queue.
- should be same O(2^n), but actual run time 7ms, slower





---




 
 
 
## Quick Select (1)
**0. [Median.java](https://github.com/awangdev/LintCode/blob/master/Java/Median.java)**      Level: Easy
      

给一串无序数组, 找到median(sort之后 位置在中间的数字).

#### Quick Select
- 与quickSort不同在于, 每次只要在一半list里面recurring, 所以把O(logn)的时间复杂度降到O(n)
- quickSelect 可以找到 kth 最小的元素
- 利用这个原理, 找这个kth最小值, 然后如果 == target index, 就找到了我们的median
- quick select 的template要熟悉一下, 一下子可能想得到, 但写不出来
- 主要步骤: partition, dfs, only recur on one part of the array 



---




 
 
 
## Divide and Conquer (12)
**0. [Majority Element.java](https://github.com/awangdev/LintCode/blob/master/Java/Majority%20Element.java)**      Level: Easy
      

方法1: Vote 计数, vote++, vote--到最后剩下的就是winner. Time O(n), Space O(1)
Majority Number是指超半数. 超半数的数字, 最后都会至少有vote>=1: match current majority number，vote++；if not, vote--. 
注意：assume valid input, 是一定有一个majority number的。否则此法不成。[1,1,1,2,2,2,3]是个invalid input,结果是3，当然也错了。

方法2: HashMap count occurance. Time, Space: O(n)

方法3: Bit manipulation. 还没有做.

Related Problems:
Majority Number II，超1/3, 那么就分三份处理，countA, countB来计算最多出现的两个。

Majority Number III, 超1/k, 那么自然分k份。这里用到 HashMap。



---

**1. [Convert Sorted Array to Binary Search Tree.java](https://github.com/awangdev/LintCode/blob/master/Java/Convert%20Sorted%20Array%20to%20Binary%20Search%20Tree.java)**      Level: Easy
      

如题

#### DFS
- Binary Search Tree特点: 左边的node都比右边的node小. 
- 如果要height相差<1, 必须左右sub tree均分. 做DFS(num, start, end)
- 在每一个level, 找到中间点, 然后分割2办, 继续dfs
- Divide and Conquer



---

**2. [Construct Binary Tree from Inorder and Preorder Traversal.java](https://github.com/awangdev/LintCode/blob/master/Java/Construct%20Binary%20Tree%20from%20Inorder%20and%20Preorder%20Traversal.java)**      Level: Medium
      

如题

#### DFS
- 和Construct from Inorder && Postorder 想法一样。
- 写出Preorder和Inorder的字母例子，发现Preorder的开头总是这Level的root。依此写helper,注意处理index。
- 跟Convert Sorted Array to Binary Tree类似, 找到对应的index, 然后:
- node.left = dfs(...), node.right = dfs(...)
- Divide and Conquer



---

**3. [Validate Binary Search Tree.java](https://github.com/awangdev/LintCode/blob/master/Java/Validate%20Binary%20Search%20Tree.java)**      Level: Medium
      

如题, 验证是否是BST.

#### DFS
- 查看每个parent-child关系: leftchild < root < rightChild
- 方法: 把root.val 传下来作为 max 或者 min, 然后检查children

##### Note: 
- min/max需要时long type. 
- 如果题目真的给node.val = Integer.MAX_VALUE, 我们需要能够与之比较, long就可以.



---

**4. [Convert Sorted List to Binary Search Tree.java](https://github.com/awangdev/LintCode/blob/master/Java/Convert%20Sorted%20List%20to%20Binary%20Search%20Tree.java)**      Level: Medium
      

如题, 把一个sorted singly linked list 转换成一个 height balanced BST

#### DFS
- Divide and Conquer   
- 找到mid node
- 然后分割两半, 分别dfs做各自两个subtree: node.left,node.right
- 用长度来定位mid, 每次找中间点做root, 然后前半段, 后半段分别dfs with length.
- 用快慢pointer 找到mid. Better: 不用traverse entire linked list

#### Details
- slowPointer = node;
- fastPointer = node.next;
- 然后把root = mid.next     
- 然后开始sortedListToBST(mid.next.next); //后半段    
- mid.next = null;//非常重要，要把后面拍过序的断掉    
- sortedListToBST(head); //从头开始的前半段     
- 最后root.left, root.right merge一下。   



---

**5. [Expression Expand.java](https://github.com/awangdev/LintCode/blob/master/Java/Expression%20Expand.java)**      Level: Medium
      

给一个expression string. 里面包括数字, 字母, 括号. 其中数字代表括号里面的内容重复几次.

括号里面可以是String, 也可能是expression.

目的: 把expression展开成一个正常的String.

#### DFS
- 与Stack时需要考虑的一些function类似. 特别之处: **检查[ ]的结尾**
- 因为DFS时候, 括号里的substring会被保留着进入下一个level, 所以我们在base level要keep track of substring.
- 用int paren 来track 括号的开合, 当paren再次==0的时候 找到closure ']'

#### Stack
- Stack存 [ ] 里面的内容, detect 括号开头结尾: 结尾时process inner string
- 有很多需要注意的细节才能做对:
- Stack<Object> 也可以用, 每个地方要注意 cast. 存进去的需要是Object: String, Integer
- 几个 type check: instanceof String, Character.isDigit(x), Integer.valueOf(int num)
- 出结果时候, 不能轻易 sb.reverse().toString(): sb.reverse() 翻转了整个连在一起的string, 错.
- 用另一个Stack<String>作为buffer, 先把stack里面的内容倒出来 (pure), 但是每个item里面顺序不变.
- 最后再从buffer里面倒进StringBuffer.




---

**6. [Find Peak Element II.java](https://github.com/awangdev/LintCode/blob/master/Java/Find%20Peak%20Element%20II.java)**      Level: Hard
      

2Dmatrix, 里面的value有一些递增, 递减的特点(细节比较长, 看原题). 目标是找到peak element

#### DFS

##### 基本原理
- 我们不可能一口气准确定位(x,y), 但是我们可以再一个row/col里面, 找到1D array的 peak.
- 根据这个点, 再往剩下两个方向移动
- 1. 在中间的一行i=midX, 找到peak所在的y.
- 2. 在中间的一列j=midY, 找到peak所在的x. (有可能强势override之前找到的y, 也就是放弃那一行的peak, 在midY上找peak)
- 3. 根据 (x,y) 的4个neighbor check (x,y)是不是 peak, 如果不是, 像更高的位置移动一格
- 4. 根据之前算的 midX, midY 把board分成4个象限, 在每一份里面再继续找
- 这个题目LintCode不给做了, 所以思路对的, 但是解答还没有再次验证.

##### 剪枝/切分象限
- 每次只是找到一个row/col里面的peak而已!
- 找到这个点, 就等于把board切成了两半.
- 然后, 再跟剩下的相邻的两个位置比较, 就知道了哪里更大, 就去哪里找peak, 也就是又切了第二刀.
- 切第二刀的时候, 也要把(x, y) 移到需要取的象限. 进行DFS
- 根据mid row 切割: 
- http://www.jiuzhang.com/solution/find-peak-element-ii/#tag-highlight-lang-java
- http://courses.csail.mit.edu/6.006/spring11/lectures/lec02.pdf

##### 时间复杂度
- 每一个level都减一半
- T(n) = n + T(n/2) = n + n/2 + n/4 + ... + 1 = n(1 + 1/2 + .... + 1/n) = 2n = O(n)

#### Binary Search
- TODO
- O(nLogN)



---

**7. [Building Outline.java](https://github.com/awangdev/LintCode/blob/master/Java/Building%20Outline.java)**      Level: Review
      

又叫做skyline. 用Sweep Line做的O(nLogN), 但是貌似还有很多做法: segement tree, hashheap, treeSet?

#### 方法1: Sweep Line, Time O(nLogN), Space O(n)
original reference http://codechen.blogspot.com/2015/06/leetcode-skyline-problem.html?_sm_au_=isVmHvFmFs40TWRt

sweep line:
- 把所有点分出来， 每个点有index x, 再加上一个height.         
- 在这个list上排序，根据index和height. 注意用负数标记building start point height, 这样保证start在end 之前
- 用负数的height标记start: 在priority queue里面同一个x-pos比较 startPoint.height, endPoint.height 的时候, 因为end height是整数, 所以compare时会自动把start point放在end point前面
- 当然了, 如果两个 start point比较, 第二个point的负数超大的话(也就是height很高), 就会顺理compare return正数, 成章形成倒位
- 在processs时候用max-heap (reversed priorityqueue)，再iterate heightPoints 来存最大的height . 遇到peek,就是一个合理的解    
- heightQueue里面加一个0, 用来在结尾的时候做closure

#### 方法2: Segment Tree
REVIEW

Binary Indexed Tree?

HashHeap?



---

**8. [Burst Balloons.java](https://github.com/awangdev/LintCode/blob/master/Java/Burst%20Balloons.java)**      Level: Hard
      

一排球, 每个球有value, 每次扎破一个, 就会积分: 左*中间*右 的值. 求, 怎么扎, 最大值?

TODO: Need more thoughts on why using dp[n + 2][n + 2] for memoization, but dp[n][n] for interval DP.

#### Interval DP
- 因为数组规律会变, 所以很难找'第一个burst的球'. 反之, 想哪一个是最后burst?
- 最后burst的那个变成一堵墙: 分开两边, 分开考虑, 加法原理; 最后再把中间的加上.
- dp[i][j] represent max value on range [i, j)
- Need to calculate dp[i][j] incrementally, starting from range size == 3 ---> n
- Use k to divide the range [i, j) and conquer each side.

##### Interval DP 三把斧:
- 中间劈开
- 砍断首或尾
- Range区间作为iteration的根本

##### Print the calculation process
- use pi[i][j] and print recursively.
- Print k, using pi[i][j]: max value taken at k

#### Memoization
- 其实会做之后挺好想的一个DP
- dp[i][j] =  balloons i~j 之间的 max. 
- 然后找哪个点开始burst? 设为x。
- For loop 所有的点作为x， 去burst。
- 每次burst都切成了三份：左边可以recusive 求左边剩下的部分的最大值 + 中间3项相乘 + 右边递归下去求最大值。
- Note: 这个是Memoization, 而不纯是DP
- 因为recursive了，其实还是搜索，但是memorize了求过的值，节省了Processing




---

**9. [Maximum Subarray.java](https://github.com/awangdev/LintCode/blob/master/Java/Maximum%20Subarray.java)**      Level: Easy
      

给一串数组, 找数组中间 subarray 数字之和的最大值

#### Sequence DP
- dp[i]: 前i个element, 包括element i 在内的 continous subsequence 的最大sum是多少?
- 因为continous sequence, 所以不满足条件的时候, 会断: track overall max,
- init dp[0] = 0; max = MIN_VALUE 因为有负数
- Time, space O(n)
- Rolling array, space O(1)

#### Divide and Conquer
- 找一个mid piont, 考虑3种情况: 只要左边, 只要右边, cross-mid
- left/rigth 的case, 直接 dfs
- corss-mid case: continuous sum max from left + continous sum max from right + mid
- continuous sum max from one direction:


---

**10. [Binary Tree Longest Consecutive Sequence II.java](https://github.com/awangdev/LintCode/blob/master/Java/Binary%20Tree%20Longest%20Consecutive%20Sequence%20II.java)**      Level: Medium
      

找到binary tree 里的最长 consecutive sequence. Sequence可以递增递减, Sequence顺序可以回溯parent.

#### DFS
- Similar to Binary Tree Longest Consecutive Sequence I
- 只不过可以递增递减, 还有连接上parent的方向.
- 对于任何一个节点, 都可能: 
- 1. 自己跟两个child链接, 成为一个sequence
- 2. 左边孩子, 右边孩子各自是一个consecutive sequence, 但是不跟root相连
- main function 一开始就divide成这三份, 然后dfs
- dfs take diff == 1, diff == -1, 来做递增递减的校对.
- dfs rules:
- 1. if node == null, leaf depth = 0
- 2. if not consecutive, reset the depth = 0 (same for both left child, and right child)
- 3. compare the leftDepth && rightDepth to find the maximum
- 4. diff is the same in the same dfs loop to maintain consistant increase/decrease

##### 注意
- dfs的结果很可能是0, 如果没有任何结果, 那么上一层的caller depth = dfs() + 1 = 1
- 那么回归到root, dfs的结果很可能就是1.
- 可能会问: 那么在tree里面的partial sequence (不连接到root)的被忽略了?
- 这里 `longestConsecutive(root.left)` 就很重要了
- 这一步特地忽略掉了root, 然后走下去一层: 因为是recursive, 所以还会继续divde && conquer
- 最后, 任何一层的孩子都会被照顾到.



---

**11. [Binary Tree Longest Consecutive Sequence.java](https://github.com/awangdev/LintCode/blob/master/Java/Binary%20Tree%20Longest%20Consecutive%20Sequence.java)**      Level: Medium
      

找到binary tree 里的最长 consecutive sequence.

#### DFS
- Divide and Conquer. dfs
- 分开 看左边/右边
- 如果左边满足连续递增的规则, dfs (depth + 1), 如果不满足规则, dfs(depth = 1)
- 右边也是一样
- 对结果跟max作比较, return



---




 
 
 
## Status DP (1)
**0. [House Robber III.java](https://github.com/awangdev/LintCode/blob/master/Java/House%20Robber%20III.java)**      Level: Medium
      

Houses被arrange成了binary tree, 规则还是一样, 连续相连的房子不能同时抄.

求Binary Tree neighbor max 能抄多少.

#### DFS
- 判断当下的node是否被采用，用一个boolean来表示. 
- 如果curr node被采用，那么下面的child一定不能被采用.
- 如果curr node不被采用，那么下面的children有可能被采用，但也可能略过，所以这里用Math.max() 比较一下两种可能有的dfs结果。
- dfs重复计算:每个root都有4种dive in的可能性, 假设level高度是h, 那么时间O(4^(h)), where h = logN, 也就是O(n^2)

#### DP, DFS
- 并不是单纯的DP, 是在发现DFS很费劲后, 想能不能代替一些重复计算?
- 基本思想是dfs解法一致: 取root找最大值, 或者不取root找最大值
- 在root上DFS, 不在dfs进入前分叉; 每一个level按照状态来存相应的值: dp[0] root not picked, dp[1] root picked.
- Optimization: DP里面, 一口气找leftDP[]会dfs到最底层, 然后自下向上做计算
- 这个过程里面, 因为没有在外面给dfs()分叉, 计算就不会重叠, 再也不用回去visit most-left-leaf了, 算过一遍就完事.
- 然而, 普通没有dp的dfs, 在算完visited的情况下的dfs, 还要重新dfs一遍!visited的情况.
- Space O(h), time O(n), 或者说是O(2^h), where h = log(n)

#### DP 特点
- 不为状态而分叉dfs
- 把不同状态model成dp
- 每一个dfs都return一个based on status的 dp array.
- 等于一次性dfs计算到底, 然后back track, 计算顶部的每一层.
- DP 并不一定要是以n为base的. 也可以是局部的去memorize状态->value.



---




 
 
 
## Topological Sort (4)
**0. [Longest Increasing Path in a Matrix.java](https://github.com/awangdev/LintCode/blob/master/Java/Longest%20Increasing%20Path%20in%20a%20Matrix.java)**      Level: Hard
      

m x n 的matrix, 找最长增序的序列长度. 这里默认连续的序列.

- 接成圈是不行的, 所以visit过得 (x,y)就不能再去了.
- 斜角方向不能走, 只能走上下左右
- 无法按照坐标DP来做, 因为计算顺序4个方向都可以走.
- 最终要visit所有node, 所以用DFS搜索比较合适.

#### DFS, Memoization
- DFS太多重复计算; memoization (dp[][], visited[][]) 省去了重复计算
- initialize dp[x][y] = 1, (x,y) 自己也算path里的一格
- dfs(matrix, x, y): 每次检查(x,y)的4个neighbor (nx, ny), 如果他们到(x,y)是递增, 那么就考虑和比较:
- Maht.max(dp[x][y], dp[nx][ny] + 1); where dp[n][ny] = dfs(matrix, nx, ny)
- top level: O(mn), 尝试从每一个 (x,y) 出发
- O(m * n * k), where k is the longest path

#### Topological sort
还没有做



---

**1. [Course Schedule.java](https://github.com/awangdev/LintCode/blob/master/Java/Course%20Schedule.java)**      Level: Medium
      

- 一堆课用int[2] pair 来表示. [1, 0] 表示要上课1的话, 必须先把课0上了. 
- 每一个数字都是一个ndoe, 题目问是否能把所有的课排了
- input是 numOfCourses, 还有这个prerequisites [[]]

#### Topological Sort
- 给一个graph of nodes
- 至关重要: 用`List[] edges; edges[i] = new ArrayList<>();` 来表示graph: 就是每个node, to all its neighbors
- 目标是根据edge 的 direction, 把这个graph 里面的 node sort 一个list
- 如果有cycle, 这个item就不会被放在最后的list 里面. 
- 比如: 如果两个课互相是dependency, 就变成了cyclic dependency, 这样不好.


#### BFS
- Kahn algorithem:
- 先build一个graph map: <node, list of nodes >; or `List[] edges; edges[i] = new ArrayList<>();`
- count in-degree: inDegree就是每个node上面, 有多少个走进来的edge?
- 那些没有 in-coming-edge的, indegree 其实就 等于 0, 那么他们就应该在final result list里面
- 对这些 indegree == 0 的 nodes BFS, add to queue.
- 模拟visit每个ndoe, 如果visit过了, 这个node上的 indegree--, 然后如果最终 indegree == 0, 这个node就成功进入final list.

##### Indegree 原理
- Note: 如果有cycle, indegree是不会变成0的, 它也无法进入最终list. 
- indegree是周围的node到我这里的次数count. 
- 如果周围所有node的连线, 都意义切除后, 我的indegree还不等于0, 那么肯定有某些node间接地有重复连线, 也就是有cycle

#### DFS
- 这道题没有要求作出final list, 相对简单, 只要visit每个nodes, 最后确认没有cycle就好了
- 用 visited int[] 来确认是否有cycle. 1 代表 paretNode visited, -1 代表在DFS上一行的标记
- 如果遇到-1, 说明这个node在上一级或者以上的同一个dfs path里面已经走过, 那么证明有cycle, return false.
- 走完一个node的所有neighbor, 都没有fail, 那么backtracking, set visited[i] = 1
- 真的topo sort会在DFS的底端, 把record放进一个stack, 最后reverse, 就是真的sort order.

#### Notes:
- 还有 List[] arrayOfList = new ArrayList[]; 这样的操作啊, 代替了map<integer, integerList>

#### Previous notes
有点绕，但是做过一次就明白一点。    
是topological sort的题目。一般都是给有dependency的东西排序。    

最终都会到一个sink node， 再不会有向后的dependency, 在那个点截止。    
我就已这样子的点为map的key, 然后value是以这个node为prerequisite的 list of courses.    

画个图的话，prerequisite都是指向那个sink node， 然后我们在组成map的时候，都是从sink node 发散回来到dependent nodes.    

在DFS里面，我们是反向的， 然后，最先完全visited的那个node, 肯定是最左边的node了，它被mark的seq也是最高的。    

而我们的sink node，当它所有的支线都visit完了，seq肯定都已经减到最小了，也就是0，它就是第一个被visit的。   


最终结果：
每个有pre-requisit的node都trace上去（自底向上），并且都没有发现cycle.也就说明schedule可以用了。



---

**2. [Course Schedule II.java](https://github.com/awangdev/LintCode/blob/master/Java/Course%20Schedule%20II.java)**      Level: Medium
      

- 一堆课用int[2] pair 来表示. [1, 0] 表示要上课1的话, 必须先把课0上了. 
- 每一个数字都是一个ndoe, 题目求这个最后排好的课的list
- 如果排不好, 就给个空就好
- input是 numOfCourses, 还有这个prerequisites [[]]
- 做法跟Course Schedule I 非常像, 可以参考.

#### Topological Sort, Indegree, BFS
- 用`List[] edges; edges[i] = new ArrayList<>();` 来表示graph: 就是每个node, to all its neighbors
- 每个没有 inDegree==0 node, 都是可以加进 final list里面的. 比如一开始找到的那些 inDegree = 0的 node
- 注意, 如果 prerequisites = [], 那么就是说这些课都independent, 开个int[0 ~ n-1]的数组并赋值就好.
- 如果有cycle, 严格意义上就做不了topological sort, 也无法涵盖所有nodes,  那么return [ ]

#### DFS
- 根据 Course Schedule 里面的DFS 修改
- 维持visited int[]全局变量
- 维持sortedList int[] 全局变量, 注意加进去的时候是 add(0, node) 加在开头这样
- 每次到一个node的children全部DFS走完之后, 就可以把他加进final list里面
- 如果有cycle, 也就是dfs return false的时候, 这个题目判定排课失败, return new int[] { }



---

**3. [Alien Dictionary.java](https://github.com/awangdev/LintCode/blob/master/Java/Alien%20Dictionary.java)**      Level: Hard
      

给一个 array of strings: 假如这个array是按照一个新的字母排序表(alien dictionary)排出来的, 需要找到这个字母排序.

有可能有多重排序的方法, 给出一种就可以.

#### Graph
- 本质: 上下两行string, 相对应的相同的index上, 如果字母不同, 就说明排在第一行的字母在字母表里更领先
- 把 string array 变成topological sort的 graph: `map<char, list<char>>`
- 也可以`List[26] edges` (Course Schedule problem)
- Build edges: find char diff between two row, and store the order indication into graph
- 注意: indegree 永远是反向的 (跟 node to neighbors 相反的方式建立)

#### BFS
- topological sort 本身很好写, 但是要在题目中先了解到字母排序的本质
- 其实上面这个排序的本质很好想, 但是把它具体化成构建graph的代码, 会稍微有点难想到
- 算indegree, 然后用 BFS 来找到那些 inDegree == 0的 node
- 最先inDegree == 0的node, 就排在字母表前面.
- 下面的解法, 用了Graph: map<Character, List<Character>>, 而不是 List[26], 其实更加试用超过26个字母的dictionary.

#### DFS
- 跟BFS建立 grpah 的过程一模一样
- DFS的不同在于: 用visited map 来标记走过的地方
- 走到leaf的时候, add to result: 但因为走到了底才add, 最终的顺序应该颠倒 (或者, sb.insert(0, x) 直接用颠倒的顺序add)



---




 
 
 
## Quick Sort (1)
**0. [Median.java](https://github.com/awangdev/LintCode/blob/master/Java/Median.java)**      Level: Easy
      

给一串无序数组, 找到median(sort之后 位置在中间的数字).

#### Quick Select
- 与quickSort不同在于, 每次只要在一半list里面recurring, 所以把O(logn)的时间复杂度降到O(n)
- quickSelect 可以找到 kth 最小的元素
- 利用这个原理, 找这个kth最小值, 然后如果 == target index, 就找到了我们的median
- quick select 的template要熟悉一下, 一下子可能想得到, 但写不出来
- 主要步骤: partition, dfs, only recur on one part of the array 



---




 
 
 
## Greedy (9)
**0. [Queue Reconstruction by Height.java](https://github.com/awangdev/LintCode/blob/master/Java/Queue%20Reconstruction%20by%20Height.java)**      Level: Medium
      

别无他法, 只能写一遍例子, 找规律,然后greedy. 
需要写一遍发现的规律比如: 从h大的开始排列, 先放入k小的. 写comparator的时候要注意正确性.
如果要sort, 并且灵活insert:用arrayList. 自己做一个object.
最后做那个'matchCount'的地方要思路清晰, 找到最正确的spot, 然后greedy insert.

O(n) space, O(nLog(n)) time, because of sorting.

可能有简化的余地, 代码有点太长.
比如试一试不用额外空间?



---

**1. [Wildcard Matching.java](https://github.com/awangdev/LintCode/blob/master/Java/Wildcard%20Matching.java)**      Level: Hard
      

Double sequence DP. 与regular expression 很像.

注意1: 分析字符 ?, * 所代表的真正意义, 然后写出表达式.
注意2: 搞清楚initialization 的时候 dp[i][0] 应该always false.当p为empty string, 无论如何都match不了 (除非s="" as well)
    同时 dp[0][j]不一定是false. 比如s="",p="*" 就是一个matching.



---

**2. [Meeting Rooms II.java](https://github.com/awangdev/LintCode/blob/master/Java/Meeting%20Rooms%20II.java)**      Level: Medium
      

给一串数字pair, 代表会议的开始/结束时间. 找同时又多少个会议发生(需要多少件房间)

#### 方法1
- PriorityQueue + 一个Class来解决.Ｏ(nlogn)
- 跟 Number of Airpline in the sky是同一道题

#### 方法2: 尝试了一下用一个sorted Array + HashMap
也还行，但是handle edge的时候,HashMap 要小心，因为相同时间start和end的map key 就会重复了。



---

**3. [Coins in a Line.java](https://github.com/awangdev/LintCode/blob/master/Java/Coins%20in%20a%20Line.java)**      Level: Medium
      

拿棋子游戏, 每个人可以拿1个或者2个, 拿走最后一个子儿的输. 问: 根据给的棋子输, 是否能确定先手的输赢?

Game Theory: 如果我要赢, 后手得到的局面一定要'有输的可能'.

#### DP, Game Theory
- 要赢, 必须保证对手拿到棋盘时, 在所有他可走的情况中, '有可能败', 那就足够.
- 设计dp[i]:表示我面对i个coins的局面时是否能赢, 取决于我拿掉1个,或者2个时, 对手是不是会可能输?
- dp[i] = !dp[i - 1] || !dp[i-2]
- 时间: O(n), 空间O(n)
- 博弈问题, 常从'我的第一步'角度分析, 因为此时局面最简单.

#### Rolling Array
空间优化O(1). Rolling array, %2



---

**4. [Jump Game.java](https://github.com/awangdev/LintCode/blob/master/Java/Jump%20Game.java)**      Level: Medium
      

给出步数，看能不能jump to end.

#### DP
- DP[i]: 在i点记录，i点之前的步数是否可以走到i点？ True of false.
- 其实j in [0~i)中间只需要一个能到达i 就好了
- Function: DP[i] = DP[j] && (A[j] >= i - j), for all j in [0 ~ i)
- Return: DP[dp.length - 1];
- It timesout, O(n^2)

#### Greedy
- Keep track of farest can go
- 一旦 farest >= nums.length - 1, 也就是到了头, 就可以停止, return true.
- 一旦 farest <= i, 也就是说, 在i点上, 已经走过了步数, 不能再往前跳, 于是 return false



---

**5. [Best Time to Buy and Sell Stock II.java](https://github.com/awangdev/LintCode/blob/master/Java/Best%20Time%20to%20Buy%20and%20Sell%20Stock%20II.java)**      Level: Easy
      

和Stock I 的区别：可以买卖多次，求总和的最大盈利.

#### 几种其他不同的思路:
- Greedy, 每次有相邻的diff符合profit条件, 就卖了, 最后把所有的diff加在一起. 计算delta, 其实简单粗暴, 也还不错.
- 如下, 从低谷找peek, sell.
- DP. (old dp solution BuyOn[], SellOn[])
- DFS计算所有(timeout).Improvement on DFS -> DP -> calculate sellOn[i] and buyOn[i], and then return buyOn[i]. 有点难想, 但是代码简单, 也是O(n)

#### Greedy
- 画图, 因为可以无限买卖, 所以只要有上升, 就卖
- 所有卖掉的, 平移加起来, 其实就是overall best profit
- O(n)

#### 找涨幅最大的区间，买卖：
- 找到低谷，买进:peek = start + 1 时候，就是每次往前走一步;若没有上涨趋势，继续往低谷前进。
- 涨到峰顶，卖出:一旦有上涨趋势，进一个while loop，涨到底, 再加个profit.
- profit += prices[peek - 1] - prices[start]; 挺特别的。
- 当没有上涨趋势时候，peek-1也就是start, 所以这里刚好profit += 0.

#### DP
- 想知道前i天的最大profit, 那么用sequence DP
- 当天的是否能卖, 取决于昨天是否买进, 也就是昨天买了或者卖了的状态: 加状态, 2D DP
- 如果今天是卖的状态, 那么昨天: 要么买进了, 今天 +price 卖出; 要么昨天刚卖, 今天不可能再卖, profit等同.
- 如果今天是买的状态, 那么昨天: 要么卖掉了, 今天 -price 买入; 要么昨天刚卖, 今天不可能再买, profit等同.

#### Rolling Array
- [i] 和 [i - 1] 相关联, roll




---

**6. [Jump Game II.java](https://github.com/awangdev/LintCode/blob/master/Java/Jump%20Game%20II.java)**      Level: Hard
      

给一串数字 是可以跳的距离. goal: 跳到最后的index 所可能用的最少次数.

#### DP 
- DP[i]: 在i点记录，走到i点上的最少jump次数
- dp[i] = Math.min(dp[i], dp[j] + 1);
- condition (j + nums[j] >= i)
- 注意使用 dp[i] = Integer.MAX_VALUE做起始值, 来找min

#### Previous Notes
- Greedy, 图解 http://www.cnblogs.com/lichen782/p/leetcode_Jump_Game_II.html
- 维护一个range, 是最远我们能走的. 
- index/i 是一步一步往前, 每次当 i <= range, 做一个while loop， 在其中找最远能到的地方 maxRange
- 然后更新 range = maxRange
- 其中step也是跟index是一样, 一步一步走.
- 最后check的condition是，我们最远你能走的range >= nums.length - 1, 说明以最少的Step就到达了重点。Good.



---

**7. [Gas Station.java](https://github.com/awangdev/LintCode/blob/master/Java/Gas%20Station.java)**      Level: Medium
      

给一串gas station array, 每个index里面有一定数量gas.

给一串cost array, 每个index有一个值, 是reach下一个gas station的油耗.

array的结尾地方, 再下一个点是开头, 形成一个circle route.

找一个index, 作为starting point: 让车子从这个点, 拿上油, 开出去, 还能开回到这个starting point

#### Greedy
- 不论从哪一个点开始, 都可以记录总油耗, total = {gas[i] - cost[i]}. 最后如果total < 0, 必然不能走回来
- 可以记录每一步的油耗积累, remain = {gas[i] - cost[i]}; 一旦 remain < 0, 说明之前的starting point 不合适, 重设: start = i + 1

#### NOT DP
- 看似有点像 House Robber II, 但是问题要求的是: 一个起始点的index
- 而不是求: 最后点可否走完/最值/计数



---

**8. [Maximum Subarray II.java](https://github.com/awangdev/LintCode/blob/master/Java/Maximum%20Subarray%20II.java)**      Level: Medium
      

给一串数组, 找数组中间 两个不交互的 subarray 数字之和的最大值

#### DP
- 考虑两个方向的dp[i]: 包括i在内的subarray max sum. 
- dp[i] 的特点是: 如果上一个 dp[i - 1] + nums[i - 1] 小于 nums[i-1], 那么就舍弃之前, 从头再来:
- dp[i] = Math.max(dp[i - 1] + nums.get(i - 1), nums.get(i - 1));
- 缺点: 无法track全局max, 需要记录max.
- 因为我们现在要考虑从左边/右边来的所有max, 所以要记录maxLeft[] 和 maxRight[] 
- maxLeft[i]: 前i个元素的最大sum是多少 (不断递增); maxRight反之, 从右边向左边
- 最后比较maxLeft[i] + maxRight[i] 最大值
- Space, Time O(n)
- Rolling array, reduce some space, but can not reduce maxLeft/maxRight

#### preSum, minPreSum
- preSum是[0, i] 每个数字一次加起来的值
- 如果维持一个minPreSum, 就是记录[0, i]sum的最小值(因为有可能有负数)
- preSum - minPreSum 就是在 [0, i]里, subarray的最大sum值
- 把这个最大subarray sum 记录在array, left[] 里面
- right[] 是一样的道理
- enumerate一下元素的排列顺位, 最后 max = Math.max(max, left[i] + right[i + 1])



---




 
 
 
## Hash Map (3)
**0. [Longest Words.java](https://github.com/awangdev/LintCode/blob/master/Java/Longest%20Words.java)**      Level: Easy
      

给一串String, 找到最长的长度, 把最长的String全都return

#### HashMap
- <Integer,List<String>>
- 存最长值, 最后map.get(max) 



---

**1. [Anagrams.java](https://github.com/awangdev/LintCode/blob/master/Java/Anagrams.java)**      Level: Medium
      

把anagram找到并output

#### HashMap
- 存在int[26], Arrays.toString(arr) 就是 string key
- anagram都有一样的key, 存进hashmap<string, list of anagrams>
- output anagrams

#### HashMap + Sort
- HashMap 的做法. sort每个string, 存进HashMap, 重复的就是anagrams,最后输出。   
- toCharArray
- Arrays.sort
- Stirng.valueOf(char[])
- 时间n*L*O(logL),L是最长string的长度。

#### Previous Notes
- Arrays.toString(arr)的做法。arr是int[26], assuming only have 26 lowercase letters.    
- Count occurrance, 然后convert to String，作为map的key.
- Time complexity: nO(L)
- 另一种做法：http://www.jiuzhang.com/solutions/anagrams/   
- 1. take each string, count the occurrance of the 26 letters. save in int[]count.   
- 2. hash the int[] count and output a unique hash value; hash = hash * a + num; a = a * b.   
- 3. save to hashmap in the same way as we do. 
- 这一步把for s: strs 里面的时间复杂度降到了O(L). L = s.length().   
- Need to work on the getHash() function.
- 时间变成n*O(L). Better.




---

**2. [Path Sum IV.java](https://github.com/awangdev/LintCode/blob/master/Java/Path%20Sum%20IV.java)**      Level: Medium
      

给一串3-digit 的数组. 每个数字的表达一个TreeNode, 3 digit分别代表: depth.position.value

这串数字已经从小到大排列. 求: 所有可能的 root->leaf path 的所有可能的 path sum 总和. 

#### DFS, Hash Map
- 因为前两个digit可以locate一个node, 所以可以把前两个digit作为key, 定位node.
- 特点: 比如考虑root, 有 n 个leaf, 就会加 n 遍root, 因为有 n 个 unique path嘛.
- 对于每一个node也是一样: 只要有child, 到这个node位置的以上path sum 就要被重加一次.
- format: depth.position.value. (on same level, position may not be continuous)
- approach: map each number into: <depth.position, value>, and dfs. 
- Start from dfs(map, rootKey, sum):
- 1. add node value to sum
- 2. compute potential child.
- 3. check child existence, if exist, add sum to result (for both left/right child). Check existence using the map.
= 4. also, if child exist, dfs into next level



---




 
 
 
## Coordinate DP (12)
**0. [Longest Increasing Subsequence.java](https://github.com/awangdev/LintCode/blob/master/Java/Longest%20Increasing%20Subsequence.java)**      Level: Medium
      

无序数组, 找最长的上升(不需要连续)数组 的长度. 先做O(n^2), 然后可否O(nLogN)?

#### DP, double for loop, O(n^2)
- 考虑nums[i]结尾的时候, 在[0, i) 里count有多少小于nums[i]
- 对于所有 i in [0, n), 最常的increasing序列有多少length?
- max需要在全局维护: nums是无序的, nums[i]也可能是一个很小的值, 所以末尾dp[i]并不是全局的max, 而只是对于nums[i]的max.
- 正因此, 每个nums[i]都要和每个nums[j] 作比较, j < i.
- dp[i] = Maht.max(dp[i], dp[j] + 1); j = [0 , i - 1]
- 时间复杂度  O(n^2)


#### O(nLogN)
- 维持一个list of increasing sequence
- 这个list其实是一个base-line, 记录着最低的increasing sequence.
- 当我们go through all nums的时候, 如果刚好都是上升, 直接append
- 如果不上升, 应该去list里面, 找到最小的那个刚好大于new num的数字, 把它换成num
- 这样就完成了baseline. 举个例子, 比如替换的刚好是在list最后一个element, 等于就是把peak下降了, 那么后面其他的数字就可能继续上升.
- '维护baseline就是一个递增的数列' 的证明, 还没有仔细想.



---

**1. [Unique Paths II.java](https://github.com/awangdev/LintCode/blob/master/Java/Unique%20Paths%20II.java)**      Level: Medium
      

跟unique path的grid一样, 目标走到右下角, 但是grid里面可能有obstacle, 不能跨越. 求unique path 的count.

#### 坐标DP
- dp[i][j]: # of paths to reach grid[i][j]
- dp[i][j] = dp[i - 1][j] + dp[i][j - 1];
- 考虑最终结尾需要的状态:如何组成,写出公式.
- 公式中注意处理能跳掉的block, marked as 1. '到不了', 即为 0 path in dp[i][j].



---

**2. [Bomb Enemy.java](https://github.com/awangdev/LintCode/blob/master/Java/Bomb%20Enemy.java)**      Level: Medium
      

2D grid, 每个格子里面可能是 'W' wall, 'E' enemy, 或者是 '0' empty.

一个bomb可以往4个方向炸. 求在grid上面, 最大能炸掉多少个敌人.

#### Corrdinate DP
- Space, Time: O(MN)
- dp[i][j] 就是(i, j)上最多能炸掉的enemy数量
- dp[i][j] 需要从4个方向加起来, 也就是4个方向都要走一遍, 所以分割成 UP/Down/Left/Right 4个 int[][]
- 最后一步的时候求max
- 分方向考虑的方法很容易想到,但是四个方向移动的代码比较繁琐.
- 往上炸: 要从顶向下考虑
- 往下炸: 要从下向上考虑
- 熟练写2D array index 的变换.

似乎还有一个更简洁的方法, 用col count array: http://www.cnblogs.com/grandyang/p/5599289.html



---

**3. [Unique Path.java](https://github.com/awangdev/LintCode/blob/master/Java/Unique%20Path.java)**      Level: Medium
      

2D array, 算走到最右下角，有多少种方式.

##### DP
- 计数DP.注意方程式前两位置加在一起: 前两种情况没有overlap, 也不会缺情况.
- 注意initialization, 归1.
- 需要initialize的原因是,也是一个reminder: 在方程中会出现-1index
- Of course, row i = 0, or col j = 0, there is only 1 way to access
- time O(mn), space O(mn)

##### 滚动数组
- [i] 只跟 [i - 1] 有关系, 用 curr/prev 建立滚动数组.
- space O(n) 优化空间




---

**4. [Maximal Square.java](https://github.com/awangdev/LintCode/blob/master/Java/Maximal%20Square.java)**      Level: Medium
      

只能往右边,下面走, 找面积最大的 square. 也就是找到变最长的 square.

#### DP
- 正方形, 需要每条边都是一样长度.
- 以右下角为考虑点, 必须满足条件: left/up/diagonal的点都是1
- 并且, 如果三个点分别都衍生向三个方向, 那么最长的 square 边就是他们之中的最短边 (受最短边限制)
- dp[i][j]: max square length when reached at (i, j), from the 3 possible directions
- dp[i][j] = Math.min(Math.min(dp[i - 1][j], dp[i][j - 1]), dp[i - 1][j - 1]) + 1;
- Space, time O(mn)

##### init
每个点都可能是边长1, 如果 matrix[i][j] == '1'

##### 滚动数组
[i] 和 [i - 1] 之间的关系, 想到滚动数组优化 space, O(n) sapce.



---

**5. [Longest Continuous Increasing Subsequence.java](https://github.com/awangdev/LintCode/blob/master/Java/Longest%20Continuous%20Increasing%20Subsequence.java)**      Level: Easy
      

找连续的持续上升子序列的长度.

#### Coordinate DP
- 1D coordinate, dp 的角标, 就是代表 index i 的状态
- 求最值, dp[i] = 在index i位置的最长子序列
- 如果 nums[i] > nums[i - 1], dp[i] = dp[i - 1] + 1
- 如果没有持续上升, 那么dp[i] = 1, 重头来过
- maintain max

#### Basic
- 用一个数存current count,  maintain max



---

**6. [Minimum Path Sum.java](https://github.com/awangdev/LintCode/blob/master/Java/Minimum%20Path%20Sum.java)**      Level: Medium
      

#### DP
- Time, Space O(MN)
- 往右下角走, 计算最短的 path sum. 典型的坐标型.
- 注意: init 第一行的时候, 要accumulate dp[0][j - 1] + grid[i][j], 而不是单纯assign grid[i][j]

#### Rolling Array
- Time O(MN), Space O(1)
- 需要在同一个for loop里面完成initialization, 和使用dp[i][j]
- 原因: dp[i % 2][j] 在被计算出来的时候, 是几乎马上在下一轮是要被用的; 被覆盖前不备用,就白算
- 如果按照第一种方法, 在开始initialize dp, 看起来固然简单, 但是不方便空间优化



---

**7. [Continuous Subarray Sum.java](https://github.com/awangdev/LintCode/blob/master/Java/Continuous%20Subarray%20Sum.java)**      Level: Medium
      

给一个非负数的数列和数字k(可正负, 可为0). 找到连续子序列(长度超过2), 使得这个subarray的sum 是 k的倍数. 问: 是否可能?

#### DP
- O(n^2)
- 需要记录在0 ~ i点(包括nums[i], 以nums[i]结尾)的sum, 坐标型动态规划.
- dp[i] = dp[i - 1] + nums[i];
- 最后移动, 作比较

#### 直接算结果
- 从sum = 每次[i ~ j]的所有情况
- 验证



---

**8. [Russian Doll Envelopes.java](https://github.com/awangdev/LintCode/blob/master/Java/Russian%20Doll%20Envelopes.java)**      Level: Hard
      

俄罗斯套娃, 这里用envelope来表现. 给一串array, 每一个[x, y] 是envelope 长宽. [[5,4],[6,4],[6,7],[2,3]]. 

看用这些套娃, 可以最多套几个.

#### DP: 1D Coordinate
- envelopes没有顺序, 先排序 (主要根据第一个index排序)
- 然后观察: 排序过后, 就变成了1D的坐标动态规划.
- max number 取决于上一个成功Russian doll的 max value + 1
- 上一个index不知道, 所以遍历找上一个index. 
- 当下index i 的状态, 取决于前面index j 的状态, 所以遍历两个index.
- O(n^2)的DP, n = envelopes.length;

#### DP: 2D Coordinate
- 这个方法是自己想出来的, 但是时间复杂度太大, timeout
- 把envelop标记在2D grid上面, 然后像走机器人一样, 求到最右下角的最大 count max.
- count 当下能存在多少Russian doll
- 两种情况: 当下coordinate 没有target, 当下coordinate有target
- 当下coordinate 没有target: 如同机器人走法, Math.max(dp[i - 1][j], dp[i][j - 1])
- 当下coordinate 有target: dp[i - 1][j - 1] + dp[i][j]
- timeout: O(n^2), n = largest coordinate.




---

**9. [Jump Game II.java](https://github.com/awangdev/LintCode/blob/master/Java/Jump%20Game%20II.java)**      Level: Hard
      

给一串数字 是可以跳的距离. goal: 跳到最后的index 所可能用的最少次数.

#### DP 
- DP[i]: 在i点记录，走到i点上的最少jump次数
- dp[i] = Math.min(dp[i], dp[j] + 1);
- condition (j + nums[j] >= i)
- 注意使用 dp[i] = Integer.MAX_VALUE做起始值, 来找min

#### Previous Notes
- Greedy, 图解 http://www.cnblogs.com/lichen782/p/leetcode_Jump_Game_II.html
- 维护一个range, 是最远我们能走的. 
- index/i 是一步一步往前, 每次当 i <= range, 做一个while loop， 在其中找最远能到的地方 maxRange
- 然后更新 range = maxRange
- 其中step也是跟index是一样, 一步一步走.
- 最后check的condition是，我们最远你能走的range >= nums.length - 1, 说明以最少的Step就到达了重点。Good.



---

**10. [Longest Increasing Continuous subsequence.java](https://github.com/awangdev/LintCode/blob/master/Java/Longest%20Increasing%20Continuous%20subsequence.java)**      Level: Easy
      

https://leetcode.com/problems/longest-continuous-increasing-subsequence/description/

O(n)跑2遍for.
O(1)是用了两个int来存：每次到i点时，i点满足条件或不满足条件所有的longestIncreasingContinuousSubsequence.
特点：返跑一回，ans还是继续和left轮的ans作比较；求的所有情况的最大值嘛。



---

**11. [Longest Increasing Continuous subsequence II.java](https://github.com/awangdev/LintCode/blob/master/Java/Longest%20Increasing%20Continuous%20subsequence%20II.java)**      Level: Medium
      

#### Coordinate DP
- due to access permission, not test
- dp[i][j]: longest continuous subsequence length at coordinate (i, j)
- dp[i][j] should come from (i-1,j) and (i, j-1).
- dp[0][0] = 1
- condition: from up/left, must be increasing
- return dp[m-1][n-1]

#### Memoization
- O(mn) space for dp and flag.
- O(mn) runtime because each spot will be marked once visited. 
- 这个题目的简单版本一个array的例子：从简单题目开始想DP会简单一点。每个位置，都是从其他位置（上下左右）来的dpValue +　１.　如果啥也没有的时候，init state 其实都是1， 就一个数字，不增不减嘛。




---




 
 
 
## Monotonous Stack (1)
**0. [Largest Rectangle in Histogram.java](https://github.com/awangdev/LintCode/blob/master/Java/Largest%20Rectangle%20in%20Histogram.java)**      Level: Hard
      

给n个bar,组成柱状图histogram. 求在这一排柱状图里面可以找到的面积最大的长方形.

思考: 找长方形面积, 无非是找两个index, 然后底边长度 * height.

#### Monotonous Stack
- 重点是根据找Histogram里面rectangle的性质, 维持一个单调递增的Stack
- 在loop over indexes的时候:
- 如果高度>= previous peek(), 那么对于那个peek, 就意味着, 往下走, 一直走高嘛, 之前的peek总可以继续抄底
- 什么时候不能抄底了呢? 就是有一个下降趋势的时候
- 这时候并不是calculate所有前面的peek, 而是考虑 大于 current height的之前所有的peek.
- 把这些peek到 current height 前一格的rectangle全部找出来: stack.pop()
- 这个stack.pop()的过程里面, 其实没有算上 current height, 因为需要留到下一轮, 把current index加进stack 再说
- 为什么用stack? 因为需要知道连续递增的peek, stack.peek() O(1), 好用
  而其实不用stack, 也可以用其他方式记录所有height, 只不过要 O(n)去找peek不方便

#### 知识点
- 理解monotonous stack 是如何被维护的
- 维护monotonous stack 是题目需要, 而不是stack本身性质, 是一种借助 stack.peek() O(1)的巧妙用法.




---




 
 
 
## Binary Tree (7)
**0. [Flatten Binary Tree to Linked List.java](https://github.com/awangdev/LintCode/blob/master/Java/Flatten%20Binary%20Tree%20to%20Linked%20List.java)**      Level: Medium
      

给一个binary tree, 把tree做成 linked list的形式, in-place.

#### DFS
- 分析题意后, 按照题意: Flatten the tree, no extra space.
1. reserve right child
2. DFS flatten部分
3. 移花接木
4. flatten 剩下的.

##### 注意
- 顺序一定要清楚, 不能写错, 写几个example可以看出来
- 移动的那些node, 要把node.left = null, 清扫干净



---

**1. [Binary Tree Paths.java](https://github.com/awangdev/LintCode/blob/master/Java/Binary%20Tree%20Paths.java)**      Level: Easy
      

给一个binary tree, 返回所有root-to-leaf path

#### DFS
- Recursive:分叉. dfs.

#### Iterative
- Iterative, 非递归练习了一下
- 因为要每次切短list, 所以再加了一个Stack 来存level
- 单这道题用dfs更简单, 因为找的就是从头到尾的path, 是dfs的pattern




---

**2. [Expression Tree Build.java](https://github.com/awangdev/LintCode/blob/master/Java/Expression%20Tree%20Build.java)**      Level: Hard
      

给一串字符, 表示的是 公式 expression. 把公式变成expression tree

#### Monotonous Stack
- 和Max-tree一样，https://leetcode.com/problems/maximum-binary-tree
- 用到bottom->top递增的stack: 最底下的root维持成最小的element.
- 这个题目是Min-tree， 头上最小，Logic 和max-tree如出一辙   
- Space: O(n) 
- Time on average: O(n).

#### 特点
- TreeNode: 用一个并不是最终结果的TreeNode, 存weight, 用来排序
- 用base weight的概念权衡同一个层面的 符号, 数字 顺序
- 每一个character都是一个节点, 都有自己的weight. 用一个TreeNode来存weight value, 利用用weight来判断: 
- 1. (while loop) 如果node.val <= stack.peek().nodeValue, 把当前stack.peek() 变成 left child. 
- 2. (if condition) 如果stack有残余, 把当前node变成 stack.peek().rightChild 




---

**3. [Expression Evaluation.java](https://github.com/awangdev/LintCode/blob/master/Java/Expression%20Evaluation.java)**      Level: Hard
      

给一个公式 expression, array of strings, 然后evaluate expression 结果.

#### DFS on Expression Tree
- 计算 expression 的值: 1. 建造 expression tree. 2. DFS计算结果
- Expression Tree: Minimum Binary Tree (https://lintcode.com/en/problem/expression-tree-build/)
- build好Min Tree以后，做PostTraversal. 
- Divde and Conquer: 先recursively找到 left和right的大小， 然后evaluate中间的符号
- Time, Space O(n), n = # expression nodes

### Note
- 1. Handle数字时，若left&&right Child全Null,那必定是我们weight最大的数字node了。   
- 2. 若有个child是null,那就return另外一个node。    
- 3. prevent Integer overflow　during operation:过程中用个Long，最后结局在cast back to int.



---

**4. [Convert Expression to Polish Notation.java](https://github.com/awangdev/LintCode/blob/master/Java/Convert%20Expression%20to%20Polish%20Notation.java)**      Level: Hard
      

给一串字符, 用来表示公式expression. 把这个expression转换成 Polish Notation (PN).

#### Expression Tree
- Expression Tree: Minimum Binary Tree (https://lintcode.com/en/problem/expression-tree-build/)
- 根据题意做出Expression Tree出来以后: 来个Pre-order-traversal 就能记录下 Polish Notation
- 本题没有给'ExpressionTreeNode', 所以把TreeNode就当做成我们需要的node, 里面扩展成有left/right child就可以了.
- Note: label需要是String. 虽然 Operator是长度为1的char, 但是数字可为多位



---

**5. [Convert Expression to Reverse Polish Notation.java](https://github.com/awangdev/LintCode/blob/master/Java/Convert%20Expression%20to%20Reverse%20Polish%20Notation.java)**      Level: Hard
      

给一串字符, 用来表示公式expression. 把这个expression转换成 Reverse Polish Notation (RPN).

#### Expression Tree
- Expression Tree: Minimum Binary Tree (https://lintcode.com/en/problem/expression-tree-build/)
- 根据题意做出Expression Tree出来以后: 来个Post-order-traversal 就能记录下 Reverse Polish Notation
- 本题没有给'ExpressionTreeNode', 所以把TreeNode就当做成我们需要的node, 里面扩展成有left/right child就可以了.



---

**6. [Basic Calculator.java](https://github.com/awangdev/LintCode/blob/master/Java/Basic%20Calculator.java)**      Level: Hard
      

给一个expression String, 要evaluate这个expression的值.

Expression string 里面包括 +, -, 整数, 开合括号, 还有space.

#### Expression Tree
- Expression Tree是一个 weight-based的 min-tree 
- 基于 运算符号 + 数字的 tree: 数字永远在leaf, 然后符号是tree node,  括号不出现在tree里面
- 用 monotonuous stack 来构建这个tree

##### Thinking points
- Understand Expression Tree
- Use stack to build the expression tree + understand the weight system
- Use post-order traversal to evaluate the tree
- 注意, input里面的数字不会是single digit, 所以需要一个buffer存number string
- 整个题目的做法, 可以参照 `Expression Evaluation`



---




 
 
 
## Expression Tree (5)
**0. [Expression Tree Build.java](https://github.com/awangdev/LintCode/blob/master/Java/Expression%20Tree%20Build.java)**      Level: Hard
      

给一串字符, 表示的是 公式 expression. 把公式变成expression tree

#### Monotonous Stack
- 和Max-tree一样，https://leetcode.com/problems/maximum-binary-tree
- 用到bottom->top递增的stack: 最底下的root维持成最小的element.
- 这个题目是Min-tree， 头上最小，Logic 和max-tree如出一辙   
- Space: O(n) 
- Time on average: O(n).

#### 特点
- TreeNode: 用一个并不是最终结果的TreeNode, 存weight, 用来排序
- 用base weight的概念权衡同一个层面的 符号, 数字 顺序
- 每一个character都是一个节点, 都有自己的weight. 用一个TreeNode来存weight value, 利用用weight来判断: 
- 1. (while loop) 如果node.val <= stack.peek().nodeValue, 把当前stack.peek() 变成 left child. 
- 2. (if condition) 如果stack有残余, 把当前node变成 stack.peek().rightChild 




---

**1. [Expression Evaluation.java](https://github.com/awangdev/LintCode/blob/master/Java/Expression%20Evaluation.java)**      Level: Hard
      

给一个公式 expression, array of strings, 然后evaluate expression 结果.

#### DFS on Expression Tree
- 计算 expression 的值: 1. 建造 expression tree. 2. DFS计算结果
- Expression Tree: Minimum Binary Tree (https://lintcode.com/en/problem/expression-tree-build/)
- build好Min Tree以后，做PostTraversal. 
- Divde and Conquer: 先recursively找到 left和right的大小， 然后evaluate中间的符号
- Time, Space O(n), n = # expression nodes

### Note
- 1. Handle数字时，若left&&right Child全Null,那必定是我们weight最大的数字node了。   
- 2. 若有个child是null,那就return另外一个node。    
- 3. prevent Integer overflow　during operation:过程中用个Long，最后结局在cast back to int.



---

**2. [Convert Expression to Polish Notation.java](https://github.com/awangdev/LintCode/blob/master/Java/Convert%20Expression%20to%20Polish%20Notation.java)**      Level: Hard
      

给一串字符, 用来表示公式expression. 把这个expression转换成 Polish Notation (PN).

#### Expression Tree
- Expression Tree: Minimum Binary Tree (https://lintcode.com/en/problem/expression-tree-build/)
- 根据题意做出Expression Tree出来以后: 来个Pre-order-traversal 就能记录下 Polish Notation
- 本题没有给'ExpressionTreeNode', 所以把TreeNode就当做成我们需要的node, 里面扩展成有left/right child就可以了.
- Note: label需要是String. 虽然 Operator是长度为1的char, 但是数字可为多位



---

**3. [Convert Expression to Reverse Polish Notation.java](https://github.com/awangdev/LintCode/blob/master/Java/Convert%20Expression%20to%20Reverse%20Polish%20Notation.java)**      Level: Hard
      

给一串字符, 用来表示公式expression. 把这个expression转换成 Reverse Polish Notation (RPN).

#### Expression Tree
- Expression Tree: Minimum Binary Tree (https://lintcode.com/en/problem/expression-tree-build/)
- 根据题意做出Expression Tree出来以后: 来个Post-order-traversal 就能记录下 Reverse Polish Notation
- 本题没有给'ExpressionTreeNode', 所以把TreeNode就当做成我们需要的node, 里面扩展成有left/right child就可以了.



---

**4. [Basic Calculator.java](https://github.com/awangdev/LintCode/blob/master/Java/Basic%20Calculator.java)**      Level: Hard
      

给一个expression String, 要evaluate这个expression的值.

Expression string 里面包括 +, -, 整数, 开合括号, 还有space.

#### Expression Tree
- Expression Tree是一个 weight-based的 min-tree 
- 基于 运算符号 + 数字的 tree: 数字永远在leaf, 然后符号是tree node,  括号不出现在tree里面
- 用 monotonuous stack 来构建这个tree

##### Thinking points
- Understand Expression Tree
- Use stack to build the expression tree + understand the weight system
- Use post-order traversal to evaluate the tree
- 注意, input里面的数字不会是single digit, 所以需要一个buffer存number string
- 整个题目的做法, 可以参照 `Expression Evaluation`



---




 
 
 
## Binary Search (25)
**0. [Guess Number Higher or Lower.java](https://github.com/awangdev/LintCode/blob/master/Java/Guess%20Number%20Higher%20or%20Lower.java)**      Level: Easy
      

binary search 公式



---

**1. [2 Sum II - Input array is sorted.java](https://github.com/awangdev/LintCode/blob/master/Java/2%20Sum%20II%20-%20Input%20array%20is%20sorted.java)**      Level: Medium
      

升序array, 找2SUM.

#### 方法1:
- 排序好的array. Two pointer移动start和end，核查sum.
- 注意sum用long.
- O(n) time

#### 方法2: Binary Search, 因为已经排好序了啊
- 定住一个valueA, 然后在剩下的里面 binary serach 找 (target - valueB)
- O(nLogN), 就不写了



---

**2. [2 Sum II.java](https://github.com/awangdev/LintCode/blob/master/Java/2%20Sum%20II.java)**      Level: Medium
      

与 2sum II - input array is sorted类似. 都是sort array, 然后two pointer.

LintCode的题. 注意找的是greater/bigger than target。

由于给定条件允许O(nLogn):   
   sort
   two pointer

while里面two pointer移动。每次如果num[left]+num[right] > target，那么其中所有num[left++]的加上num[right]都>target.   
也就是,num[right]不动，计算加入挪动left能有多少组，那就是: right-left这么多。 全部加到count上去。     
然后right--.换个right去和前面的left部分作比较。



---

**3. [Longest Increasing Subsequence.java](https://github.com/awangdev/LintCode/blob/master/Java/Longest%20Increasing%20Subsequence.java)**      Level: Medium
      

无序数组, 找最长的上升(不需要连续)数组 的长度. 先做O(n^2), 然后可否O(nLogN)?

#### DP, double for loop, O(n^2)
- 考虑nums[i]结尾的时候, 在[0, i) 里count有多少小于nums[i]
- 对于所有 i in [0, n), 最常的increasing序列有多少length?
- max需要在全局维护: nums是无序的, nums[i]也可能是一个很小的值, 所以末尾dp[i]并不是全局的max, 而只是对于nums[i]的max.
- 正因此, 每个nums[i]都要和每个nums[j] 作比较, j < i.
- dp[i] = Maht.max(dp[i], dp[j] + 1); j = [0 , i - 1]
- 时间复杂度  O(n^2)


#### O(nLogN)
- 维持一个list of increasing sequence
- 这个list其实是一个base-line, 记录着最低的increasing sequence.
- 当我们go through all nums的时候, 如果刚好都是上升, 直接append
- 如果不上升, 应该去list里面, 找到最小的那个刚好大于new num的数字, 把它换成num
- 这样就完成了baseline. 举个例子, 比如替换的刚好是在list最后一个element, 等于就是把peak下降了, 那么后面其他的数字就可能继续上升.
- '维护baseline就是一个递增的数列' 的证明, 还没有仔细想.



---

**4. [Copy Books.java](https://github.com/awangdev/LintCode/blob/master/Java/Copy%20Books.java)**      Level: Hard
      

给一串书pages[i], k个人, pages[i] 代表每本书的页数. k个人从不同的点同时开始抄书. 

问, 最快什么时候可以抄完?

#### Partition DP
- 第一步, 理解题目要求的问题: 前k个人copy完n本书, 找到最少的用时; 也可以翻译成, n本书, 让k个人来copy, 也就是分割成k段.
- 最后需要求出 dp[n][k]. 开: int[n+1][k+1]. 
- 在[0 ~ n - 1]本书里, 最后一个人可以选择copy 1 本, 2 本....n本, 每一种切割的方法的结果都不一样
- 木桶原理, 因为K个人同时开始, 最坏的情况决定结果
- dp[n][k] = Math.min(Math.max(dp[j][k - 1], sum[j+1, n-1]), loop over i, k, j)
- Time: O(kn^2), space O(nk)

##### Init
- Init: dp[0][0] = 0, 0个人0本书
- Integer.MAX_VALUE的运用:
- 当 i = 1, k = 1, 表达式: dp[i][k] = Math.min(dp[i][k], Math.max(dp[j][k - 1], sum));
- 唯一可行的情况就只有一种: i=0, k=0, 刚好 0 个人 copy 0 本书, dp[0][0] = 0.
- 其他情况, i = 1, k = 0, 0 个人读 1本书, 不可能发生: 所以用Integer.MAX_VALUE来冲破 Math.max, 维持荒谬值.
- 当 i=0, k=0 的情况被讨论时候, 上面的方程式才会按照实际情况计算出 dp[i][k]
- 这道题的init是非常重要而tricky的

##### 计算顺序
- k个人, 需要一个for loop; 
- k个人, 从copy1本书开始, 2, 3, ... n-1,所以 i=[1, n], 需要第二个for loop
- 在每一个i上, 切割的方式可以有[0 ~ i] 中, 我们要计算每一种的worst time

##### 滚动数组
- [k] 只有和 [k - 1] 相关
- Space: O(n)

#### Binary Search
- 根据: 每个人花的多少时间(time)来做binary search: 每个人花多久时间, 可以在K个人之内, 用最少的时间完成?
- time variable的范围不是index, 也不是page大小. 而是[minPage, pageSum]
- validation 的时候注意3种情况: 人够用 k>=0, 人不够所以结尾减成k<0, 还有一种是time(每个人最多花的时间)小于当下的页面, return -1
- O(nLogM). n = pages.length; m = sum of pages.




---

**5. [Valid Perfect Square.java](https://github.com/awangdev/LintCode/blob/master/Java/Valid%20Perfect%20Square.java)**      Level: Review
      

Binary找sqrt. 基本 mid+1, mid-1 template.
注意: define index as long. 



---

**6. [Intersection of Two Arrays II.java](https://github.com/awangdev/LintCode/blob/master/Java/Intersection%20of%20Two%20Arrays%20II.java)**      Level: Easy
      

方法1:
用HashMap: 存一个nums1, 再拿nums2 check against map. 时间/空间:O(n)

方法2:
Binary search? 需要array sorted. 否则时间O(nlogn)不值得.
[没做完, 有错]



---

**7. [Find Peak Element.java](https://github.com/awangdev/LintCode/blob/master/Java/Find%20Peak%20Element.java)**      Level: Medium
      

binary search. 
Goal: find peak, where both sides are descending
最左边, 最右边是Integer.MIN_VALUE时候, 也能构成中间数mid是peak的条件.

Note:
没有必要特别check (mid-1)<0或者(mid+1)>=n.
证明:
1. 最左端: 当start=0, end = 2 => mid = 1, mid-1 = 0;
2. 最右端: 当end = n - 1, start = n - 3; mid = (start+end)/2 = n - 2; 
那么mid + 1 = n - 2 + 1 = n - 1 < n 是理所当然的



---

**8. [Pow(x,n).java](https://github.com/awangdev/LintCode/blob/master/Java/Pow(x,n).java)**      Level: Medium
      

傻做就O(n), 要更好就考虑O(logN).
减少重复计算, 一切两半.

注意:
- n/2的奇数偶数
- n的正负
- n == 0的情况, x == 0, x == 1 的情况.


---

**9. [Minimum Size Subarray Sum.java](https://github.com/awangdev/LintCode/blob/master/Java/Minimum%20Size%20Subarray%20Sum.java)**      Level: Medium
      

方法1:
2 pointer, O(n). 找subarray, start 或 end pointer，每次一格这样移动.

好的策略: 
1. 先找一个solution, 定住end. 
2. 然后移动start; 记录每个solution if occurs
3. 然后再移动end，往下找。

Note: 虽然一眼看上去是nested loop.但是分析后，发现其实就是按照end pointer移动的Loop。start每次移动一格。总体上，还是O(n)

方法2:
Double for loop, base i 每次只+1, 所以最后O(n^2)

方法3:
Binary Search, O(nLogN)
Not done yet



---

**10. [Kth Smallest Number in Sorted Matrix.java](https://github.com/awangdev/LintCode/blob/master/Java/Kth%20Smallest%20Number%20in%20Sorted%20Matrix.java)**      Level: Medium
      

方法1:
和Merge K sorted Array/ List 类似：使用PriorityQueue。

因为Array的element无法直接找到next,所以用一个class Node 存value, x,y positions.

方法2:
Binary Search
https://leetcode.com/problems/kth-smallest-element-in-a-sorted-matrix/discuss/85182/my-solution-using-binary-search-in-c


变型: Kth Largest in N Arrays


---

**11. [Find Minimum in Rotated Sorted Array.java](https://github.com/awangdev/LintCode/blob/master/Java/Find%20Minimum%20in%20Rotated%20Sorted%20Array.java)**      Level: Medium
      

画图, 最小值被rotate之后, 变成array中间的最低谷.
并且, 左边山坡的最小值, 大于右边山坡的最大值. 
以此来给binary search做判断.

O(nlogn)



---

**12. [Find Minimum in Rotated Sorted Array II.java](https://github.com/awangdev/LintCode/blob/master/Java/Find%20Minimum%20in%20Rotated%20Sorted%20Array%20II.java)**      Level: Hard
      

一个需要严谨思考的题目. 因为有duplicate, 会导致不断平移, 所以最终time complexity是O(n)
所以不如直接扫一遍, 给出答案.

但是还是写一个Binary Search的样子, 只不过worst结果是O(n)



---

**13. [Find Peak Element II.java](https://github.com/awangdev/LintCode/blob/master/Java/Find%20Peak%20Element%20II.java)**      Level: Hard
      

2Dmatrix, 里面的value有一些递增, 递减的特点(细节比较长, 看原题). 目标是找到peak element

#### DFS

##### 基本原理
- 我们不可能一口气准确定位(x,y), 但是我们可以再一个row/col里面, 找到1D array的 peak.
- 根据这个点, 再往剩下两个方向移动
- 1. 在中间的一行i=midX, 找到peak所在的y.
- 2. 在中间的一列j=midY, 找到peak所在的x. (有可能强势override之前找到的y, 也就是放弃那一行的peak, 在midY上找peak)
- 3. 根据 (x,y) 的4个neighbor check (x,y)是不是 peak, 如果不是, 像更高的位置移动一格
- 4. 根据之前算的 midX, midY 把board分成4个象限, 在每一份里面再继续找
- 这个题目LintCode不给做了, 所以思路对的, 但是解答还没有再次验证.

##### 剪枝/切分象限
- 每次只是找到一个row/col里面的peak而已!
- 找到这个点, 就等于把board切成了两半.
- 然后, 再跟剩下的相邻的两个位置比较, 就知道了哪里更大, 就去哪里找peak, 也就是又切了第二刀.
- 切第二刀的时候, 也要把(x, y) 移到需要取的象限. 进行DFS
- 根据mid row 切割: 
- http://www.jiuzhang.com/solution/find-peak-element-ii/#tag-highlight-lang-java
- http://courses.csail.mit.edu/6.006/spring11/lectures/lec02.pdf

##### 时间复杂度
- 每一个level都减一半
- T(n) = n + T(n/2) = n + n/2 + n/4 + ... + 1 = n(1 + 1/2 + .... + 1/n) = 2n = O(n)

#### Binary Search
- TODO
- O(nLogN)



---

**14. [Sqrt(x).java](https://github.com/awangdev/LintCode/blob/master/Java/Sqrt(x).java)**      Level: Easy
      

#### s- qrt(int x)
- 理解题意, 从[0, x]找一个可以m*m=x的值.
- 注意, 如果找不到, 最后问考官该return一个什么值：按道理，因为return int, 会取整，那么return一个平方最close to x就可以.
- 注意 mid 用 long, 因为很可能超过最大int.

#### sqrt(double x)
- 二分float number, 应该用精度来定义结尾.
- 还是二分, 但是判断条件变成: while ( end - start > eps)
- eps = 1e-12,也就是精度到1e-12



---

**15. [First Bad Version.java](https://github.com/awangdev/LintCode/blob/master/Java/First%20Bad%20Version.java)**      Level: Easy
      

Binary Search

根据isBadVersion的性质，判断还如何end=mid or start=mid.     
isBadVersion 是有方向的嘛，一个点错了，后面全错。



---

**16. [Wood Cut.java](https://github.com/awangdev/LintCode/blob/master/Java/Wood%20Cut.java)**      Level: Medium
      

二分的思想: 判断的是一个 validate() function, 而不是简单的'=='

不需要sort! 为什么呢? 因为我们不是在given array上面二分, 我们是根据最大值在[0, max]上二分.

Overall time: O(nLogM), where M = largest wood length



---

**17. [Find the Duplicate Number.java](https://github.com/awangdev/LintCode/blob/master/Java/Find%20the%20Duplicate%20Number.java)**      Level: Medium
      

- 注意不要思维定式: 以为mid是index
- 这里mid其实是binary search on value [1, n] 的一个value.
- 再次用到validate() function

Time: O(nLogN)



---

**18. [Maximum Average Subarray II.java](https://github.com/awangdev/LintCode/blob/master/Java/Maximum%20Average%20Subarray%20II.java)**      Level: Review
      

给int[] nums 和 window min size k. window size可以大于K. 找最大的连续数列average value.

- Binary Search的思想, 用在所要找的这个 average sum 上面. 大小是在[min, max]之中
- 找k的时候, 是>=k都可以, 巧用一个 min(preSum)的概念.
- 找k的时候, 画图, 可以看出来, 其实要的是 k window 里面的sum [x, i], 所以要用 sum[0, i] - sum[0, x]

需要仔细去读下面的notes.



---

**19. [Classical Binary Search.java](https://github.com/awangdev/LintCode/blob/master/Java/Classical%20Binary%20Search.java)**      Level: Easy
      

#### Binary Search Template
- while: start + 1 < end
- mid = start + (end - start) / 2;
- 根据mid作比较
- 末尾double check start, end.




---

**20. [Closest Binary Search Tree Value.java](https://github.com/awangdev/LintCode/blob/master/Java/Closest%20Binary%20Search%20Tree%20Value.java)**      Level: Easy
      

给一个BST, 和一个double target, 走位找到最接近的number.

#### Recursive
- when less than curr val, consider left
- when greater than curr val, consider right
- dfs到底, 然后每一层比较, 再return

#### Binary Search
- 记录找到过的closest
- Binary Search, 根据current node走位,
- 找到 node.val == target, 或者走位走完, return closest



---

**21. [Count Complete Tree Nodes.java](https://github.com/awangdev/LintCode/blob/master/Java/Count%20Complete%20Tree%20Nodes.java)**      Level: Medium
      

Complete Tree就是说, 最后一个level可能是缺node的(不是说最右下角缺node, 别忘了!)

#### DFS + Optimization
- 每次看最左left depth和最右leaf depth 是不是一样, 如果一样, 直接 2 ^ h - 1就好
- 不一样的话, 再DFS

##### Trick
- 直接DFS会timeout, O(n), 其实可以optimize
- to pass the test with O(h^2), 位运算: Math.pow(2, h) = 2 << (h - 1). 神奇!
- 2 << 1就是把所有bits往左移动一位, 也就是 * 2 

#### Iteratively
- See details in comments inline. 要对tree非常理解
- binary tree one child tree nodes # = 2 ^ h - 1; 所以一个child tree + root = 2 ^ h



---

**22. [Closest Number in Sorted Array.java](https://github.com/awangdev/LintCode/blob/master/Java/Closest%20Number%20in%20Sorted%20Array.java)**      Level: Easy
      

- Binary Search 的一种变型, LintCode无法再跑一边.
- 考虑mid-1, mid+1.
- 一旦没有mid = target.index。 那么target最终就narrow down在(mid-1,mid) 或者(mid,mid+1)   



---

**23. [Russian Doll Envelopes.java](https://github.com/awangdev/LintCode/blob/master/Java/Russian%20Doll%20Envelopes.java)**      Level: Hard
      

俄罗斯套娃, 这里用envelope来表现. 给一串array, 每一个[x, y] 是envelope 长宽. [[5,4],[6,4],[6,7],[2,3]]. 

看用这些套娃, 可以最多套几个.

#### DP: 1D Coordinate
- envelopes没有顺序, 先排序 (主要根据第一个index排序)
- 然后观察: 排序过后, 就变成了1D的坐标动态规划.
- max number 取决于上一个成功Russian doll的 max value + 1
- 上一个index不知道, 所以遍历找上一个index. 
- 当下index i 的状态, 取决于前面index j 的状态, 所以遍历两个index.
- O(n^2)的DP, n = envelopes.length;

#### DP: 2D Coordinate
- 这个方法是自己想出来的, 但是时间复杂度太大, timeout
- 把envelop标记在2D grid上面, 然后像走机器人一样, 求到最右下角的最大 count max.
- count 当下能存在多少Russian doll
- 两种情况: 当下coordinate 没有target, 当下coordinate有target
- 当下coordinate 没有target: 如同机器人走法, Math.max(dp[i - 1][j], dp[i][j - 1])
- 当下coordinate 有target: dp[i - 1][j - 1] + dp[i][j]
- timeout: O(n^2), n = largest coordinate.




---

**24. [Last Position of Target.java](https://github.com/awangdev/LintCode/blob/master/Java/Last%20Position%20of%20Target.java)**      Level: Easy
      

给一个sorted integer array, 找target出现的最后的index. array 里有重复数字

有重复,不是末尾点，继续binary search



---




 
 
 
## Array (64)
**0. [Plus One.java](https://github.com/awangdev/LintCode/blob/master/Java/Plus%20One.java)**      Level: Easy
      

简单的实现, 加1, 进位. 唯一取巧的地方, 最后如果要多一位, 一定是10000...这个模式, 可以走捷径, 直接来个+1size的array, 然后第一位=1.
注意,转换成long也不合理,用太多memory.


---

**1. [Wiggle Sort.java](https://github.com/awangdev/LintCode/blob/master/Java/Wiggle%20Sort.java)**      Level: Medium
      

方法1:
排序, nLog(n). 然后把直线上坡变成层叠山峰, 需要每隔几个(题目中是每隔2位)就做个swap 造成高低不平.
Note: 每隔山峰之间是相互没有关系的, 所以每次只要操心 [i], [i-1]两个位置就好了.

方法2:
O(n)
看好奇数偶数位的规律, 然后根据题目给出的规律, 跑一遍, 每次只关注两个位置: 把不合适的[i], [i-1]调换位置就好了.

方法3:
跟法2一样, 只是更巧妙一点罢了:
第一遍想太多. 其实做一个fall-through就能把问题解决，原因是因为：
这样的fall-through每次在乎两个element，可以一口气搞定，无关乎再之前的elements。
特别的一点：flag来巧妙的掌控山峰和低谷的变化。又是神奇的一幕啊！
这样子的奇观，见过就要知道了，没见过的时候有点摸不着头脑。



---

**2. [2 Sum.java](https://github.com/awangdev/LintCode/blob/master/Java/2%20Sum.java)**      Level: Easy
      

tutorial:https://www.youtube.com/watch?v=P8zBxoVY1oI&feature=youtu.be

解法1：相对暴力简洁, HashMap<value, index>，找到一个value, 存一个; 若在HashMap里面 match 到结果, 就return HashMap里存的index. O(n) space && time.

解法2：Sort array, two pointer 前后++,--搜索。Sort 用时O(nlogn).     
1. 第一步 two pointer 找 value.       
2. 注意，要利用额外的空间保留original array， 用来时候找index. (此处不能用HashMap，因为以value 为key，但value可能重复)      
O(n) space, O(nlogn) time.    




---

**3. [2 Sum II - Input array is sorted.java](https://github.com/awangdev/LintCode/blob/master/Java/2%20Sum%20II%20-%20Input%20array%20is%20sorted.java)**      Level: Medium
      

升序array, 找2SUM.

#### 方法1:
- 排序好的array. Two pointer移动start和end，核查sum.
- 注意sum用long.
- O(n) time

#### 方法2: Binary Search, 因为已经排好序了啊
- 定住一个valueA, 然后在剩下的里面 binary serach 找 (target - valueB)
- O(nLogN), 就不写了



---

**4. [2 Sum II.java](https://github.com/awangdev/LintCode/blob/master/Java/2%20Sum%20II.java)**      Level: Medium
      

与 2sum II - input array is sorted类似. 都是sort array, 然后two pointer.

LintCode的题. 注意找的是greater/bigger than target。

由于给定条件允许O(nLogn):   
   sort
   two pointer

while里面two pointer移动。每次如果num[left]+num[right] > target，那么其中所有num[left++]的加上num[right]都>target.   
也就是,num[right]不动，计算加入挪动left能有多少组，那就是: right-left这么多。 全部加到count上去。     
然后right--.换个right去和前面的left部分作比较。



---

**5. [Maximum Product Subarray.java](https://github.com/awangdev/LintCode/blob/master/Java/Maximum%20Product%20Subarray.java)**      Level: Medium
      

从一组数列(正负都有)里面找一串连续的子序列, 而达到乘积product最大值.

#### DP
- 求最值, 想到DP. Time/Space O (n)
- 两个特别处: 
- 1. 正负数情况, 需要用两个DP array. 
- 2. continuous prodct 这个条件决定了在Math.min, Math.max的时候, 
- 是跟nums[x]当下值比较的, 如果当下值更适合, 会舍去之前的continous product, 然后重新开始.
- 这也就注定了需要一个global variable 来hold result.

#### Space optimization, rolling array
- maxProduct && minProduct 里面的 index i, 都只能 i - 1相关, 所以可以省去redundant operatoins
- Time: O(n), space: O(1)



---

**6. [3 Sum Closest.java](https://github.com/awangdev/LintCode/blob/master/Java/3%20Sum%20Closest.java)**      Level: Medium
      

3Sum 的一种简单形式, 并且都没有找index, value, 而只是找个sum罢了.

double for loop。 2Sum只能用土办法 left/right 2 pointers。 O(n^2)

注意：check closest时候用long, 以免int不够用



---

**7. [Triangle Count.java](https://github.com/awangdev/LintCode/blob/master/Java/Triangle%20Count.java)**      Level: Medium
      

其实也就是3sum的变形, 或者而说2sum的变形. 主要用2 pointers来做.
注意, 在选index时候每次定好一个 [0 ~ i], 在这里面找点start, end, 然后i 来组成triangle.
Note巧妙点:
在此之中, 如果一种start/end/i 符合, 那么从这个[start~end]中, 大于start的都可以, 所以我们count+= end-start.
反而言之, <end的其他index, 就不一定能符合nums[start] + nums[end] > nums[i]



---

**8. [3 Sum.java](https://github.com/awangdev/LintCode/blob/master/Java/3%20Sum.java)**      Level: Medium
      

方法1:
sort array, for loop + two pointer. O(n)
处理duplicate wthin triplets: 
如果最外圈的移动点i重复, 一直顺到结尾的最后一个再用.
如果是triplet内有重复, 用完start point, 移动到结尾.

Previous notes:
注意:   
   1. 找 value triplets, 多个结果。注意，并非找index。    
   2. 要升序, 第一层for loop 从最后一个元素挑起, 保证了顺序。    
   3. 去掉duplicate: check用过的同样的数字，都跳掉。不需要用同样的数字再计算一边已有结果。

步骤:   
   1. For loop 挑个数字A.    
   2. 2Sum 出一堆2个数字的结果    
   3. Cross match 步骤1里面的A.   

时间 O(n^2), 两个nested loop

另外, 还是可以用HashMap来做2Sum。稍微短点。还是要注意handle duplicates.




---

**9. [Unique Paths II.java](https://github.com/awangdev/LintCode/blob/master/Java/Unique%20Paths%20II.java)**      Level: Medium
      

跟unique path的grid一样, 目标走到右下角, 但是grid里面可能有obstacle, 不能跨越. 求unique path 的count.

#### 坐标DP
- dp[i][j]: # of paths to reach grid[i][j]
- dp[i][j] = dp[i - 1][j] + dp[i][j - 1];
- 考虑最终结尾需要的状态:如何组成,写出公式.
- 公式中注意处理能跳掉的block, marked as 1. '到不了', 即为 0 path in dp[i][j].



---

**10. [3 Sum Smaller.java](https://github.com/awangdev/LintCode/blob/master/Java/3%20Sum%20Smaller.java)**      Level: Medium
      

一般的O(n3)肯定不行。在此基础上优化。
发现j,k满足条件时候，(k - j)就是所有 sum <target的情况了。
而一旦>target, 又因为j不能后退，只能k--，那么问题就被锁定了. 这样可以做到O(n2)



---

**11. [Array Partition I.java](https://github.com/awangdev/LintCode/blob/master/Java/Array%20Partition%20I.java)**      Level: Easy
      

从结果出发, 只需要找到加法的结果，而不强调具体配对。
找到排列取单数位的规律，再考虑负数和正数的相同规律，即可找到排列求解的方法。




---

**12. [1-bit and 2-bit Characters.java](https://github.com/awangdev/LintCode/blob/master/Java/1-bit%20and%202-bit%20Characters.java)**      Level: Easy
      

方法1:
Greedy.
从第一个bit开始数: 如果遇到1, 一定是跳两位;如果遇到0, 一定是跳一位.
loop to end, and see if index reaches the end.

方法2:
用DP硬做了一下: 
1. 如果i位是0, 那么前面dp[i-1]或者dp[i-2] true就够了.
2. 如果i位是1, 那么i-1位必须是1才满足规则, 并且 dp[i-2]需要true.



---

**13. [Non-decreasing Array.java](https://github.com/awangdev/LintCode/blob/master/Java/Non-decreasing%20Array.java)**      Level: Easy
      

比较升序的时候, 必须要估计到 i-1, i, i+1三个数位.
写出来i-1, i+1之间的关系, 然后做合理的fix.

需要真的fix数组, 因为loop through做比较时会用到fix后的数字.



---

**14. [Max Consecutive Ones.java](https://github.com/awangdev/LintCode/blob/master/Java/Max%20Consecutive%20Ones.java)**      Level: Easy
      

Basic. Math.max track结果。
记得在有对外操作的loop后，一定要把result object清理干净。



---

**15. [Find All Numbers Disappeared in an Array.java](https://github.com/awangdev/LintCode/blob/master/Java/Find%20All%20Numbers%20Disappeared%20in%20an%20Array.java)**      Level: Easy
      

方法1:
换到正确的位置。
需要小心handle i, 因为不知道换到nums[i]上的是什么，所以必须原地清理干净 方能move on.

方法2:
做标记！
很巧妙地运用了标记的方法, 标记成负数，证明visit过。
Preserve原数的负数，这样可以继续用此负数的绝对值来寻找原数所该被定的位置。非常巧妙！

方法3:
做标记！
跟方法2类似，也是做标记，这一次是加上一个大于n的数（因为题目给了n的border），最后check一下就好。为不超Integer.MAX_VALUE, 每次加n前，取余数。

做标记的方法固然快，但是相对来说比较hacky，在常规的代码中，估计不会用到.




---

**16. [Maximum Average Subarray I.java](https://github.com/awangdev/LintCode/blob/master/Java/Maximum%20Average%20Subarray%20I.java)**      Level: Easy
      

简单的求sum, 同时求max, 结尾求余数就好.


---

**17. [Largest Number At Least Twice of Others.java](https://github.com/awangdev/LintCode/blob/master/Java/Largest%20Number%20At%20Least%20Twice%20of%20Others.java)**      Level: Easy
      

找最大值, 和第二大的值, 看是否符合题意, 就行了.
分析题意, 最简单方法, 可以loop 两遍: 找最值; 作比较.
但其实, 举个反例: 有一个不满足, 就够反对这个'at least twice of alllll others'.



---

**18. [Toeplitz Matrix.java](https://github.com/awangdev/LintCode/blob/master/Java/Toeplitz%20Matrix.java)**      Level: Easy
      

似乎没什么算法特点, 就是array基本运算, 然后分割成一个helper function去做重复计算, 剪短代码.
注意check MxN 的分界线.



---

**19. [Find Peak Element.java](https://github.com/awangdev/LintCode/blob/master/Java/Find%20Peak%20Element.java)**      Level: Medium
      

binary search. 
Goal: find peak, where both sides are descending
最左边, 最右边是Integer.MIN_VALUE时候, 也能构成中间数mid是peak的条件.

Note:
没有必要特别check (mid-1)<0或者(mid+1)>=n.
证明:
1. 最左端: 当start=0, end = 2 => mid = 1, mid-1 = 0;
2. 最右端: 当end = n - 1, start = n - 3; mid = (start+end)/2 = n - 2; 
那么mid + 1 = n - 2 + 1 = n - 1 < n 是理所当然的



---

**20. [Majority Element.java](https://github.com/awangdev/LintCode/blob/master/Java/Majority%20Element.java)**      Level: Easy
      

方法1: Vote 计数, vote++, vote--到最后剩下的就是winner. Time O(n), Space O(1)
Majority Number是指超半数. 超半数的数字, 最后都会至少有vote>=1: match current majority number，vote++；if not, vote--. 
注意：assume valid input, 是一定有一个majority number的。否则此法不成。[1,1,1,2,2,2,3]是个invalid input,结果是3，当然也错了。

方法2: HashMap count occurance. Time, Space: O(n)

方法3: Bit manipulation. 还没有做.

Related Problems:
Majority Number II，超1/3, 那么就分三份处理，countA, countB来计算最多出现的两个。

Majority Number III, 超1/k, 那么自然分k份。这里用到 HashMap。



---

**21. [Construct Binary Tree from Inorder and Preorder Traversal.java](https://github.com/awangdev/LintCode/blob/master/Java/Construct%20Binary%20Tree%20from%20Inorder%20and%20Preorder%20Traversal.java)**      Level: Medium
      

如题

#### DFS
- 和Construct from Inorder && Postorder 想法一样。
- 写出Preorder和Inorder的字母例子，发现Preorder的开头总是这Level的root。依此写helper,注意处理index。
- 跟Convert Sorted Array to Binary Tree类似, 找到对应的index, 然后:
- node.left = dfs(...), node.right = dfs(...)
- Divide and Conquer



---

**22. [Minimum Size Subarray Sum.java](https://github.com/awangdev/LintCode/blob/master/Java/Minimum%20Size%20Subarray%20Sum.java)**      Level: Medium
      

方法1:
2 pointer, O(n). 找subarray, start 或 end pointer，每次一格这样移动.

好的策略: 
1. 先找一个solution, 定住end. 
2. 然后移动start; 记录每个solution if occurs
3. 然后再移动end，往下找。

Note: 虽然一眼看上去是nested loop.但是分析后，发现其实就是按照end pointer移动的Loop。start每次移动一格。总体上，还是O(n)

方法2:
Double for loop, base i 每次只+1, 所以最后O(n^2)

方法3:
Binary Search, O(nLogN)
Not done yet



---

**23. [Find Minimum in Rotated Sorted Array.java](https://github.com/awangdev/LintCode/blob/master/Java/Find%20Minimum%20in%20Rotated%20Sorted%20Array.java)**      Level: Medium
      

画图, 最小值被rotate之后, 变成array中间的最低谷.
并且, 左边山坡的最小值, 大于右边山坡的最大值. 
以此来给binary search做判断.

O(nlogn)



---

**24. [Find Minimum in Rotated Sorted Array II.java](https://github.com/awangdev/LintCode/blob/master/Java/Find%20Minimum%20in%20Rotated%20Sorted%20Array%20II.java)**      Level: Hard
      

一个需要严谨思考的题目. 因为有duplicate, 会导致不断平移, 所以最终time complexity是O(n)
所以不如直接扫一遍, 给出答案.

但是还是写一个Binary Search的样子, 只不过worst结果是O(n)



---

**25. [Word Search.java](https://github.com/awangdev/LintCode/blob/master/Java/Word%20Search.java)**      Level: Medium
      

Backtracking:
找到开头的字母, 然后recursively DFS 去把word串到底:
每到一个字母, 朝四个方向走, 之中一个true就可以.

Note:每次到一个字母，mark一下'#'. 4个path recurse回来后，mark it back.

Backtracking方法2:    
用一个boolean visited[][]





---

**26. [Trapping Rain Water.java](https://github.com/awangdev/LintCode/blob/master/Java/Trapping%20Rain%20Water.java)**      Level: Hard
      

这道题目的方法比较多.
#### 方法1
Array, 维持一个左手最高墙array, 右手最高强array.
对于每个index而言, vertically 能存放的最大水柱, 就是靠左右最高墙决定的:
min(leftHighestWall, rightHighestWall) - currHeight.

#### 方法2
方法1上面的优化, two pointer, 还是找左边最高和右边最高. O(1) space.
利用到了方法3里面的想法一样: 整个structure是被中间的最高bar 二分天下:
左边按照maxLeft来计算, 右边按照maxRight来计算.

#### 方法3
2 Pointers， 双面夹击:
1. 找中间最高bar的index    
2. 两面往中心扫：每次加上（topBarIndex - currIndex）* (elevation from previous index).也就是每次加一个横条。    
3. 每次还要减去block自身的height

#### 方法4
主要想法和方法3一致: 在山坡下坡的基础上, 一直用stack堆积bottom. 
最后遇到上升之前, 此时bottom可以用来跟stack之前堆积的所有下坡index做比较, 算跟他们高度相差的积水.
用了stack记录下坡, 然后用个while loop一挖到底的想法非常棒.




---

**27. [Largest Rectangle in Histogram.java](https://github.com/awangdev/LintCode/blob/master/Java/Largest%20Rectangle%20in%20Histogram.java)**      Level: Hard
      

给n个bar,组成柱状图histogram. 求在这一排柱状图里面可以找到的面积最大的长方形.

思考: 找长方形面积, 无非是找两个index, 然后底边长度 * height.

#### Monotonous Stack
- 重点是根据找Histogram里面rectangle的性质, 维持一个单调递增的Stack
- 在loop over indexes的时候:
- 如果高度>= previous peek(), 那么对于那个peek, 就意味着, 往下走, 一直走高嘛, 之前的peek总可以继续抄底
- 什么时候不能抄底了呢? 就是有一个下降趋势的时候
- 这时候并不是calculate所有前面的peek, 而是考虑 大于 current height的之前所有的peek.
- 把这些peek到 current height 前一格的rectangle全部找出来: stack.pop()
- 这个stack.pop()的过程里面, 其实没有算上 current height, 因为需要留到下一轮, 把current index加进stack 再说
- 为什么用stack? 因为需要知道连续递增的peek, stack.peek() O(1), 好用
  而其实不用stack, 也可以用其他方式记录所有height, 只不过要 O(n)去找peek不方便

#### 知识点
- 理解monotonous stack 是如何被维护的
- 维护monotonous stack 是题目需要, 而不是stack本身性质, 是一种借助 stack.peek() O(1)的巧妙用法.




---

**28. [Find the Duplicate Number.java](https://github.com/awangdev/LintCode/blob/master/Java/Find%20the%20Duplicate%20Number.java)**      Level: Medium
      

- 注意不要思维定式: 以为mid是index
- 这里mid其实是binary search on value [1, n] 的一个value.
- 再次用到validate() function

Time: O(nLogN)



---

**29. [Game of Life.java](https://github.com/awangdev/LintCode/blob/master/Java/Game%20of%20Life.java)**      Level: Medium
      

#### basic
- 简单的implementation, 把count function写清楚就好.
- time: O(mn), extra space: O(mn)
- 注意结尾要一个个board[i][j]copy

#### follow up
unlimited border? 可能需要分割board. 用大框分割, 每次换行的时候, 重复计算2行就好了. see details below.

#### improvement: do it in place!
- time: O(mn), extra space: O(1)
- bit manipulation: 用第二个bit来存previous value.
- 因为我们只考虑 0 和 1 而已, 所以可以这样取巧. 但是并不scalable.
- 如果需要存multiple state, 可能需要移动更多位, 或者用一个 state map
- 注意 bit manipulation 的细节: <<1, >>1, 还有 mast的用法: |, & 




---

**30. [Maximum Average Subarray II.java](https://github.com/awangdev/LintCode/blob/master/Java/Maximum%20Average%20Subarray%20II.java)**      Level: Review
      

给int[] nums 和 window min size k. window size可以大于K. 找最大的连续数列average value.

- Binary Search的思想, 用在所要找的这个 average sum 上面. 大小是在[min, max]之中
- 找k的时候, 是>=k都可以, 巧用一个 min(preSum)的概念.
- 找k的时候, 画图, 可以看出来, 其实要的是 k window 里面的sum [x, i], 所以要用 sum[0, i] - sum[0, x]

需要仔细去读下面的notes.



---

**31. [Number of Airplane in the sky.java](https://github.com/awangdev/LintCode/blob/master/Java/Number%20of%20Airplane%20in%20the%20sky.java)**      Level: Medium
      

#### Sweep Line
- 把Interval拆分成数轴上的Point 
- 起飞mark 1   
- 降落mark -1     
- 用PriorityQueue排序， loop through queue, 计算(起飞+降落)值可能有的max。

#### 注意
- 同时起飞和降落，就是 1 - 1 = 0. 所以在while loop里面有第二个while loop，    
- 当坐标x重合时，在这里做完所有x点的加减，然后再比较 max。     
- 这避免了错误多count，或者少count



---

**32. [Unique Path.java](https://github.com/awangdev/LintCode/blob/master/Java/Unique%20Path.java)**      Level: Medium
      

2D array, 算走到最右下角，有多少种方式.

##### DP
- 计数DP.注意方程式前两位置加在一起: 前两种情况没有overlap, 也不会缺情况.
- 注意initialization, 归1.
- 需要initialize的原因是,也是一个reminder: 在方程中会出现-1index
- Of course, row i = 0, or col j = 0, there is only 1 way to access
- time O(mn), space O(mn)

##### 滚动数组
- [i] 只跟 [i - 1] 有关系, 用 curr/prev 建立滚动数组.
- space O(n) 优化空间




---

**33. [Maximal Rectangle.java](https://github.com/awangdev/LintCode/blob/master/Java/Maximal%20Rectangle.java)**      Level: Hard
      

#### 方法1: monotonous stack
分解开来, 其实是'Largest Rectangle in Histogram', 只不过这里要自己model heights.
一个2D array里面的rectangle, 最终也是用height * width做出来的.
巧妙在于, 把每一行当做底边, 算出这个底边, 到顶部的height: 
- 如果底边上的一个value==0, 那么算作没有height(以这个底边做rectangle, value==0的位置是空中楼阁, 不能用)
- 如果底边上的value==1, 那么就把上面的height加下来, 做成histogram

如果看具体实例, 有些row似乎是白算的, 但是没有办法, 这是一个搜索的过程, 最终会比较出最优解.

#### 方法2: DP
Coordinate DP?



---

**34. [Coins in a Line II.java](https://github.com/awangdev/LintCode/blob/master/Java/Coins%20in%20a%20Line%20II.java)**      Level: Medium
      

给一串coins, 用values[]表示; 每个coin有自己的value. 先手/后手博弈,
每次只能 按照从左到右的顺序, 拿1个或者2个棋子, 最后看谁拿的总值最大.

MiniMax的思考方法很神奇, 最后写出来的表达式很简单

#### DP, Game Theory 自考过程比较长
- 跟Coins in a line I 不一样: 每个coin的value不同.
- 用到MiniMax的思想, 这里其实是MaxiMin. Reference: http://www.cnblogs.com/grandyang/p/5864323.html
- Goal: 使得player拿到的coins value 最大化.
- 设定dp[i]: 从index i 到 index n的最大值. 所以dp[0]就是我们先手在[0 ~ n]的最大取值 
- 于此同时, 你的对手playerB也想最大化, 而你的选择又不得不被对手的选择所牵制.
- 用MaxiMin的思想, 我们假设一个当下的状态, 假想对手playerB会做什么反应(从对手角度, 如何让我输)
- 在劣势中(对手让我输的目标下)找到最大的coins value sum


##### 推算表达式
- Reference里面详细介绍了表达式如何推到出来, 简而言之:
- 如果我选了i, 那么对手就只能选(i+1), (i+2) 两个位置, 而我在对方掌控时的局面就是min(dp[i+2], dp[i+3])
- 如果我选了i和(i+1), 那么对手就只能选(i+2), (i+3) 两个位置, 而我在对方掌控时的局面就是min(dp[i+3], dp[i+4])
- 大家都是可选1个或者2个coins
- 目标是maximize上面两个最坏情况中的最好结果

##### 简化表达式
- 更加简化一点: 如果我是先手, dp[i]代表我的最大值.
- 取决于我拿了[i], 还是[i] + [i+1], 对手可能是dp[i + 1], 或者是dp[i+2]
- 其实dp[i] = Math.max(sum - dp[i + 1], sum - dp[i + 2]);
- 这里的sum[i] = [i ~ n] 的sum, 减去dp[i+1], 剩下就是dp[i]的值没错了

##### Initialization
- 这个做法是从最后往前推的, 注意initialize dp末尾的值.
- dp = new int[n + 1]; dp[n] = 0; // [n ~ n]啥也不选的时候, 为0.
- sum = new int[n + 1]; sum[n] = 0; // 啥也不选的时候, 自然等于0
- 然后记得initialize (n-1), (n-2)

##### 时间/空间
Time O(n)
Space O(n): dp[], sum[]



---

**35. [Coins in a Line III.java](https://github.com/awangdev/LintCode/blob/master/Java/Coins%20in%20a%20Line%20III.java)**      Level: Hard
      

还是2个人拿n个coin, coin可以有不同的value. 

只不过这次选手可以从任意的一头拿, 而不限制从一头拿. 算先手会不会赢?

#### Memoization + Search
- 跟Coins in a Line II 一样, MaxiMin的思想: 找到我的劣势中的最大值
- dp[i][j] 代表在[i,j]区间上 选手最多能取的value 总和
- 同样, sum[i][j]表示[i] 到 [j]间的value总和
- 对手的最差情况, 也就是先手的最好情况:
- dp[i][j] = sum[i][j] - Math.min(dp[i][j - 1], dp[i + 1][j]);
- 这里需要search, 画出tree可以看明白是如何根据取前后而分段的.

#### 博弈 + 区间DP
- 因为是看区间[i,j]的情况, 所以可以想到是区间 DP
- 这个方法需要复习, 跟数学表达式的推断相关联: S(x) = - S(y) + m. 参考下面的公式推导.
- dp[i][j]表示 从index(i) 到 index(j), 先手可以拿到的最大值与对手的数字差. 也就是S(x).
- 其中一个S(x) = dp[i][j] = a[i] - dp[i + 1][j]
- m 取在开头, m 取在末尾的两种情况:
- dp[i][j] = max{a[i] - dp[i + 1][j], a[j] - dp[i][j - 1]}
- len = 1, 积分就是values[i]
- 最后判断 dp[0][n] >= 0, 最大数字和之差大于0, 就赢.
- 时间/空间 O(n^2)

##### 公式推导
- S(x) = X - Y, 找最大数字和之差, 这里X和Y是选手X的总分, 选手Y的总分. 
- 对于选手X而言: 如果S(x)最大值大于0, 就是赢了; 如果最大值都小于0, 就一定是输了. 
- 选手Y: S(y)来表示 对于Y,  最大数字和之差. S(y) = Y - X
- 根据S(x) 来看, 如果从 数字和X里面, 拿出一个数字 m, 也就是 X = m + Xwithout(m)
- S(x) = m + Xwithout(m) - Y = m + (Xwithout(m) - Y). 
- 如果我们从全局里面索性去掉m, 那么 S(y'') = Y - Xwithout(m)
- 那么推算下来: S(x) = m + (Xwithout(m) - Y) = m - (Y - Xwithout(m)) = m - S(y'')
- 在这个问题里面, 我们model X 和 Y的时候, 其实都是 dp[i][j], 而区别在于先手/后手.
- 将公式套用, 某一个S(x) = a[i] - dp[i + 1][j],  也就是m=a[i], 而 S(y'') = dp[i + 1][j]

##### 注意
- 如果考虑计算先手[i, j]之间的最大值, 然后可能还需要两个数组, 最后用于比较先手和opponent的得分大小 => 那么就要多开维.
- 我们这里考虑的数字差, 刚好让人不需要计算先手的得分总值, 非常巧妙.
- Trick: 利用差值公式, 推导有点难想到.

##### 区间型动态规划
- 找出[i, j]区间内的性质: dp[i][j]下标表示区间范围 [i, j]
- 子问题: 砍头, 砍尾, 砍头砍尾
- loop应该基于区间的length
- template: 考虑len = 1, len = 2; 设定i的时候一定是 i <= n - len; 设定j的时候, j = len + i - 1;




---

**36. [Contains Duplicate.java](https://github.com/awangdev/LintCode/blob/master/Java/Contains%20Duplicate.java)**      Level: Easy
      

无序数组, 找是否有重复element, return true/false.

#### HashSet
- No brain: HashSet.
- Time O(n), Space O(n)

#### Sort, Binary Search
- Arrays.sort(x): Time O(nLogN), Space O(1)
- 排序后, 重复数会排在一起, 然后 binary search



---

**37. [Contains Duplicate II.java](https://github.com/awangdev/LintCode/blob/master/Java/Contains%20Duplicate%20II.java)**      Level: Easy
      

Unsorted array, 找出是否有duplicate elemenets: 必要条件是, 这两个element的index i,j 的大小最多相差k.

#### HashSet
- 很巧妙地根据k range地条件, 把HashSet里面的值控制在[i - k, i]
- 每次不断地往set里面加新元素, 从set里减去末尾index的元素
- 而set.add(x)如果遇到重复, 会return false.
- 一旦在这个length k 的 range里面, 有重复, 就符合条件. 
- Time O(n)

#### HashTable<value, List of duplicates>
- 记录每个element value的index in the list
- 一旦有重复element重复, 就把整个list of indexes 端出来, 查看有没有符合条件的: (index - i) <= k
- Time O(nm), m = # of duplicates

#### 这两种做法的区别很有艺术感觉
- 方法1是限定选拔的candidate, 不合格就去掉, 那么一旦有符合条件的(duplicates), 那么一定中, 剩下的就不看了.
- 方法2是把符合条件的index找出来, 集中处理, 但是所有candidate都会选出来
- 就好像招人一样: 一种是遇到好的就停止; 第二种是看过所有人, 从中选拔最好的. 显然第一种更快.




---

**38. [Jump Game.java](https://github.com/awangdev/LintCode/blob/master/Java/Jump%20Game.java)**      Level: Medium
      

给出步数，看能不能jump to end.

#### DP
- DP[i]: 在i点记录，i点之前的步数是否可以走到i点？ True of false.
- 其实j in [0~i)中间只需要一个能到达i 就好了
- Function: DP[i] = DP[j] && (A[j] >= i - j), for all j in [0 ~ i)
- Return: DP[dp.length - 1];
- It timesout, O(n^2)

#### Greedy
- Keep track of farest can go
- 一旦 farest >= nums.length - 1, 也就是到了头, 就可以停止, return true.
- 一旦 farest <= i, 也就是说, 在i点上, 已经走过了步数, 不能再往前跳, 于是 return false



---

**39. [Longest Continuous Increasing Subsequence.java](https://github.com/awangdev/LintCode/blob/master/Java/Longest%20Continuous%20Increasing%20Subsequence.java)**      Level: Easy
      

找连续的持续上升子序列的长度.

#### Coordinate DP
- 1D coordinate, dp 的角标, 就是代表 index i 的状态
- 求最值, dp[i] = 在index i位置的最长子序列
- 如果 nums[i] > nums[i - 1], dp[i] = dp[i - 1] + 1
- 如果没有持续上升, 那么dp[i] = 1, 重头来过
- maintain max

#### Basic
- 用一个数存current count,  maintain max



---

**40. [Minimum Path Sum.java](https://github.com/awangdev/LintCode/blob/master/Java/Minimum%20Path%20Sum.java)**      Level: Medium
      

#### DP
- Time, Space O(MN)
- 往右下角走, 计算最短的 path sum. 典型的坐标型.
- 注意: init 第一行的时候, 要accumulate dp[0][j - 1] + grid[i][j], 而不是单纯assign grid[i][j]

#### Rolling Array
- Time O(MN), Space O(1)
- 需要在同一个for loop里面完成initialization, 和使用dp[i][j]
- 原因: dp[i % 2][j] 在被计算出来的时候, 是几乎马上在下一轮是要被用的; 被覆盖前不备用,就白算
- 如果按照第一种方法, 在开始initialize dp, 看起来固然简单, 但是不方便空间优化



---

**41. [Best Time to Buy and Sell Stock I.java](https://github.com/awangdev/LintCode/blob/master/Java/Best%20Time%20to%20Buy%20and%20Sell%20Stock%20I.java)**      Level: Easy
      

给个array of stock prices, 限制能交易(买/买)一轮, 问如何找到最大profit.

#### 理解意思是关键
- 每天都就交易价格，n天只让买卖一次，那就找个最低价买进，找个最高价卖出
- 记录每天最小值Min是多少. O(n)
- 每天都算和当下的Min买卖，profit最大多少.

#### DP
- Find min value for first i items, new dp[n + 1].
- 然后用当天的price做减法算max profit.
- Time, Space: O(n)
- 更进一步, 用一个min来表示min[i], 因为计算中只需要当下的min.

#### Rolling array
- index i only depend on [i - 2]
- Space O(n)

#### Brutle Failed
- 每天都试着买进，然后之后的每一天尝试卖出. double for loop, O(n^2). timeout.
- 其中很多都是没必要的计算：[7, 1, 5, 3, 6, 4]。 if we know buyin with 1 is cheapest, we don't need to buyin at 5, 3, 6, 4 later on; we'll only sell on higher prices.



---

**42. [Best Time to Buy and Sell Stock II.java](https://github.com/awangdev/LintCode/blob/master/Java/Best%20Time%20to%20Buy%20and%20Sell%20Stock%20II.java)**      Level: Easy
      

和Stock I 的区别：可以买卖多次，求总和的最大盈利.

#### 几种其他不同的思路:
- Greedy, 每次有相邻的diff符合profit条件, 就卖了, 最后把所有的diff加在一起. 计算delta, 其实简单粗暴, 也还不错.
- 如下, 从低谷找peek, sell.
- DP. (old dp solution BuyOn[], SellOn[])
- DFS计算所有(timeout).Improvement on DFS -> DP -> calculate sellOn[i] and buyOn[i], and then return buyOn[i]. 有点难想, 但是代码简单, 也是O(n)

#### Greedy
- 画图, 因为可以无限买卖, 所以只要有上升, 就卖
- 所有卖掉的, 平移加起来, 其实就是overall best profit
- O(n)

#### 找涨幅最大的区间，买卖：
- 找到低谷，买进:peek = start + 1 时候，就是每次往前走一步;若没有上涨趋势，继续往低谷前进。
- 涨到峰顶，卖出:一旦有上涨趋势，进一个while loop，涨到底, 再加个profit.
- profit += prices[peek - 1] - prices[start]; 挺特别的。
- 当没有上涨趋势时候，peek-1也就是start, 所以这里刚好profit += 0.

#### DP
- 想知道前i天的最大profit, 那么用sequence DP
- 当天的是否能卖, 取决于昨天是否买进, 也就是昨天买了或者卖了的状态: 加状态, 2D DP
- 如果今天是卖的状态, 那么昨天: 要么买进了, 今天 +price 卖出; 要么昨天刚卖, 今天不可能再卖, profit等同.
- 如果今天是买的状态, 那么昨天: 要么卖掉了, 今天 -price 买入; 要么昨天刚卖, 今天不可能再买, profit等同.

#### Rolling Array
- [i] 和 [i - 1] 相关联, roll




---

**43. [Best Time to Buy and Sell Stock III .java](https://github.com/awangdev/LintCode/blob/master/Java/Best%20Time%20to%20Buy%20and%20Sell%20Stock%20III%20.java)**      Level: Hard
      

比stock II 多了一个限制：只有2次卖出机会.

#### DP加状态
- 只卖2次, 把买卖分割成5个状态模块.
- 在状态index 0, 2, 4: 没有持有股票. 1. 一直在此状态, max profit不变; 2. 刚卖掉, dp[i][前状态] + profit
- 在状态index 1, 3: 持有股票. 1. 一直在此状态, daily profit. 2. 刚刚买进, 状态改变, 但是没有profit yet: dp[i][前状态]

##### Partial profit
- 把每天的partial profit (diff)加在一起, 最终的overall profit是一样的. 唯一更好的是, 不需要记录中间买入的时间点.
- 什么时候会积累profit呢? 
- 1. 原本就持有股票的, 如果毫无动作, 那么状态不变, 积累profit diff. 
- 2. 卖出了股票, 状态改变, 积累profit diff.
- 注意: 只有在状态index: 0, 2, 4, 也就是卖掉股票的时候, 猜可以积累profit

##### Rolling Array
- [i] 只有和 [i-1] 打交道, reduce space
- O(1) space, O(n) time

#### 找峰头
- 找峰头；然后往下再找一个峰头。
- 怎么样在才能Optimize两次巅峰呢？从两边同时开始找Max！（棒棒的想法）
- leftProfit是从左往右，每个i点上的最大Profit。
- rightProfit是从i点开始到结尾，每个点上的最大profit.
- 那么在i点上，就是leftProfit，和右边rightProfit的分割点。在i点，leftProfit+rightProfit相加，找最大值。
- 三个O(n),还是O(n)



---

**44. [Jump Game II.java](https://github.com/awangdev/LintCode/blob/master/Java/Jump%20Game%20II.java)**      Level: Hard
      

给一串数字 是可以跳的距离. goal: 跳到最后的index 所可能用的最少次数.

#### DP 
- DP[i]: 在i点记录，走到i点上的最少jump次数
- dp[i] = Math.min(dp[i], dp[j] + 1);
- condition (j + nums[j] >= i)
- 注意使用 dp[i] = Integer.MAX_VALUE做起始值, 来找min

#### Previous Notes
- Greedy, 图解 http://www.cnblogs.com/lichen782/p/leetcode_Jump_Game_II.html
- 维护一个range, 是最远我们能走的. 
- index/i 是一步一步往前, 每次当 i <= range, 做一个while loop， 在其中找最远能到的地方 maxRange
- 然后更新 range = maxRange
- 其中step也是跟index是一样, 一步一步走.
- 最后check的condition是，我们最远你能走的range >= nums.length - 1, 说明以最少的Step就到达了重点。Good.



---

**45. [First Missing Positive.java](https://github.com/awangdev/LintCode/blob/master/Java/First%20Missing%20Positive.java)**      Level: Hard
      

给一串无序数字, 有负数: 找这个array里面第一个 missing的 positive integer

missing positive integer 其实是以 [1, n] 来做比较的.

#### Array分析, index 技巧
- 用while loop, 不断地尝试把 number 送到该放的地方
- 如果 index = nums[i] 超过了nums.length, 当然就不移动了
- 注意: 检查 val != nums[val], avoid infinitely loop
- 检验: nums[i] 是否等于 i, 如果不对, 就找到了结果

#### Edge Case
- 如果nums==null, 其实missing positive integer 自然而然是 1
- validation时, 有可能这串数字里没有断开的integer, 但是最大的integer在首位 (因为index超标, 无法被放到正确的地方)
- 这种时候, n被放在 index 0, 其实就是说, 下一个integer应该是 n + 1
- 最终, 如果array本来就是完全sorted, 也不缺, 还符合角标的条件, 那么唯一下一个就是array范围外的第一个positive number: n



---

**46. [Longest Increasing Continuous subsequence.java](https://github.com/awangdev/LintCode/blob/master/Java/Longest%20Increasing%20Continuous%20subsequence.java)**      Level: Easy
      

https://leetcode.com/problems/longest-continuous-increasing-subsequence/description/

O(n)跑2遍for.
O(1)是用了两个int来存：每次到i点时，i点满足条件或不满足条件所有的longestIncreasingContinuousSubsequence.
特点：返跑一回，ans还是继续和left轮的ans作比较；求的所有情况的最大值嘛。



---

**47. [Longest Increasing Continuous subsequence II.java](https://github.com/awangdev/LintCode/blob/master/Java/Longest%20Increasing%20Continuous%20subsequence%20II.java)**      Level: Medium
      

#### Coordinate DP
- due to access permission, not test
- dp[i][j]: longest continuous subsequence length at coordinate (i, j)
- dp[i][j] should come from (i-1,j) and (i, j-1).
- dp[0][0] = 1
- condition: from up/left, must be increasing
- return dp[m-1][n-1]

#### Memoization
- O(mn) space for dp and flag.
- O(mn) runtime because each spot will be marked once visited. 
- 这个题目的简单版本一个array的例子：从简单题目开始想DP会简单一点。每个位置，都是从其他位置（上下左右）来的dpValue +　１.　如果啥也没有的时候，init state 其实都是1， 就一个数字，不增不减嘛。




---

**48. [Maximum Subarray.java](https://github.com/awangdev/LintCode/blob/master/Java/Maximum%20Subarray.java)**      Level: Easy
      

给一串数组, 找数组中间 subarray 数字之和的最大值

#### Sequence DP
- dp[i]: 前i个element, 包括element i 在内的 continous subsequence 的最大sum是多少?
- 因为continous sequence, 所以不满足条件的时候, 会断: track overall max,
- init dp[0] = 0; max = MIN_VALUE 因为有负数
- Time, space O(n)
- Rolling array, space O(1)

#### Divide and Conquer
- 找一个mid piont, 考虑3种情况: 只要左边, 只要右边, cross-mid
- left/rigth 的case, 直接 dfs
- corss-mid case: continuous sum max from left + continous sum max from right + mid
- continuous sum max from one direction:


---

**49. [Maximum Subarray II.java](https://github.com/awangdev/LintCode/blob/master/Java/Maximum%20Subarray%20II.java)**      Level: Medium
      

给一串数组, 找数组中间 两个不交互的 subarray 数字之和的最大值

#### DP
- 考虑两个方向的dp[i]: 包括i在内的subarray max sum. 
- dp[i] 的特点是: 如果上一个 dp[i - 1] + nums[i - 1] 小于 nums[i-1], 那么就舍弃之前, 从头再来:
- dp[i] = Math.max(dp[i - 1] + nums.get(i - 1), nums.get(i - 1));
- 缺点: 无法track全局max, 需要记录max.
- 因为我们现在要考虑从左边/右边来的所有max, 所以要记录maxLeft[] 和 maxRight[] 
- maxLeft[i]: 前i个元素的最大sum是多少 (不断递增); maxRight反之, 从右边向左边
- 最后比较maxLeft[i] + maxRight[i] 最大值
- Space, Time O(n)
- Rolling array, reduce some space, but can not reduce maxLeft/maxRight

#### preSum, minPreSum
- preSum是[0, i] 每个数字一次加起来的值
- 如果维持一个minPreSum, 就是记录[0, i]sum的最小值(因为有可能有负数)
- preSum - minPreSum 就是在 [0, i]里, subarray的最大sum值
- 把这个最大subarray sum 记录在array, left[] 里面
- right[] 是一样的道理
- enumerate一下元素的排列顺位, 最后 max = Math.max(max, left[i] + right[i + 1])



---

**50. [Median.java](https://github.com/awangdev/LintCode/blob/master/Java/Median.java)**      Level: Easy
      

给一串无序数组, 找到median(sort之后 位置在中间的数字).

#### Quick Select
- 与quickSort不同在于, 每次只要在一半list里面recurring, 所以把O(logn)的时间复杂度降到O(n)
- quickSelect 可以找到 kth 最小的元素
- 利用这个原理, 找这个kth最小值, 然后如果 == target index, 就找到了我们的median
- quick select 的template要熟悉一下, 一下子可能想得到, 但写不出来
- 主要步骤: partition, dfs, only recur on one part of the array 



---

**51. [Merge Sorted Array.java](https://github.com/awangdev/LintCode/blob/master/Java/Merge%20Sorted%20Array.java)**      Level: Easy
      

给两个排好序的数组, merge. 其中一个数组nums1有多余的位置

#### Basics
- A够长，那么可以从A的尾部开始加新元素。     
- 注意，从尾部，是大数字优先排末尾的.  



---

**52. [Merge Intervals.java](https://github.com/awangdev/LintCode/blob/master/Java/Merge%20Intervals.java)**      Level: Medium
      

给一串int[Interval]. 把所以Interval merge起来.

#### Sweep Line
- O(nlogn)         
- 扫描线+Count无敌手。注意start end把interval给合起来。   
- count==0的时候，就是每次start end双数抵消的时候，就应该是一个interval的开头/结尾。写个例子就知道了。   
- 空间：O(2n) -> O(n)   
- 时间,priorityqueue: O(nlogn)   
- 记得怎么写comparator. New way: new PriorityQueue<>(Comparator.comparing(p -> p.val));
- 在 LeetCode里面，Sweep Line比方法2要快很多.

#### Sort Interval 
- Collections.sort() on interval.start之后，试着跑一遍，按照merge的需求，把需要merge的地方续好，然后减掉多余的interval就好。
- (不知为何LeetCode把Merge Interval, Insert Interval 标为Hard)
- Collections.sort(..., new comparator): sort by Interval.start.

- 画两个相连的Interval， prev, curr:
- prev只有 prev.end覆盖了 curr.start， 才需要merge. 那么比较一下, marege.     
- 记得如果merge, 一定要list.remove(i), 并且i--， 因为改变了List的大小。
- 若没有重合，就继续iteration: prev = curr. move on.

#### Sort Intervals and append end logically
- Sort intervals: O(nlogn)
- 找到结尾 interval, 满足条件就可以save
- 如果不到return的条件, 就继续延伸 interval.end



---

**53. [Missing Number.java](https://github.com/awangdev/LintCode/blob/master/Java/Missing%20Number.java)**      Level: Easy
      

给一串unique数字, 数字取自 [0 ~ n], 无序, 找第一个skipped的数字.

#### Swap 
- 跟First Missing Positive 非常像, 只有一行代码的区别.
- swap 所有的数字, 到自己的correct position
- 最后一个for loop找到错位的index, 也就是缺的数字.

#### Bit Manipulation
- XOR will only retain bits that are different 1 ^ 0 = 1, but 0^0, 1^1 == 0
- Use that feature, 把所有value都和index XOR了
- 剩下的多余的数字, 其实是那个index无法被XOR消掉, 也就是那个缺的number value.
- 注意: 题目告诉数字是 [0 ~ n], 然而缺一个数字, 那么在[0 ~ n - 1] 里面, 最大的数字(不管缺没缺), 一定是 n = nums.length.

#### HastSet
- 全存, 找missing
- O(n) space, 不合题意

#### sorting
- sort, 找1st missing
- O(n log n) 太慢, 不合题意



---

**54. [Remove Duplicates from Sorted Array.java](https://github.com/awangdev/LintCode/blob/master/Java/Remove%20Duplicates%20from%20Sorted%20Array.java)**      Level: Easy
      

给一个sorted array, 把重复的去掉: 也就是把不重复的按照顺序贴上来, array末尾多余的位置无所谓.

return unique item 的长度.

#### Two Pointers
- sorted array, 重复元素都在一起
- Two pointers 其实也可以是一个 for loop pointer, 另一个 dynamic variable.
- track unique index
- skip duplicated items
- O(n)

#### 思考模式:
- Remove Duplicate from Array 不同于remove from linked list.
- LinkedList里面我们是最好不要动node.val的，直接把node去掉。
- 而array我们很难直接把node去掉，又不能用新array，那么就要：
- 把不重复的element一个个放到最前面。
- 这个思想跟merge two sorted array （其中一个后续非常长的array可以放下arr1,arr2） 类似。
- 就是找个不会事后mess up，不会去动得index,把满足条件的element 填进去。这样保证了in place.
- *反向思维*：remove duplicate, 实际上也是找unique elements, and insert into original array



---

**55. [Remove Duplicates from Sorted Array II.java](https://github.com/awangdev/LintCode/blob/master/Java/Remove%20Duplicates%20from%20Sorted%20Array%20II.java)**      Level: Medium
      

给一个sorted array, 把重复的去掉: 也就是把不重复的按照顺序贴上来, array末尾多余的位置无所谓.

最多可重复出元素的数量不超过2个. return unique item 的长度.

#### Two Pointers
- sorted array, 重复元素都在一起
- 跟 `Remove Duplicates from Sorted Array` 几乎一模一样, 只不过unique index现在可以 validate 2 位
- 其余一模一样, use index to track unique item; skip if duplicated for more than 2 times
- O(n) time, O(1) space
- 这里也可以真的用2个pointers 写while loop, 但是没有必要, 只是单纯地走一个for loop其实就足够.



---

**56. [Anagrams.java](https://github.com/awangdev/LintCode/blob/master/Java/Anagrams.java)**      Level: Medium
      

把anagram找到并output

#### HashMap
- 存在int[26], Arrays.toString(arr) 就是 string key
- anagram都有一样的key, 存进hashmap<string, list of anagrams>
- output anagrams

#### HashMap + Sort
- HashMap 的做法. sort每个string, 存进HashMap, 重复的就是anagrams,最后输出。   
- toCharArray
- Arrays.sort
- Stirng.valueOf(char[])
- 时间n*L*O(logL),L是最长string的长度。

#### Previous Notes
- Arrays.toString(arr)的做法。arr是int[26], assuming only have 26 lowercase letters.    
- Count occurrance, 然后convert to String，作为map的key.
- Time complexity: nO(L)
- 另一种做法：http://www.jiuzhang.com/solutions/anagrams/   
- 1. take each string, count the occurrance of the 26 letters. save in int[]count.   
- 2. hash the int[] count and output a unique hash value; hash = hash * a + num; a = a * b.   
- 3. save to hashmap in the same way as we do. 
- 这一步把for s: strs 里面的时间复杂度降到了O(L). L = s.length().   
- Need to work on the getHash() function.
- 时间变成n*O(L). Better.




---

**57. [Combination Sum.java](https://github.com/awangdev/LintCode/blob/master/Java/Combination%20Sum.java)**      Level: Medium
      

给一串数字candidates (no duplicates), 和一个target. 

找到所有unique的 组合(combination) int[], 要求每个combination的和 = target.

注意: 同一个candidate integer, 可以用任意多次.


#### DFS, Backtracking
- 考虑input: 没有duplicate, 不需要sort
- 考虑重复使用的规则: 可以重复使用, 那么for loop里面dfs的时候, 使用curr index
- the result is trivial, save success list into result.

##### Combination DFS 思想
- 在每个index上面都要面临: pick/not pick的选择
- 每次pick以后, 就生成一条新的routine, from this index
- 下一个level的dfs从这个index开始, 对后面(或者当下/if allow index reuse) 进行同样的 pick/not pick 的选择
- 注意1: 每个level dfs 里面, for loop 里会有 end condition: 就不必要dfs下去了.
- 注意2: Backtracking在success case && dfs case 后都要做, 因为backtrack 是为了之前上一层dfs.




---

**58. [Combination Sum II.java](https://github.com/awangdev/LintCode/blob/master/Java/Combination%20Sum%20II.java)**      Level: Medium
      

给一串数字candidates (can have duplicates), 和一个target. 

找到所有unique的 组合(combination) int[], 要求每个combination的和 = target.

注意: 同一个candidate integer, 只可以用一次.

#### DFS, Backtracking
- when the input has duplicates, and want to skip redundant items? 
- 1. sort. 2. in for loop, skip same neighbor.
- 考虑input: 有duplicate, 必须sort
- 考虑重复使用的规则: 不可以重复使用
- 1. for loop里面dfs的时候, 使用curr index + 1
- 2. for loop里面, 同一个level, 同一个数字, 不能重复使用: `(i > index && candidates[i] == candidates[i - 1]) continue`
- 因为在同一个level里面重复的数字在下一个dfs level里面是会被考虑到的, 这里必须skip (这个就记住吧)
- the result is trivial, save success list into result.




---

**59. [Combination Sum III.java](https://github.com/awangdev/LintCode/blob/master/Java/Combination%20Sum%20III.java)**      Level: Medium
      

给一个integer k, 和一个target n. 

从positive数字[1 ~ 9], 找到所有unique的 组合(combination) int[], size = k, 要求每个combination的和 = n.

(隐藏条件, 需要clarify): 同一个candidate integer [1 ~ 9], 只可以用一次.

#### DFS, Backtracking
- 跟Combination Sum I, II 没什么太大区别, 只不过, 一定要用k个数字, 也就是一个for loop里面的特别条件
- 考虑input: 没有重复数字 [1 ~ 9]
- 考虑candidate重复利用: 不可以重复利用, next level dfs 时候, curr index + 1
- the result is trivial, save success list into result.



---

**60. [Combination Sum IV.java](https://github.com/awangdev/LintCode/blob/master/Java/Combination%20Sum%20IV.java)**      Level: Medium
      

给一串数字candidates (no duplicates), 和一个target. 

找到所有unique的 组合(combination) int[], 要求每个combination的和 = target.

注意: 同一个candidate integer, 可以用任意多次.

#### Backpack DP
- 计数问题, 可以想到DP. 其实就是Backpack VI.
- 从x个数字里面找candidate(可以重复用同一个数字), 来sum up to target. 找: # of ways to form the sequence.
- Backpack VI: 给一个数组nums, 全正数, 无重复数字; 找: # of 拼出m的方法
- dp[i]: # of ways to build up to target i
- consider last step: 如果上一步取的是 candidate A, 那么就该加到dp[i]:
- dp[i] += dp[i - A]
- 要找overall dp[i], 就做一个for loop: dp[i] = sum{dp[i - num]}, where for (num: nums)
- Time: O(mn). m = size of nums, n = target
- If we optimize dp for loop, 需要Sort nums. O(mlogm). will efficient 如果m是constant或者relatively small. Overall: O(n)

#### DFS, backtracking
- 尽管思考方式是对的, 但是 times out
- 可以重复使用数字的时候, 比如用1 来拼出 999, 这里用1就可以走999 dfs level, 不efficient



---

**61. [Subset.java](https://github.com/awangdev/LintCode/blob/master/Java/Subset.java)**      Level: Medium
      

给一串unique integers, 找到所有可能的subset. result里面不能有重复.

#### DFS
- dfs的两种路子: 1. pick&&skip dfs, 2. for loop dfs
- 1. pick&&skip dfs: 取或者不取 + backtracking. 当level/index到底，return 一个list.
- 2. for loop dfs: for loop + backtracking. 记得：做subset的时候, 每个dfs recursive call是一种独特可能，先加进rst。
- Time&&space: subset means independent choice of either pick&&not pick. You pick n times: O(2^n), 3ms

#### Bit Manipulation
- n = nums.length, 那么在每一个index, 都是 pick / not pick: 0/1
- 考虑subset index 0/1的bit map: range 的就是 [0000...00 ~ 2^n-1]
- 每一个bitmap就能展现出一个subset的内容: all the 1 represents picked indexes
- 做法:
- 1. 找出Range
- 2. 遍历每一个bitmap candidate
- 3. 对每一个integer 的 bit representation 遍历, 如果是1, add to list
- time: O(2^n * 2^n) = O(4^n), still 3ms, fast.

#### Iterative, BFS
- Regular BFS, 注意考虑如果让one level to generate next level
- 1. 用queue来存每一次的candidate indexes
- 2. 每一次打开一层candiates, add them all to result
- 3. 并且用每一轮的candidates, populate next level, back into queue.
- should be same O(2^n), but actual run time 7ms, slower





---

**62. [Subsets II.java](https://github.com/awangdev/LintCode/blob/master/Java/Subsets%20II.java)**      Level: Medium
      

给一串integers(may have duplicates), 找到所有可能的subset. result里面不能有重复.

#### DFS
- DFS, 找准需要pass along的几个数据结构. 先sort input, 然后DFS
- Using for loop approach: 每个dfs call是一种可能性，直接add into result.     
- 为了除去duplicated result, skip used item at current level: `if (i > depth && nums[i] == nums[i - 1]) continue;`
- srot O(nlogn), subset: O(2^n)

#### BFS
- Regular BFS, 注意考虑如果让one level to generate next level
- skip duplicate: `if (i > endIndex && nums[i] == nums[i - 1]) continue;`
- 1. 用queue来存每一次的candidate indexes
- 2. 每一次打开一层candiates, add them all to result
- 3. 并且用每一轮的candidates, populate next level, back into queue.
- srot O(nlogn), subset: O(2^n)
- should be same O(2^n). slower than dfs

#### Previous notes:
- 在DFS种skip duplicate candidates, 基于sorted array的技巧：    
- 一旦for loop里面的i!=index，并且nums[i] == nums[i-1],
- 说明x=nums[i-1]已经在curr level 用过，不需要再用一次: [a,x1,x2]，x1==x2    
- i == index -> [a,x1]    
- i == index + 1 -> [a,x2]. 我们要skip这一种
- 如果需要[a,x1,x2]怎么办？ 其实这一种在index变化时，会在不同的两个dfs call 里面涉及到。

#### 注意
- 不能去用result.contains(), 这本身非常costly O(nlogn)




---

**63. [Longest Consecutive Sequence.java](https://github.com/awangdev/LintCode/blob/master/Java/Longest%20Consecutive%20Sequence.java)**      Level: Hard
      

给一串数字, unsorted, 找这串数字里面的连续元素序列长度 (consecutive序列, 是数字连续, 并不是说要按照原order)

#### HashSet
- 要想看连续元素, 必须要num++, num--这样搜索
- 1. 需要O(1)找到元素
- 2. 需要简单快速找到 num - 1, num + 1.
- 如果用min,max开array, 耗费空间
- 用HashSet来存, 用set.contains() 来查找 num - 1, num + 1 存在与否
- for loop. O(n) 
- 里面的while loop 一般不会有O(n); 一旦O(n), 也意味着set 清零, for loop也不会有更多 inner while 的衍生.
- overall O(n) 时间复杂度


#### Union Find
- 最终是要把相连的元素算一下总长, 其实也就是把元素group起来, 相连的group在一起, 于是想到UnionFind
- 这里用到了一个`int[] size` 来帮助处理 `合并的时候parent是哪个`的问题: 永远往group大的union里去
- main function 里面, 有一个map来track, 每个元素, 只处理1遍.
- union的内容: current number - 1, current number + 1
- https://www.jianshu.com/p/e6b955ca208f

##### 特点
- Union Find 在index上做好像更加容易
- 其他union find function: `boolean connected(a,b){return find(a) == find(b)}`



---




 
 
 
## Memoization (10)
**0. [Coin Change.java](https://github.com/awangdev/LintCode/blob/master/Java/Coin%20Change.java)**      Level: Medium
      

给一串不同数额的coins, 和total amount to spent. 求 最少 用多少个coin可以组合到这个amount. 每种coins个数不限量.

#### DP
- 找对方程dp[x], 积累到amount x最少用多少个coin: #coin是value, index是 [0~x].
- 子问题的关系是: 如果用了一个coin, 那么就应该是f[x - coinValue]那个位置的#coins + 1

##### initialization
- 处理边界, 一开始0index的时候, 用value0. 
- 中间利用Integer.MAX_VALUE来作比较, initialize dp[x]
- 注意, 一旦 Integer.MAX_VALUE + 1 就会变成负数. 这种情况会在coin=0的时候发生.

##### Optimization
- 方法1: 直接用Integer.MAX_VALUE
- 方法2: 用-1, 稍微简洁一点, 每次比较dp[i]和 dp[i - coin] + 1, 然后save. 不必要做多次min比较.

#### Memoization
- dp[i] 依然表示: min # of coints to make amount i
- initialize dp[i] = Integer.MAX_VALUE
- 先选最后一步(遍历coins),  然后dfs做同样的操作
- 记录dp[amount] 如果已经给过value, 不要重复计算, 直接return.
- 但是这道题没必要强行做memoization, 普通DP的状态和方程相对来说很好找到



---

**1. [Longest Increasing Subsequence.java](https://github.com/awangdev/LintCode/blob/master/Java/Longest%20Increasing%20Subsequence.java)**      Level: Medium
      

无序数组, 找最长的上升(不需要连续)数组 的长度. 先做O(n^2), 然后可否O(nLogN)?

#### DP, double for loop, O(n^2)
- 考虑nums[i]结尾的时候, 在[0, i) 里count有多少小于nums[i]
- 对于所有 i in [0, n), 最常的increasing序列有多少length?
- max需要在全局维护: nums是无序的, nums[i]也可能是一个很小的值, 所以末尾dp[i]并不是全局的max, 而只是对于nums[i]的max.
- 正因此, 每个nums[i]都要和每个nums[j] 作比较, j < i.
- dp[i] = Maht.max(dp[i], dp[j] + 1); j = [0 , i - 1]
- 时间复杂度  O(n^2)


#### O(nLogN)
- 维持一个list of increasing sequence
- 这个list其实是一个base-line, 记录着最低的increasing sequence.
- 当我们go through all nums的时候, 如果刚好都是上升, 直接append
- 如果不上升, 应该去list里面, 找到最小的那个刚好大于new num的数字, 把它换成num
- 这样就完成了baseline. 举个例子, 比如替换的刚好是在list最后一个element, 等于就是把peak下降了, 那么后面其他的数字就可能继续上升.
- '维护baseline就是一个递增的数列' 的证明, 还没有仔细想.



---

**2. [Longest Palindromic Subsequence.java](https://github.com/awangdev/LintCode/blob/master/Java/Longest%20Palindromic%20Subsequence.java)**      Level: Medium
      

#### Interval DP
- 用[i][j]表示区间的首尾
- 考虑3个情况: 砍头, 砍尾, 砍头并砍尾 (考虑首尾关系)
- Iteration一定是以i ~ j 之间的len来看的. 
- len = j - i + 1; 那么反推, 如果len已知, j = len + i -1;
- 注意考虑len == 1, len == 2是的特殊情况.

#### Memoization
- 同样的方式model dp[i][j]: range [i, j] 之间的  max palindromic length
- 三种情况: 
- 1. 首尾match 继而 dfs[i+1, j-1]
- 2. 首尾不match,dfs[i+1,j] 
- 3. 首尾不match,dfs[i,j-1] 
- 注意: init dp[i][j]=-1, dfs的时候查dp[i][j] 是否算过



---

**3. [Longest Increasing Path in a Matrix.java](https://github.com/awangdev/LintCode/blob/master/Java/Longest%20Increasing%20Path%20in%20a%20Matrix.java)**      Level: Hard
      

m x n 的matrix, 找最长增序的序列长度. 这里默认连续的序列.

- 接成圈是不行的, 所以visit过得 (x,y)就不能再去了.
- 斜角方向不能走, 只能走上下左右
- 无法按照坐标DP来做, 因为计算顺序4个方向都可以走.
- 最终要visit所有node, 所以用DFS搜索比较合适.

#### DFS, Memoization
- DFS太多重复计算; memoization (dp[][], visited[][]) 省去了重复计算
- initialize dp[x][y] = 1, (x,y) 自己也算path里的一格
- dfs(matrix, x, y): 每次检查(x,y)的4个neighbor (nx, ny), 如果他们到(x,y)是递增, 那么就考虑和比较:
- Maht.max(dp[x][y], dp[nx][ny] + 1); where dp[n][ny] = dfs(matrix, nx, ny)
- top level: O(mn), 尝试从每一个 (x,y) 出发
- O(m * n * k), where k is the longest path

#### Topological sort
还没有做



---

**4. [Coins in a Line II.java](https://github.com/awangdev/LintCode/blob/master/Java/Coins%20in%20a%20Line%20II.java)**      Level: Medium
      

给一串coins, 用values[]表示; 每个coin有自己的value. 先手/后手博弈,
每次只能 按照从左到右的顺序, 拿1个或者2个棋子, 最后看谁拿的总值最大.

MiniMax的思考方法很神奇, 最后写出来的表达式很简单

#### DP, Game Theory 自考过程比较长
- 跟Coins in a line I 不一样: 每个coin的value不同.
- 用到MiniMax的思想, 这里其实是MaxiMin. Reference: http://www.cnblogs.com/grandyang/p/5864323.html
- Goal: 使得player拿到的coins value 最大化.
- 设定dp[i]: 从index i 到 index n的最大值. 所以dp[0]就是我们先手在[0 ~ n]的最大取值 
- 于此同时, 你的对手playerB也想最大化, 而你的选择又不得不被对手的选择所牵制.
- 用MaxiMin的思想, 我们假设一个当下的状态, 假想对手playerB会做什么反应(从对手角度, 如何让我输)
- 在劣势中(对手让我输的目标下)找到最大的coins value sum


##### 推算表达式
- Reference里面详细介绍了表达式如何推到出来, 简而言之:
- 如果我选了i, 那么对手就只能选(i+1), (i+2) 两个位置, 而我在对方掌控时的局面就是min(dp[i+2], dp[i+3])
- 如果我选了i和(i+1), 那么对手就只能选(i+2), (i+3) 两个位置, 而我在对方掌控时的局面就是min(dp[i+3], dp[i+4])
- 大家都是可选1个或者2个coins
- 目标是maximize上面两个最坏情况中的最好结果

##### 简化表达式
- 更加简化一点: 如果我是先手, dp[i]代表我的最大值.
- 取决于我拿了[i], 还是[i] + [i+1], 对手可能是dp[i + 1], 或者是dp[i+2]
- 其实dp[i] = Math.max(sum - dp[i + 1], sum - dp[i + 2]);
- 这里的sum[i] = [i ~ n] 的sum, 减去dp[i+1], 剩下就是dp[i]的值没错了

##### Initialization
- 这个做法是从最后往前推的, 注意initialize dp末尾的值.
- dp = new int[n + 1]; dp[n] = 0; // [n ~ n]啥也不选的时候, 为0.
- sum = new int[n + 1]; sum[n] = 0; // 啥也不选的时候, 自然等于0
- 然后记得initialize (n-1), (n-2)

##### 时间/空间
Time O(n)
Space O(n): dp[], sum[]



---

**5. [Climbing Stairs.java](https://github.com/awangdev/LintCode/blob/master/Java/Climbing%20Stairs.java)**      Level: Easy
      

#### Recursive + Memoization
- 递归很好写, 但是重复计算, timeout. time: O(2^n)
- O(2^n): each n can spawn 2 dfs child, at next level, it will keep spawn. Total 2^n nodes will spawn.
- 用全局变量int[] memo 帮助减少重复计算
- O(n) time, space

#### DP
- 最后一步被前两种走法决定: dp[i] = dp[i - 1] + dp[i - 2]
- 基础sequence DP, int[] dp = int[n + 1];
- DP[]存的是以 1-based index的状态
- 需要知道dp[n] 的状态, 但是最大坐标是[n-1], 所以int[n+1]
- dp[0]往往是有特殊状态的
- O(n) space, time

#### 序列DP, 滚动数组
- [i] only associates with [i-2], [i-1].
- %2
- O(1) space



---

**6. [Coins in a Line III.java](https://github.com/awangdev/LintCode/blob/master/Java/Coins%20in%20a%20Line%20III.java)**      Level: Hard
      

还是2个人拿n个coin, coin可以有不同的value. 

只不过这次选手可以从任意的一头拿, 而不限制从一头拿. 算先手会不会赢?

#### Memoization + Search
- 跟Coins in a Line II 一样, MaxiMin的思想: 找到我的劣势中的最大值
- dp[i][j] 代表在[i,j]区间上 选手最多能取的value 总和
- 同样, sum[i][j]表示[i] 到 [j]间的value总和
- 对手的最差情况, 也就是先手的最好情况:
- dp[i][j] = sum[i][j] - Math.min(dp[i][j - 1], dp[i + 1][j]);
- 这里需要search, 画出tree可以看明白是如何根据取前后而分段的.

#### 博弈 + 区间DP
- 因为是看区间[i,j]的情况, 所以可以想到是区间 DP
- 这个方法需要复习, 跟数学表达式的推断相关联: S(x) = - S(y) + m. 参考下面的公式推导.
- dp[i][j]表示 从index(i) 到 index(j), 先手可以拿到的最大值与对手的数字差. 也就是S(x).
- 其中一个S(x) = dp[i][j] = a[i] - dp[i + 1][j]
- m 取在开头, m 取在末尾的两种情况:
- dp[i][j] = max{a[i] - dp[i + 1][j], a[j] - dp[i][j - 1]}
- len = 1, 积分就是values[i]
- 最后判断 dp[0][n] >= 0, 最大数字和之差大于0, 就赢.
- 时间/空间 O(n^2)

##### 公式推导
- S(x) = X - Y, 找最大数字和之差, 这里X和Y是选手X的总分, 选手Y的总分. 
- 对于选手X而言: 如果S(x)最大值大于0, 就是赢了; 如果最大值都小于0, 就一定是输了. 
- 选手Y: S(y)来表示 对于Y,  最大数字和之差. S(y) = Y - X
- 根据S(x) 来看, 如果从 数字和X里面, 拿出一个数字 m, 也就是 X = m + Xwithout(m)
- S(x) = m + Xwithout(m) - Y = m + (Xwithout(m) - Y). 
- 如果我们从全局里面索性去掉m, 那么 S(y'') = Y - Xwithout(m)
- 那么推算下来: S(x) = m + (Xwithout(m) - Y) = m - (Y - Xwithout(m)) = m - S(y'')
- 在这个问题里面, 我们model X 和 Y的时候, 其实都是 dp[i][j], 而区别在于先手/后手.
- 将公式套用, 某一个S(x) = a[i] - dp[i + 1][j],  也就是m=a[i], 而 S(y'') = dp[i + 1][j]

##### 注意
- 如果考虑计算先手[i, j]之间的最大值, 然后可能还需要两个数组, 最后用于比较先手和opponent的得分大小 => 那么就要多开维.
- 我们这里考虑的数字差, 刚好让人不需要计算先手的得分总值, 非常巧妙.
- Trick: 利用差值公式, 推导有点难想到.

##### 区间型动态规划
- 找出[i, j]区间内的性质: dp[i][j]下标表示区间范围 [i, j]
- 子问题: 砍头, 砍尾, 砍头砍尾
- loop应该基于区间的length
- template: 考虑len = 1, len = 2; 设定i的时候一定是 i <= n - len; 设定j的时候, j = len + i - 1;




---

**7. [Burst Balloons.java](https://github.com/awangdev/LintCode/blob/master/Java/Burst%20Balloons.java)**      Level: Hard
      

一排球, 每个球有value, 每次扎破一个, 就会积分: 左*中间*右 的值. 求, 怎么扎, 最大值?

TODO: Need more thoughts on why using dp[n + 2][n + 2] for memoization, but dp[n][n] for interval DP.

#### Interval DP
- 因为数组规律会变, 所以很难找'第一个burst的球'. 反之, 想哪一个是最后burst?
- 最后burst的那个变成一堵墙: 分开两边, 分开考虑, 加法原理; 最后再把中间的加上.
- dp[i][j] represent max value on range [i, j)
- Need to calculate dp[i][j] incrementally, starting from range size == 3 ---> n
- Use k to divide the range [i, j) and conquer each side.

##### Interval DP 三把斧:
- 中间劈开
- 砍断首或尾
- Range区间作为iteration的根本

##### Print the calculation process
- use pi[i][j] and print recursively.
- Print k, using pi[i][j]: max value taken at k

#### Memoization
- 其实会做之后挺好想的一个DP
- dp[i][j] =  balloons i~j 之间的 max. 
- 然后找哪个点开始burst? 设为x。
- For loop 所有的点作为x， 去burst。
- 每次burst都切成了三份：左边可以recusive 求左边剩下的部分的最大值 + 中间3项相乘 + 右边递归下去求最大值。
- Note: 这个是Memoization, 而不纯是DP
- 因为recursive了，其实还是搜索，但是memorize了求过的值，节省了Processing




---

**8. [Longest Increasing Continuous subsequence II.java](https://github.com/awangdev/LintCode/blob/master/Java/Longest%20Increasing%20Continuous%20subsequence%20II.java)**      Level: Medium
      

#### Coordinate DP
- due to access permission, not test
- dp[i][j]: longest continuous subsequence length at coordinate (i, j)
- dp[i][j] should come from (i-1,j) and (i, j-1).
- dp[0][0] = 1
- condition: from up/left, must be increasing
- return dp[m-1][n-1]

#### Memoization
- O(mn) space for dp and flag.
- O(mn) runtime because each spot will be marked once visited. 
- 这个题目的简单版本一个array的例子：从简单题目开始想DP会简单一点。每个位置，都是从其他位置（上下左右）来的dpValue +　１.　如果啥也没有的时候，init state 其实都是1， 就一个数字，不增不减嘛。




---

**9. [Fibonacci.java](https://github.com/awangdev/LintCode/blob/master/Java/Fibonacci.java)**      Level: Easy
      

#### Memoization
- fib[n] = fibonacci(n - 1) + fibonacci(n - 2);

#### DP array.
- 滚动数组, 简化DP

#### recursively calculate
- recursively calculate fib(n - 1) + fib(n - 2). 公式没问题, 但是时间太长, timeout.




---




 
 
 
## Two Stacks (1)
**0. [Binary Tree Postorder Traversal.java](https://github.com/awangdev/LintCode/blob/master/Java/Binary%20Tree%20Postorder%20Traversal.java)**      Level: Medium
      

如题, POST-ORDER traversal.

LeetCode给了hard, 应该是觉得stack的做法比较难想到.

#### Recursive
trivial, 先加left recursively, 再加right recursively, 然后组成头部.

#### Stack
- 双stack的思想, 需要在图纸上画一画
- 原本需要的顺序是: 先leftChild, rightChild, currNode.
- 营造一个stack, reversely process: 先currNode, 再rightChild, 再leftChild
- 这样出来的结果是reverse的, 那么翻转一下就可以了.
- v1做的时候用了stack1, stack2, 因为根据这个双stack的思想而来
- v2简化, 可以放在一个stack里面, 每次record result 的时候: rst.add(0, item);

##### 利用stack的特点
- 每次加element进stack的时候, 想要在 bottom/后process的, 先加
- 想要下一轮立刻process的, 最后push进stack.

##### 注意
这些binary tree traversal的题目.常常有多个做法:recursive or iterative



---




 
 
 
## backtracking (1)
**0. [Flip Game II.java](https://github.com/awangdev/LintCode/blob/master/Java/Flip%20Game%20II.java)**      Level: Review
      

String 只包含 + , - 两个符号. 两个人轮流把consecutive连续的`++`, 翻转成 `--`.

如果其中一个人再无法翻转了, 另一个人就赢. 求: 给出string, 先手是否能赢.

#### Backtracking
- curr player 每走一步, 就生成一种新的局面, dfs on this
- 等到dfs结束, 不论成功与否, 都要backtracking
- curr level: 把"++" 改成 "--"; backtrack的时候, 改回 '--'
- 换成boolean[] 比 string/stringBuilder要快很多, 因为不需要重新生成string.
- ++ 可以走 (n - 1)个位置: 
- T(N) = T(1) + T(2) + T(3) + ... + T(N-2) + T(N - 1)
- => T(N) = 2T(N-1) = 2 * 2 * T(N - 2) = ... = (2^n)T(1) = O(2 ^ n)

##### iterate based on "++"
- 做一个String s的 replica: string or stringBuilder
- 每次dfs后, 然后更替里面的字符 "+" => "-"
- 目的只是Mark已经用过的index
- 真正的dfs 还是在 original input string s 身上展开
- 每次都重新生成substring, 并不是很efficient

##### Game theory
- 保证p1能胜利，就必须保持所有p2的move都不能赢
- 或者说, 在知道棋的所有情况时, 只要p2有一种路子会输, p1就一定能走对路能赢.
- 同时，p1只要在可走的Move里面，有一个move可以赢就足够了。
- p1: player1, p2: player2

#### O(N^2) 的 DP
- 需要Game Theory的功底, Nim game. https://www.jiuzhang.com/qa/941/
- http://www.1point3acres.com/bbs/thread-137953-1-1.html



---




