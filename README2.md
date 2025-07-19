## 41141114

作業二：

## 解題說明
本題要求實作一個 遞迴函式，計算一個集合 S 的 Power Set（冪集合），即所有子集合的集合。

## 解題策略
問題拆解
對集合 S 中的每個元素，遞迴地選擇是否包含它，進而產生所有子集合。

遞迴函式設計
設 index 為目前處理到的元素索引，current 為目前累積的子集合：

若 index == S.size()，表示到底了，輸出 current。

否則遞迴呼叫兩次：

一次不包含 S[index]

一次包含 S[index] 到目前子集合。

## 程式實作
以下為主要程式碼：
```cpp
#include <iostream>
#include <vector>
#include <string>
using namespace std;

// 遞迴計算 Power Set
void generatePowerSet(const vector<char>& set, int index, string current) {
    if (index == set.size()) {
        cout << "{" << current << "}" << endl;
        return;
    }

    // 不選當前元素
    generatePowerSet(set, index + 1, current);

    // 選當前元素
    generatePowerSet(set, index + 1, current + set[index]);
}

int main() {
    vector<char> S = {'a', 'b', 'c'};
    cout << "Power set of {a, b, c}:\n";
    generatePowerSet(S, 0, "");
    return 0;
}
```
## 效能分析

時間複雜度:為 \(O(2^n)\)，成長快速，適用於小型集合。

空間複雜度:為 \(O(n)\)（呼叫堆疊空間），加上輸出空間。

## 測試與驗證

| 測試編號 | 輸入集合       | 預期子集合數 | 實際結果                   | 
|----------|----------------|--------------|----------------------------|
| 測試 1   | {a, b, c}      | 8            | {}, {a}, {b}, {c}, {ab}, {ac}, {bc}, {abc} |

### 編譯與執行指令
```
g++ -std=c++17 -o powerset powerset.cpp
./powerset
```

### 結論
程式能正確列舉集合中所有子集合。

遞迴解法簡潔，適合學習樹狀結構與分支選擇。

適用於集合元素較少的情況，因為子集合總數為 2ⁿ，成長快速。

## 申論及開發報告
 ### 1.數學定義自然對應遞迴邏輯 ###
子集合枚舉本質上是每個元素做「要 / 不要」決策，非常適合遞迴表示。

 ### 2.邏輯清晰，易於理解與撰寫 ###
每一層遞迴代表一個選擇分支，程式結構直觀。

### 3.程式簡潔，不需額外資料結構 ###

#### 遞迴模式有助於理解 樹狀遞迴結構 的形成，以及每層決策如何影響最終結果  
但Power Set 的成長不像 Ackermann 函數那麼極端，但子集合數為2ⁿ，屬指數成長。當元素數超過 20，子集合數將達百萬，可能導致執行效率降低或記憶體不足
