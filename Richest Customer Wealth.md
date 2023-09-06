# Richest Customer Wealth
題目解析:
給定一個客戶的財富陣列，每個陣列內的元素代表每個客戶的財富。請您寫一個函數，計算出所有客戶的財富總和。

解題思路:
首先，初始化一個變量 max_wealth 用於存儲最富有的客戶的財富。然後，遍歷每一個客戶的財富，將客戶的財富與 max_wealth 比較，如果客戶的財富大於 max_wealth，則更新 max_wealth。最後，返回 max_wealth。
   
EX:
Input: accounts = [[1,2,3],[3,2,1]]
Output: 6
Explanation:
1st customer has wealth = 1 + 2 + 3 = 6
2nd customer has wealth = 3 + 2 + 1 = 6
Both customers are considered the richest with a wealth of 6 each, so return 6.


```c++=
class Solution {
public:
    int maximumWealth(vector<vector<int>>& accounts) {
           int maxWealth = 0;
           int sum = 0;
           for(int i = 0; i < accounts.size(); i++){
               sum = 0;
               for(int j = 0; j < accounts[0].size(); j++){
                   sum += accounts[i][j];
               }
               maxWealth = max(maxWealth, sum); 
           }
    return maxWealth;       
    }
};
```
遍歷二維vector的方法
```C++=
vector<vector<int>> vec = { {1, 2, 3},
                            {4, 5, 6},
                            {7, 8, 9} };
for(int i=0; i<vec.size(); i++) {
    for(int j=0; j<vec[i].size(); j++) {
        // 对vec[i][j]进行操作
        cout << vec[i][j] << " ";
    }
    cout << endl;
}
```

vec 是一个二维 vector，包含三个子 vector，即三行数据。通过 vec[0]，我们可以获得第一行的数据。我们使用一个 for 循环，遍历第一行中的所有元素，并将它们打印出来。输出结果应该为：


###### tags: `array`