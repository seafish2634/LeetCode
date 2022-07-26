# 240. Search a 2D Matrix II

Write an efficient algorithm that searches for a value `target` in an `m x n` integer matrix `matrix`. This matrix has the following properties:

- Integers in each row are sorted in ascending from left to right.
- Integers in each column are sorted in ascending from top to bottom.

**Example 1:**

![https://assets.leetcode.com/uploads/2020/11/24/searchgrid2.jpg](https://assets.leetcode.com/uploads/2020/11/24/searchgrid2.jpg)

```
Input: matrix = [[1,4,7,11,15],[2,5,8,12,19],[3,6,9,16,22],[10,13,14,17,24],[18,21,23,26,30]], target = 5
Output: true

```

**Example 2:**

![https://assets.leetcode.com/uploads/2020/11/24/searchgrid.jpg](https://assets.leetcode.com/uploads/2020/11/24/searchgrid.jpg)

```
Input: matrix = [[1,4,7,11,15],[2,5,8,12,19],[3,6,9,16,22],[10,13,14,17,24],[18,21,23,26,30]], target = 20
Output: false

```

**Constraints:**

- `m == matrix.length`
- `n == matrix[i].length`
- `1 <= n, m <= 300`
- `109 <= matrix[i][j] <= 109`
- All the integers in each row are **sorted** in ascending order.
- All the integers in each column are **sorted** in ascending order.
- `109 <= target <= 109`

### Code:

```cpp
**class Solution {
public:
    bool searchMatrix(vector<vector<int>>& ma, int t) {
        int c=0;
        for(int i=0;i<ma.size();++i)
        {
            int start=0,end=ma[0].size()-1;
            while(start<end)
            {
                
                int mid=(start+end-1)/2;
                if(ma[i][mid]<t)
                {
                    start=mid+1;
                }
                else if(ma[i][mid]>t)
                {
                    end=mid;
                }
                else
                    return 1;
                
            }
            if(ma[i][0]==t || ma[i][ma[0].size()-1]==t)return 1;
        }
        return false;
    } 
};**
```

## Solution:

**It looks like it can use brute force, then we will TLE.**

**so we have to use more effective way to search the number.**

**because they  are sorted in ascending ,so we can use binary search in every column.**