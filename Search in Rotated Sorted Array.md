There is an integer array nums sorted in ascending order (with distinct values).

Prior to being passed to your function, nums is possibly rotated at an unknown pivot index k (1 <= k < nums.length) such that the resulting array is [nums[k], nums[k+1], ..., nums[n-1], nums[0], nums[1], ..., nums[k-1]] (0-indexed). For example, [0,1,2,4,5,6,7] might be rotated at pivot index 3 and become [4,5,6,7,0,1,2].

Given the array nums after the possible rotation and an integer target, return the index of target if it is in nums, or -1 if it is not in nums.

You must write an algorithm with O(log n) runtime complexity.

来源：力扣（LeetCode）
链接：https://leetcode.cn/problems/search-in-rotated-sorted-array


思路：现在是两端有序数列组成的一个新数列，时间复杂度要求logn，所以会猜测用二分来解决问题；如果使用二分就会转化为两个问题：
- 第1个问题是二分后，和nums[mid]比较后，调整范围变成一个**有序数列**
- 第2个问题是二分后，和nums[mid]比较后，删除了一些数据，**缩小了总体的数据**，依旧是由两个有序数组组成

代码：

        
    class Solution:
        def search(self, nums: List[int], target: int) -> int:
            '''
            看到logn的复杂度，首先反应就是二叉树或者二分这类的算法 
            '''
            if not nums:
                return -1

            left, right = 0, len(nums) - 1
            while left <= right:
                mid = (right+left) // 2
                if target == nums[mid]:
                    return mid

                if nums[left] <= nums[mid]:  #旋转后排在前面的大数比较多
                    if nums[left] <= target <= nums[mid]:
                        right = mid - 1     #变成一个有序数组的问题
                    else:
                        left = mid + 1      #缩小数组范围（两端递增数组）

                else:                        #旋转后排在后面的小数比较多
                    if nums[mid] <= target <= nums[right]:
                        left = mid + 1      #变成一个有序数组问题
                    else:
                        right = mid - 1     #缩小数组范围（两端递增数组）

            return -1
            

                        
        




            
