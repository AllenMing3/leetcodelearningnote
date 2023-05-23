You are given two strings word1 and word2. Merge the strings by adding letters in alternating order, starting with word1. If a string is longer than the other, append the additional letters onto the end of the merged string.

Return the merged string.

来源：力扣（LeetCode）
链接：https://leetcode.cn/problems/merge-strings-alternately

思路：因为要遍历两个字符串，所以就可以考虑用for循环链解决，但是在for循环的**边界**可能出现**三种情况**：
- 两个字符串一样长
- word1更长
- word2更长
所以就需要先对两个字符串长度进行比较，在共同长度的时候可以结合for循环和append（）来解决，超过共同长度直接试用append和切片来解决

难点：判断边界位置后的处理方式，还有就是把append后的内容转化到同一个字符串中

代码：


  class Solution:

      def mergeAlternately(self, word1: str, word2: str) -> str:
          '''
          1. 先遍历共同长度的部分，在这个阶段一次循环append word1再append word2
          2. 再加上多余的部分
          3. 再用join（）方法放入一个字符串中
          '''
          minlen = min(len(word1), len(word2))
          ans = []
          for i in range(minlen):
              ans.append(word1[i])
              ans.append(word2[i])
          if len(word1) < len(word2):
              ans.append(word2[minlen:])
          else:
              ans.append(word1[minlen:])
          return "".join(ans)
