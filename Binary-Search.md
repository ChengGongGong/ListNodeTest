# 二分查找
1. 二分查找使用场景：寻找一个数、寻找左侧边界、寻找右侧边界

2. 二分查找框架
  
        int binarySearch(int[] nums, int target) {
      
            int left = 0, right = ...;

            while(...) {
                int mid = left + (right - left) / 2;
            if (nums[mid] == target) {
                 ...
            } else if (nums[mid] < target) {
                left = ...
            } else if (nums[mid] > target) {
                right = ...
            }
         }
            return ...;
       }
