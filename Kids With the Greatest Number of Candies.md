#### 题目
There are n kids with candies. You are given an integer array candies, where each candies[i] represents the number of candies the ith kid has, and an integer extraCandies, denoting the number of extra candies that you have.

Return a boolean array result of length n, where result[i] is true if, after giving the ith kid all the extraCandies, they will have the greatest number of candies among all the kids, or false otherwise.

Note that multiple kids can have the greatest number of candies.

来源：力扣（LeetCode） 
链接：https://leetcode.cn/problems/kids-with-the-greatest-number-of-candies

#### 思路
- 很明显，这个题目需要先用max（）方法求出数列的 candies_max 值，然后在让原数列 candies[] 中的每个数值加上 extracandies 求得candies_new 用这个新的数值和 max 值比较，如果大于等于 candies_max 就append true，另外的情况就 append false
- 需要注意的是在代码解释的时候如果用 true 而没用 True 可能造成错误：
  NameError: name 'true' is not defined. Did you mean: 'True'?


#### 代码
  class Solution:

      def kidsWithCandies(self, candies: List[int], extraCandies: int) -> List[bool]:
          '''
          先求出最大值，然后遍历一遍整个列表，并与最大值比较，大于等于就 append true，反之 append false 
          '''
          ans = []
          candies_max = max(candies)
          for i in candies:
              if i+extraCandies >= candies_max:
                  ans.append(True)
              else:
                  ans.append(False)
          return ans
