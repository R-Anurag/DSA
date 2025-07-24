## Set Matrix Zeroes (In-place)

**Problem**:  
Given an `m x n` matrix, if any element is `0`, set its entire row and column to `0` — in-place.

---

### Approach 1: Extra Space (O(m + n))

**Idea**:  
Use two separate arrays to track which rows and columns contain 0.

---

### Code

```cpp
void setZeroes(vector<vector<int>>& matrix) {
    int m = matrix.size(), n = matrix[0].size();
    vector<int> row(m, 0), col(n, 0);

    // Mark the rows and columns that need to be zeroed
    for (int i = 0; i < m; ++i)
        for (int j = 0; j < n; ++j)
            if (matrix[i][j] == 0)
                row[i] = col[j] = 1;

    // Set matrix[i][j] to 0 if row[i] or col[j] is marked
    for (int i = 0; i < m; ++i)
        for (int j = 0; j < n; ++j)
            if (row[i] || col[j])
                matrix[i][j] = 0;
}
```

**Time**: O(m × n)  
**Space**: O(m + n)

---

### Approach 2: Optimal In-place (O(1) space)

**Idea**:  
Use the first row and first column as markers to indicate which rows/cols should be zeroed.  
Use two flags to check if the first row and column themselves need to be zeroed.

---

### Code

```cpp
void setZeroes(vector<vector<int>>& matrix) {
    int m = matrix.size(), n = matrix[0].size();
    bool row0 = false, col0 = false;

    // Check if first column has zero
    for (int i = 0; i < m; ++i)
        if (matrix[i][0] == 0) col0 = true;

    // Check if first row has zero
    for (int j = 0; j < n; ++j)
        if (matrix[0][j] == 0) row0 = true;

    // Mark zeros in first row and column
    for (int i = 1; i < m; ++i)
        for (int j = 1; j < n; ++j)
            if (matrix[i][j] == 0)
                matrix[i][0] = matrix[0][j] = 0;

    // Set elements based on markers
    for (int i = 1; i < m; ++i)
        for (int j = 1; j < n; ++j)
            if (matrix[i][0] == 0 || matrix[0][j] == 0)
                matrix[i][j] = 0;

    // Zero the first column if needed
    if (col0)
        for (int i = 0; i < m; ++i)
            matrix[i][0] = 0;

    // Zero the first row if needed
    if (row0)
        for (int j = 0; j < n; ++j)
            matrix[0][j] = 0;
}
```

**Time**: O(m × n)  
**Space**: O(1)

---
```
