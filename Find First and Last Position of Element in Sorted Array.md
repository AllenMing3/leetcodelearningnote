Given an array of integers nums sorted in non-decreasing order, find the starting and ending position of a given target value.

If target is not found in the array, return [-1, -1].

You must write an algorithm with O(log n) runtime complexity.

来源：力扣（LeetCode）
链接：https://leetcode.cn/problems/find-first-and-last-position-of-element-in-sorted-array

思路：
因为考虑到时间**复杂度是Ologn**，那么就是不能遍历整个数组了
我的想法结合**二分法**来做，就是从mid开始出发，在辐射到1/4, 3/4用这些下标的值target比较，
确认是左半部分还是右半部分，这样二分式的确定范围，最终去确认下标
显然strat，end两个值的寻找方法是类似的，所以可以考虑先寻找start，end

难点：
目前卡在了设定两个函数，求出start，end后，不太会如何在leetcode中控制在同一个类中函数结果的调用。等下去看一下结果。

代码：



  class Solution:
  
      def start_bound(nums:List[int], target:int) -> int:
          left, right = 0, len(nums) - 1
          while left <= right:
              mid = (left + right) // 2
              if nums[mid] < target:
                  left = mid + 1
              else:           #因为是找第一个出现的值，所以>和>=等效
                  right = mid - 1
          return left
          
          
      def end_bound(nums:List[int], target:int) -> int:
          left, right = 0, len(nums) - 1
          while left <= right:
              mid = (left + right) // 2
              if nums[mid] < target:
                  left = mid
              else:           #因为是找最后一个出现的值，所以>和>=等效
                  right = mid
          return right 
          
          
      def searchRange(self, nums: List[int], target: int) -> List[int]:
          '''
          因为考虑到时间复杂度是Ologn，那么就是不能遍历整个数组了
          我的想法结合二分法来做，就是从mid开始出发，在辐射到1/4, 3/4用这些下标的值target比较，
          确认是左半部分还是右半部分，这样二分式的确定范围，最终去确认下标
          显然strat，end两个值的寻找方法是类似的，所以可以考虑先寻找start，end
          '''
          start = self.start_bound(nums, target)
          if start == len(nums) or nums[start] != target:
              return[-1, -1]
          end = self.end_bound(nums, target)
          return [start, end]
 
