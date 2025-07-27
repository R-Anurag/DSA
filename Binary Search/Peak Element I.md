# 🔺 Find Peak Element – Revision Notes

---

## 📌 Problem Definition

Given an array `nums`, a **peak element** is one that is **strictly greater than its neighbors**.

Return the **index of any peak element**.

> A peak is defined as:  
> `nums[i] > nums[i - 1] && nums[i] > nums[i + 1]`

---

## ✅ Binary Search Approach (O(log n))

### ✔️ Why Binary Search?

Even though the array is not sorted, you can use **slope logic** to perform binary search:
- If you're on an **increasing slope**, the peak lies to the **right**
- If you're on a **decreasing slope**, the peak lies to the **left**
- If the current element is greater than both neighbors → it’s a **peak**

### ✅ Code:

```cpp
class Solution {
public:
    int findPeakElement(vector<int>& nums) {
        int n = nums.size();
        if (n == 1) return 0;
        if (nums[0] > nums[1]) return 0;
        if (nums[n-1] > nums[n-2]) return n-1;

        int low = 1;
        int high = n - 2;

        while (low <= high) {
            int mid = low + (high - low) / 2;

            if (nums[mid] > nums[mid - 1] && nums[mid] > nums[mid + 1])
                return mid;
            else if (nums[mid] > nums[mid - 1] && nums[mid] < nums[mid + 1])
                low = mid + 1;
            else
                high = mid - 1;
        }

        return -1; // Should never reach here
    }
};
```

---

## 📈 Graphical Example

Example array:

```
Index:      0   1   2   3    4   5   6
nums[]:     1   3   8   12   4   2   0
```

Graph (conceptually):
```
           *
         *   ← peak at index 3 (12)
       *
     *
   *
 *
*
```

- `nums[3] = 12` is a **peak**: greater than both neighbors `8` and `4`

---

## ⛓️ Time and Space Complexity

| Approach        | Time Complexity | Space Complexity |
|-----------------|-----------------|------------------|
| Binary Search   | `O(log n)`      | `O(1)`           |
| Linear Search   | `O(n)`          | `O(1)`           |

---

## 🔥 Why Binary Search is Better Than Linear

| Feature               | Linear Search        | Binary Search         |
|------------------------|----------------------|------------------------|
| Strategy              | Check every element  | Use slope direction    |
| Performance on large input | Slower             | Much faster            |
| Peak Guarantee        | Always finds highest | Returns *a* peak       |
| Use Case              | Simple, brute-force  | Efficient, smart       |

---

## 🧠 Tips for Interviews

- Always check edge cases: size = 1, peak at start or end
- Binary search doesn't require sorted array here
- Understand slope-based movement:
  - `mid < mid+1`: go **right**
  - `mid > mid+1`: go **left**
- Can modify to return **highest peak** using linear scan

---

## ✨ Bonus: Highest Peak (Value-wise)

```cpp
int findHighestPeakElement(vector<int>& nums) {
    int n = nums.size();
    int peakIndex = -1;
    int maxPeak = INT_MIN;

    for (int i = 0; i < n; i++) {
        bool leftOK = (i == 0) || (nums[i] > nums[i - 1]);
        bool rightOK = (i == n - 1) || (nums[i] > nums[i + 1]);

        if (leftOK && rightOK && nums[i] > maxPeak) {
            maxPeak = nums[i];
            peakIndex = i;
        }
    }
    return peakIndex;
}
```

---

## 📚 Resources

- LeetCode #162: Find Peak Element
- Binary Search Explained Visually: [https://visualgo.net](https://visualgo.net/en/bst)
```
