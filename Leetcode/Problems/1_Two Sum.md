## 1 Two Sum
题目描述：Given an array of integers, return indices of the two numbers such that they add up to a specific target.

You may assume that each input would have exactly one solution, and you may not use the same element twice.

题目理解：输入一个数组和一个目标值，若数组中两个值之和等于目标值，返回它们的下标，每个数只能使用一次。

---

代码：

    public class Solution {
        public int[] twoSum(int[] nums, int target) {
            Map<Integer,Integer> diffs = new HashMap<>();
            Integer i = null, index = null;
            for (i = 0; i < nums.length ; i++) {
                if (  ( index = diffs.get( nums[i] ) ) != null ) {
                    break;
                } else {
                    diffs.put( target - nums[i] , i);
                }
            }
            int[] indexs = {index,i};
            return indexs;
        }
    }
    
重头开始遍历，查看当前数字是否在差值中，在其中就返回，否则计算差值，加入map。

复杂度：nlog(n)，运行时间12ms。

![images](https://raw.githubusercontent.com/isadamu/note/master/Leetcode/Problems/images/Two_Sum_1.png)

---

代码：

    public class Solution {
        public int[] twoSum(int[] nums, int target) {
            int[][] inums = new int[nums.length][2];
            for ( int i = 0; i < nums.length; i++ ) {
                inums[i][0] = nums[i];
                inums[i][1] = i;
            }
            Arrays.sort(inums, new Comparator<int[]>() {
                public int compare( int[] o1, int[] o2 ) {
                    return o1[0] - o2[0];
                }
            });
            int[] res = {-1,-1};
            int l = 0, r = inums.length - 1;
            while ( l < r ) {
                int sum = inums[l][0] + inums[r][0];
                if ( sum < target ) {
                    l++;
                } else if ( sum > target ) {
                    r--;
                } else {
                    res[0] = inums[l][1]; res[1] = inums[r][1];
                    return res;
                }
            }
            return res;
        }
    }
    
将原始数据排序，然后进行左右逼近，得到结果。

复杂度nlog(n),运行时间12ms。

![images](https://raw.githubusercontent.com/isadamu/note/master/Leetcode/Problems/images/Two_Sum.png)
