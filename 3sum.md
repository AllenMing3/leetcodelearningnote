#### 题目
Given an integer array nums, return all the triplets [nums[i], nums[j], nums[k]] such that i != j, i != k, and j != k, and nums[i] + nums[j] + nums[k] == 0.

Notice that the solution set must not contain duplicate triplet

来源：力扣（LeetCode）
链接：https://leetcode.cn/problems/3sum

#### 思路：
确定先排序，最外层的循坏从小到大。内测循环利用指针，最小值和最大值相加再加上外侧循环的值，小于0小数变大，大于0大数变小
注意：
- 最小值大于0直接return []
- 可能存在index不同但是值相同的情况  
- return res的位置
      
      
#### 代码:


      class Solution:
          def threeSum(self, nums: List[int]) -> List[List[int]]:
              nums.sort()
              res, k =[], 0
              for k in range(len(nums) - 2): # the outmost circle
                  if nums[k] > 0: break      #all integer bigger than 0
                  if k > 0 and nums[k] == nums[k - 1]: continue
                  i, j = k + 1, len(nums) - 1
                  while i < j:
                      s = nums[k] + nums[i] + nums[j]
                      if s < 0:   # need a bigger integer
                          i += 1  
                          while  i < j and nums[i] == nums[i - 1]:
                              i += 1
                      elif s > 0: # need a smaller integer
                          j -= 1  
                          while i < j and nums[j] == nums[j + 1]:
                              j -= 1
                      else:       # need to append
                          res.append([nums[k], nums[i], nums[j]])
                          i += 1      # maybe the same value appear
                          j -= 1
                          while i < j and nums[i] == nums[i - 1]:  # need a bigger nums[i]
                              i += 1
                          while i < j and nums[j] == nums[j + 1]:  # need a smaller nums[j]
                              j -= 1
              return res

