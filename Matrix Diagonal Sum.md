# Matrix Diagonal Sum
題目描述：
  
給定一個矩陣 mat，請計算它的對角線元素的和。

說明：

1. 矩陣的對角線是從左上到右下的一條直線。
1. 輸入矩陣的行數和列數不超過100。
1. 輸入矩陣中的整數在(-2^31, 2^31 - 1)範圍內。

解題思路：

1. 遍歷矩陣，並計算主對角線和副對角線上的元素的和。
1. 如果矩陣的行數和列數是奇數，那麼它的中心元素會被計算兩次，因此需要減去一次。
1. 返回主對角線和副對角線上元素的總和。
```c++=
class Solution {
public:
    int diagonalSum(vector<vector<int>>& mat) {
        //正對角線[0][0], [1][1], [2][2], ..., [i][i]
        //逆對角線[0][n-1-0], [1][n-1-1], ..., [i][n-1-i];
        //中心點如果n為奇數會重複計算
        int sum = 0;
        int n = mat.size();
        for(int i = 0; i < mat.size(); i++){        
            sum += mat[i][i] + mat[i][n-1-i];
        }
        if((n % 2) == 1){                       //利用%求餘判斷是否是奇數matrix
            sum -= mat[n/2][n/2];
        }
        return sum;
    }
};
```
```C++=
class Solution {
public:
    int diagonalSum(vector<vector<int>>& mat) {
        //正對角線[0][0], [1][1], [2][2], ..., [i][i]
        //逆對角線[0][n-1-0], [1][n-1-1], ..., [i][n-1-i];
        //中心點如果n為奇數會重複計算
        int sum = 0;    // 初始對角線和為0
        int n = mat.size();  // n為matrix的大小，由於matrix是正方形，可以只取其中一個維度的大小
        for(int i = 0; i < mat.size(); i++){  // 遍歷matrix中每一列
            sum += mat[i][i] + mat[i][n-1-i];  // 將正對角線和逆對角線的值加總
        }
        if((n % 2) == 1){    // 如果matrix的大小是奇數
            sum -= mat[n/2][n/2];  // 減去中心點的值，中心點會被重複計算
        }
        return sum;   // 回傳對角線和
    }
};
```


###### tags: `array`