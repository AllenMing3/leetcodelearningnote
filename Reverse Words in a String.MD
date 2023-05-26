#### 题目
Given an input string s, reverse the order of the words.

A word is defined as a sequence of non-space characters. The words in s will be separated by at least one space.

Return a string of the words in reverse order concatenated by a single space.

Note that s may contain leading or trailing spaces or multiple spaces between two words. The returned string should only have a single space separating the words. Do not include any extra spaces.

来源：力扣（LeetCode）
链接：https://leetcode.cn/problems/reverse-words-in-a-string

#### 思路
先用sprip()出去多余的空格，然后双指针方法，从后往前遍历，每次遍历到空格的时候就说明已经遍历过了一个单词，这个时候就可以把遍历的单词写入 res 中
然后遍历在空格区域，就需要一直移动头指针，知道第一次遍历到字母，这时候，移动尾指针。重复这个操作，直到头指针遍历完整个字符串

#### 难点
- 出去多余的空格
- 遍历的时候，尾指针移动的时机是在遍历完空格后的第一次
- append的时候要运用到切片，所以sec_指针位置需要 +1
- 便利完成后，因为要重新返回一个字符串所以需要做" ".join(s)操作

#### 代码

  class Solution:


      def reverseWords(self, s: str) -> str:
          '''
          思路：利用双指针从最后一个字符开始向前遍历整个字符串，每次遇到一个空格，则成功记录一个单词，把他append到新的列表中
          重复这个操作，已知到遍历完整个字符串        
          时间复杂度为 ON,空间复杂度为ON
          '''
          s = s.strip()
          fir_p = sec_p = len(s)-1
          res = []
          while fir_p >= 0:
              while fir_p >=0 and s[fir_p] != ' ': fir_p -= 1
              res.append(s[fir_p+1:sec_p+1])
              while s[fir_p] == ' ': fir_p -= 1
              sec_p = fir_p
          return ' '.join(res)
