# Search Insert Position

題目描述：

給定一個排序過的整數陣列 nums 和一個目標值 target，請在數組中找到 target，並返回其索引。如果目標值不存在於數組中，則返回它將會被按順序插入的位置。

解題思路：
此題可以使用二分法來解決，首先找到中心點，若中心點比目標小，則將中心點右邊的數字當作新的數列再次進行二分法，反之，將中心點左邊的數字當作新的數列再次進行二分法，直到找到目標值或是無法再切割，此時返回最後一個比目標值小的數字的索引+1，即為目標值應該插入的位置。
在程式實現方面，先將輸入的陣列進行排序，然後使用二分法查找目標值或者目標值應該插入的位置。若目標值存在於陣列中，則直接返回其索引；否則，最終會找到最後一個比目標值小的數字的索引 i，此時返回 i+1，即為目標值應該插入的位置。
  
```c++=
class Solution {
public:
    int searchInsert(vector<int>& nums, int target) {
        int high = nums.size(); // 設定右邊界
        int low = 0; // 設定左邊界
        int mid; // 設定中心點
        if(target > nums[high-1]){ // 如果目標值大於數組中的最後一個元素，則返回右邊界
            return high;
        }
        while(low <= high){ // 當左邊界小於等於右邊界時
            mid = (low + high) /2; // 計算中心點
            if(target == nums[mid]){ // 如果中心點等於目標值，直接返回中心點索引
                return mid;
            }

            if(target > nums[mid]){ // 如果目標值大於中心點，將左邊界右移
                low = mid +1;
            }else{ // 如果目標值小於中心點，將右邊界左移
                high = mid -1;
            }
        }
        return low; // 若遍歷完整個數列仍未找到目標值，此時 left 就是最後一個比目標值小的數字的索引，因此返回 left+1
    }
};
```


###### tags: `array`