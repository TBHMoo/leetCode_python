
### 题目大意
Given a sorted array consisting of only integers where every element appears twice except for one element which appears once. Find this single element that appears only once.

* 输入一个有序数组，除了一个元素只出现一次，数组中每个元素出现两次。
* 求只出现一次的元素

### Example 1:
* Input: [1,1,2,3,3,4,4,8,8]
* Output: 2
### Example 2:
* Input: [3,3,7,7,10,11,11]
* Output: 10

Note: Your solution should run in O(log n) time and O(1) space.
* 要求算法复杂度只能是 O(logn) 不能遍历数组
~~~java
class Solution {
   public int singleNonDuplicate(int[] nums) {
        int l = 0, mid = 0, r = nums.length - 1;
        int result = 0;
        while (l < r) {
            mid = (l + r) / 2;
            int leftval = nums[mid] ^ nums[mid - 1];
            int rightval = nums[mid] ^ nums[mid + 1];
            if (l == r - 2) {
                if (leftval == 0 && rightval != 0) {
                    result = nums[r];
                } else if (leftval != 0 && rightval == 0) {
                    result = nums[l];
                }
                break;
            }
            
            if (leftval == 0 && rightval != 0) {
                int leftCount = mid -1;
                int rightCount = r-mid; 
                if(leftCount %2 ==0){
                     l = mid + 1  ;
                }
                if (rightCount %2 == 0){
                     r = mid - 2;
                }      
            } else if (leftval != 0 && rightval == 0) {
                int leftCount = mid;
                int rightCount = r- (mid+1); 
                if(leftCount %2 ==0){
                     l = mid + 2  ;
                }
                if (rightCount %2 == 0){
                     r = mid - 1;
                }
            } else if (leftval != 0 && rightval != 0) {
                result = nums[mid];
                break;
            }
        }
        return result;
    }
}
~~~

算法没问题，回头改成python实现