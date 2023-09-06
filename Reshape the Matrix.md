# Reshape the Matrix
     
***题目描述*** 
給定一個矩陣 nums 和兩個正整數 r 和 c，其中 nums 的行數是 m，列數是 n。重塑矩陣，使其成為一個新的矩陣，新矩陣也是 m x n 的，並且新矩陣的元素按照逐行順序排列。

如果可以重塑矩陣，返回重塑後的新矩陣；否則，返回原始矩陣。
在c++中建立2維vctor
    
```C++=
vector<vector<int>> matrix;
```
```C++=
// 宣告一個 3x3 的矩陣
vector<vector<int>> matrix(3, vector<int>(3, 0));
```


```C++=
v[i][j]=mat[k/mat[0].size()][k%mat[0].size()];
```
這段程式碼的目的是將原先的矩陣 mat 進行重塑，轉換為一個 r 列 c 行的新矩陣 v。

其中，k 為一個用來紀錄處理到原始矩陣中的哪個位置的變數。 k 的初始值為 0，當將 mat 中的數字按照新的行列放入 v 中後， k 的值將會變為原始矩陣的元素個數 mat.size()*mat[0].size()。

此時， v[i][j] 表示新矩陣中第 i 行第 j 列的值。
***它所對應的原始矩陣中的位置可以用 (k/mat[0].size(), k%mat[0].size()) 表示。其中 k/mat[0].size() 表示 k 在原始矩陣中所在的行， k%mat[0].size() 表示 k 在原始矩陣中所在的列。***
(除上的是行數)

最後，將 k 的值加 1，以便處理下一個原始矩陣中的數字。重複以上步驟，直到所有的元素都被放入新的矩陣 v 中。

```C++=
class Solution {
public:
    vector<vector<int>> matrixReshape(vector<vector<int>>& mat, int r, int c) {
        // 判斷是否滿足轉換條件，mat.size() 要和 r * c 一樣大
        if ((mat.size() * mat[0].size()) != (r * c)) {
            // 不滿足條件，返回原始矩陣
            return mat;
        }
        
        // 創建一個 r 行 c 列的矩陣，初始化為 0
        vector<vector<int>> Rmatrix(r, vector<int>(c, 0));

        // 初始化 k 變量，k 用來遍歷原始矩陣
        int k = 0;
        for (int i = 0; i < Rmatrix.size(); i++) {
            for (int j = 0; j < Rmatrix[0].size(); j++) {
                // 將原始矩陣的元素轉換到新的矩陣中
                // 使用 mat[k/mat[0].size()][k%mat[0].size()] 訪問原始矩陣
                // mat[0].size() 是用來求每行元素個數的
                Rmatrix[i][j] = mat[k/mat[0].size()][k%mat[0].size()];

                // 更新 k 變量
                k++;
            }
        }
        // 返回轉換後的矩陣
        return Rmatrix;
    }
};
```


[1, 2, 3]
[4, 5, 6]
[7, 8, 9]

第0個元素是1 在mat中是[0 / 3][0 % 3]= [0][0]
第1個元素是2 在mat中是[1 / 3][1 % 3]= [0][1]
第2個元素是3 在mat中是[2 / 3][2 % 3]= [0][2]
第3個元素是4 在mat中是[3 / 3][3 % 3]= [1][0]
第4個元素是5 在mat中是[4 / 3][4 % 3]= [1][1]...
第n個元素是[n / mat[0].size()][n % mat[0].size()]
          (除行數商得列)       (除行數餘得行)
          
          
法二:
用queue


```C++=
class Solution {
public:
    vector<vector<int>> matrixReshape(vector<vector<int>>& nums, int r, int c) {
        //檢查是否可以Reshape矩陣
        if((nums.size() * nums[0].size()) != (r * c)){
            return nums;
        }
        vector<vector<int>>Rmatrix(r, vector<int>(c, 0));
        queue<int>temp;
        for(int i = 0; i < nums.size(); i++){
            for(int j = 0; j < nums[0].size(); j++){
                temp.push(nums[i][j]);
            }
        }
        for(int i = 0; i < r; i++){
            for(int j = 0; j < c; j++){
                Rmatrix[i][j] = temp.front();
                temp.pop();
            }
        }
        return Rmatrix;
    }
};

```

###### tags: `array`