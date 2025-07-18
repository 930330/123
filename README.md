## 41141114
作業一
## 解題說明
本題要求實現一個 遞迴函式，計算 Ackermann 函數𝐴(𝑚,𝑛)的值。
## 解題策略
1. 使用遞迴函式將問題拆解為更小的子問題

   ```cpp
   若 m=0，回傳 n+1
   若 n=0，回傳 A(m−1,1)
   否則，先計算 A(m,𝑛−1)，再以結果作為第二個參數，繼續計算 A(m−1,...)
   當 m=0 時，返回 n+1 作為遞迴的結束條件
3. 主程式呼叫遞迴函式，並輸出計算結果

## 程式實作
以下為主要程式碼：

```cpp
#include <iostream>
using namespace std;

// 遞迴實作 Ackermann 函數
int ackermann_recursive(int m, int n) {
    if (m == 0) return n + 1;
    else if (n == 0) return ackermann_recursive(m - 1, 1);
    else return ackermann_recursive(m - 1, ackermann_recursive(m, n - 1));
}

int main() {
    int m, n;
    cout << "請輸入 m 的值：";
    cin >> m;
    cout << "請輸入 n 的值：";
    cin >> n;
    
    int result = ackermann_recursive(m, n);
    cout << "Ackermann 函數結果為：" << result << endl;
    return 0;
}
```
## 效能分析
時間複雜度：程式的時間複雜度為 O(A(m,n))。

Ackermann 函數的成長速度非常快，甚至比指數函數還快，其遞迴呼叫次數會隨著 m 和 n 急劇增加。對於輸入 m 和 n 的不同組合，其執行時間近乎呈現超指數級別成長

空間複雜度：空間複雜度為 O(A(m,n))。

程式每次遞迴呼叫都會佔用一次堆疊空間，最壞情況下的呼叫深度接近 Ackermann 函數本身的值，空間需求也會非常高。

## 測試與驗證

## 測試案例
| 測試案例 | 輸入參數 $m、n$ | 預期輸出 | 實際輸出 |
|----------|--------------|----------|----------|
| 測試一   | $n = 0$      | 0        | 0        |
| 測試二   | $n = 1$      | 1        | 1        |
| 測試三   | $n = 3$      | 6        | 6        |
| 測試四   | $n = 5$      | 15       | 15       |
| 測試五   | $n = -1$     | 異常拋出 | 異常拋出 |
| m | n | Ackermann 函數結果 |

