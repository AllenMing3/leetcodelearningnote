#### 题目
For two strings s and t, we say "t divides s" if and only if s = t + ... + t (i.e., t is concatenated with itself one or more times).

Given two strings str1 and str2, return the largest string x such that x divides both str1 and str2.

来源：力扣（LeetCode）
链接：https://leetcode.cn/problems/greatest-common-divisor-of-strings

#### 思路：
首先这个题目寻找的是最小公因字符串，如果存在此字符串，那么 str1 和 str2 都是由n个最小子字符串构成的，就会满足一个特性，**str1+str2 == str2 + str1**。
可以用 math.gcd(a,b) 的方法先算出最小字串的长度，然后再用切片读出最小字符字串的内容。

#### 代码：


  class Solution:

      def gcdOfStrings(self, str1: str, str2: str) -> str:
          '''
          特性：如果两者有最小公因数，那么将两个字符串拼接后，无论凭借的顺序如何，那么这两个字符串是相等的
          方法：先算出最小公因数的长度，然后再利用切片方法读出这个字符串。再利用特性来返回值，满足特性及返回目标字符串，不满足则返回“”
          '''
          target_str_len = math.gcd(len(str1), len(str2))
          target_str = str1[:target_str_len]
          if str1+str2 == str2+str1:
              return target_str
          else:
              return ""
