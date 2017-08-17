## 16.3Sum Cloest

> Description:
>
>> Given an array S of n integers, find three integers in S such that the sum is closest to a given number, target. Return the sum of the three integers. You may assume that each input would have exactly one solution.
>
> example
>
>> For example, given array S = {-1 2 1 -4}, and target = 1.
>> 
>> The sum that is closest to the target is 2. (-1 + 2 + 1 = 2).

---

题目理解：输入一个数组和一个目标值，求数组中三个数的和，返回和与目标值之间的最小差值。

---

代码：

    public class Solution {
        public int threeSumClosest(int[] nums, int target) {
            int dis = Integer.MAX_VALUE, result = -1, m = nums.length;
            Arrays.sort(nums);
            for ( int i = 0, bound = m - 2 ; i < bound && dis != 0 && nums[i] - target < dis; ) {
                int l = i + 1, r = m - 1;
                while ( l < r ) {
                    int sum = nums[i] + nums[l] + nums[r];
                    int temp_dis = sum - target;
                    temp_dis = temp_dis > 0 ? temp_dis : -temp_dis;
                    if ( temp_dis < dis ) {
                        dis = temp_dis;
                        result = sum;
                    }
                    if ( sum - target < 0 ) l++;
                    else r--;
                }
                i++;
                while ( i < bound && nums[i] == nums[i-1] ) i++;
            }
            return result;
        }
    }
    
方法和3Sum几乎一样，只是多进行一下距离的比较。

复杂度 n^2, 运行时间 18ms.

![images](https://raw.githubusercontent.com/isadamu/note/master/Leetcode/Problems/images/3Sum_Closest.png)

