# 1.模版一
区分语法

初始条件：left = 0, right = length-1

终止：left > right

向左查找：right = mid-1

向右查找：left = mid+1

关键属性：

二分查找的最基础和最基本的形式。

查找条件可以在不与元素的两侧进行比较的情况下确定（或使用它周围的特定元素）。

不需要后处理，因为每一步中，你都在检查是否找到了元素。如果到达末尾，则知道未找到该元素。


```C
int binarySearch(vector<int>& nums, int target){
  if(nums.size() == 0)
    return -1;

  int left = 0, right = nums.size() - 1;
  while(left <= right){
    // Prevent (left + right) overflow
    int mid = left + (right - left) / 2;
    if(nums[mid] == target){ return mid; }
    else if(nums[mid] < target) { left = mid + 1; }
    else { right = mid - 1; }
  }

  // End Condition: left > right
  return -1;
}
```
