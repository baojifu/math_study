# 1.模版1
区分语法

- 初始条件：left = 0, right = length-1   
- 终止：left > right   
- 向左查找：right = mid-1   
- 向右查找：left = mid+1   

关键属性：   
- 二分查找的最基础和最基本的形式。   
- 查找条件可以在不与元素的两侧进行比较的情况下确定（或使用它周围的特定元素）。   
- 不需要后处理，因为每一步中，你都在检查是否找到了元素。如果到达末尾，则知道未找到该元素。


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

# 2.模版2
区分语法   
- 初始条件：left = 0, right = length   
- 终止：left == right   
- 向左查找：right = mid   
- 向右查找：left = mid+1   

关键属性：   
- 一种实现二分查找的高级方法。  
- 查找条件需要访问元素的直接右邻居。  
- 使用元素的右邻居来确定是否满足条件，并决定是向左还是向右。  
- 保证查找空间在每一步中至少有 2 个元素。  
- 需要进行后处理。 当你剩下 1 个元素时，循环 / 递归结束。 需要评估剩余元素是否符合条件。   

```C
int binarySearch(vector<int>& nums, int target){
  if(nums.size() == 0)
    return -1;

  int left = 0, right = nums.size();
  while(left < right){
    // Prevent (left + right) overflow
    int mid = left + (right - left) / 2;
    if(nums[mid] == target){ return mid; }
    else if(nums[mid] < target) { left = mid + 1; }
    else { right = mid; }
  }

  // Post-processing:
  // End Condition: left == right
  if(left != nums.size() && nums[left] == target) return left;
  return -1;
}
```

# 3.模版3
区分语法   
- 初始条件：left = 0, right = length-1  
- 终止：left + 1 == right  
- 向左查找：right = mid  
- 向右查找：left = mid  

关键属性：   
- 实现二分查找的另一种方法。  
- 搜索条件需要访问元素的直接左右邻居。  
- 使用元素的邻居来确定它是向右还是向左。  
- 保证查找空间在每个步骤中至少有 3 个元素。  
- 需要进行后处理。 当剩下 2 个元素时，循环 / 递归结束。 需要评估其余元素是否符合条件。  
   

```C
int binarySearch(vector<int>& nums, int target){
    if (nums.size() == 0)
        return -1;

    int left = 0, right = nums.size() - 1;
    while (left + 1 < right){
        // Prevent (left + right) overflow
        int mid = left + (right - left) / 2;
        if (nums[mid] == target) {
            return mid;
        } else if (nums[mid] < target) {
            left = mid;
        } else {
            right = mid;
        }
    }

    // Post-processing:
    // End Condition: left + 1 == right
    if(nums[left] == target) return left;
    if(nums[right] == target) return right;
    return -1;
}
```

https://www.cnblogs.com/kyoner/p/11080078.html
# 4.模版4
寻找左边界  
```C
int left_bound(int[] nums, int target) {
    if (nums.length == 0) return -1;
    int left = 0;
    int right = nums.length; // 注意

    while (left < right) { // 注意
        int mid = (left + right) / 2;
        if (nums[mid] == target) {
            right = mid;  // 注意：不退出，像左侧缩小区间继续查找，不退出
        } else if (nums[mid] < target) {
            left = mid + 1;
        } else if (nums[mid] > target) {
            right = mid; // 注意
        }
    }
    return left;
}
```
上述返回值，没有返回-1，实际返回值的含义可以看成是“小于target的数量”。[1, 2, 3, 4] target=8, 返回4   
如果要返回左侧第一个目标值，那么增加如下：  
```C
// target 比所有数都大
if (left == nums.length) return -1;
// 类似之前算法的处理方式
return nums[left] == target ? left : -1;
```
面试题 10.03. 搜索旋转数组
https://leetcode-cn.com/problems/search-rotate-array-lcci/

# 5.模版5
寻找右侧边界  
```C
int right_bound(int[] nums, int target) {
    if (nums.length == 0) return -1;
    int left = 0, right = nums.length;

    while (left < right) {
        int mid = (left + right) / 2;
        if (nums[mid] == target) {
            left = mid + 1; // 注意
        } else if (nums[mid] < target) {
            left = mid + 1;
        } else if (nums[mid] > target) {
            right = mid;
        }
    }
    return left - 1; // 注意
```

```C
if (left == 0) return -1;
return nums[left-1] == target ? (left-1) : -1;
```
