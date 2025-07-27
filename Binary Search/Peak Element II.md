# 2D Peak Finding

## Problem Statement
Given a 2D matrix `mat` of integers (size `m x n`), find any **peak element**.
A **peak** is an element that is **strictly greater** than its top, bottom, left, and right neighbors (if they exist).
### Input
- `mat`: 2D vector of integers
- `1 <= m, n <= 500`
- All elements in `mat` are distinct
### Output
- Return a vector `[i, j]` such that `mat[i][j]` is a peak
### Note
- Multiple peaks may exist; return **any one**
- You may assume that the entire matrix is surrounded by an outer perimeter with the value -1 in each cell
- You must write an algorithm that runs in O(m log(n)) or O(n log(m)) time.
---

## Intuition
- In each **row**, find the **maximum element** (i.e., the tallest pillar).
- Then check whether it's a **2D peak** by comparing it with its **above and below** neighbors.
- Use binary search on **rows** to cut the search space in half each time. 
---

## Algorithm Steps
1. Binary search over the row space (`rowLow` to `rowHigh`).
2. In each middle row:
   - Find the **column index** of the **maximum element** in that row.
3. Check if that element is a **2D peak**:
   - If it’s greater than the same column values in both the **above** and **below rows**, return it.
   - If the **below** element is greater, move search window **down**.
   - Else, move **up**.
4. Repeat until found.
---

## Code 
```cpp
class Solution {
public:
    int maximumElementColumn(vector<int>& rowArr) {
        int ans = 0;
        for (int i = 0; i < rowArr.size(); ++i) {
            if (rowArr[i] > rowArr[ans])
                ans = i;
        }
        return ans;
    }

    vector<int> findPeakGrid(vector<vector<int>>& mat) {
        int m = mat.size();
        int n = mat[0].size();

        int rowLow = 0, rowHigh = m - 1;
        while (rowLow <= rowHigh) {
            int rowMid = rowLow + (rowHigh - rowLow) / 2;

            int maxElCol = maximumElementColumn(mat[rowMid]);

            // Check if it's greater than top and bottom neighbors
            if ((rowMid == 0 || mat[rowMid][maxElCol] > mat[rowMid - 1][maxElCol]) &&
                (rowMid == m - 1 || mat[rowMid][maxElCol] > mat[rowMid + 1][maxElCol]))
                return {rowMid, maxElCol};

            else if (rowMid < m - 1 && mat[rowMid + 1][maxElCol] > mat[rowMid][maxElCol])
                rowLow = rowMid + 1; // Move down
            else
                rowHigh = rowMid - 1; // Move up
        }

        return {-1, -1}; // Should never reach here
    }
};
```
---

## Time Complexity

| Step | Complexity |
|------|------------|
| Find max in row | O(n) |
| Binary search on rows | O(log m) |
| **Total** | **O(n × log m)** |
---

## When to Use What
| Scenario | Approach |
|----------|----------|
| Rows ≫ Columns | Row-wise binary search (this method) |
| Columns ≫ Rows | Column-wise binary search |
---

## Why a 2D Binary Search fails But 1D Binary Search Works?
### Double Binary Search May Miss the Peak
- It checks a middle element (rowMid, colMid) and compares it to all four neighbors.
- But this point might not be the max in its row or column, so moving diagonally may miss actual peaks.
- Without any sorted structure, there's no guarantee you're moving toward the global peak.
> It would work only if both rows and columns are sorted.

### Single Binary Search Works Because
- We fix one direction (row or column), and in that row/column, we always take the maximum element.
- That guarantees we’re exploring the most promising peak candidate.
- Then we reduce the search space in the other direction based on the slope (neighboring values).
---
