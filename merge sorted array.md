# merge sorted array
###### tags: `array`
 
題目描述：
給定兩個已排序的整數數組 nums1 和 nums2，將 nums2 合併到 nums1 中，使 nums1 成為一個已排序的數組。
註：
初始化 nums1 和 nums2 的元素數分別為 m 和 n。
可以假設 nums1 有足夠的空間（大於或等於 m + n）來保存 nums2 中的其他元素。 

範例：
輸入：
nums1 = [1,2,3,0,0,0], m = 3
nums2 = [2,5,6], n = 3
輸出：
[1,2,2,3,5,6]

解題思路：
因為 nums1 有足夠的空間來容納 nums2 中的元素，所以可以從 nums1 和 nums2 的末尾開始，依次比較兩個數組的元素，將較大的元素插入到 nums1 的末尾。
具體做法是，先將 nums1 和 nums2 的末尾下標分別記為 m - 1 和 n - 1。然後從 nums1 和 nums2 的末尾開始遍歷，每次取兩個數組中當前位置的元素，比較其大小，將較大的元素插入到 nums1 的末尾。如果 nums1 中的元素都已經排列好了，但 nums2 中還有元素沒有被遍歷到，那麼可以直接將剩餘的元素插入到 nums1 的前面

```c++=
class Solution {
public:
    void merge(vector<int>& nums1, int m, vector<int>& nums2, int n) {
        //兩個vector都已經排序過
        //比較兩個vector的值然後插入
        //因為nums1有空格了從後面開始放會更好
        int i = m - 1;  //nums1的尾端
        int j = n - 1;  //nums2的尾端
        int k = m + n -1;   //合併後的尾端
        if(nums2.empty()){
            return ;
        }
        if(nums1.empty()){
            for(int k = 0; k < nums2.size(); k++){
                nums1.push_back(nums2[k]);             
            }
        }

        while(i >= 0 && j >= 0){
            if(nums1[i] >= nums2[j]){   
                nums1[k] = nums1[i];    //升序
                k--;
                i--;
            }else{
                nums1[k] = nums2[j];
                k--;
                j--;
            }
        }
        //如果nums2還有沒被放到的元素代表剩下的都小於nums1了 所以按照順序放入 因為是已經排序好的
        while(j >= 0){
            nums1[k] = nums2[j];
            k--;
            j--;
        }
    }
};
```