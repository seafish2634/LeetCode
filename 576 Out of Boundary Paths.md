# 576. Out of Boundary Paths

There is an `m x n` grid with a ball. The ball is initially at the position `[startRow, startColumn]`. You are allowed to move the ball to one of the four adjacent cells in the grid (possibly out of the grid crossing the grid boundary). You can apply **at most** `maxMove` moves to the ball.

Given the five integers `m`, `n`, `maxMove`, `startRow`, `startColumn`, return the number of paths to move the ball out of the grid boundary. Since the answer can be very large, return it **modulo** `109 + 7`.

# **Example 1:**

![Untitled](576%20Out%20of%20Boundary%20Paths%20494474f2129c404e87f44508e9a6bbac/Untitled.png)

```
Input: m = 2, n = 2, maxMove = 2, startRow = 0, startColumn = 0
Output: 6
```

# **Example 2:**

![Untitled](576%20Out%20of%20Boundary%20Paths%20494474f2129c404e87f44508e9a6bbac/Untitled%201.png)

```
Input: m = 1, n = 3, maxMove = 3, startRow = 0, startColumn = 1
Output: 12
```

**Constraints:**

- `1 <= m, n <= 50`
- `0 <= maxMove <= 50`
- `0 <= startRow < m`
- `0 <= startColumn < n`

## Code :

```cpp
**class Solution {
public:
    int mm, nn;
    int memo[50][50][51];
    int DIR[5] = {0, 1, 0, -1, 0};
    int findPaths(int m, int n, int maxMove, int startRow, int startColumn) {
        mm = m; nn = n;
        memset(memo, -1, sizeof(memo));
        return dp(startRow, startColumn, maxMove);
    }
    int dp(int r, int c, int maxMove) {
        if (r < 0 || r == mm || c < 0 || c == nn) return 1; 
        if (maxMove == 0) return 0;
        if (memo[r][c][maxMove] != -1) return memo[r][c][maxMove];
        int ans = 0;
        for (int i = 0; i < 4; ++i)
            ans = (ans + dp(r + DIR[i], c + DIR[i+1], maxMove - 1)) % 1000000007;
        return memo[r][c][maxMove] = ans;
    }
};**
```

# Solution :

## Why use DP ?

**because Maxmove( x ) will need to add ( x -1 )’s value for example : Maxmove( 2 ) = CurrentMove( 2 )  + Maxmove( 1 ), Maxmove( 3 ) = CurrentMove( 3 )  + Maxmove( 2 ).**

---

**—> so we need to use dp to solve it.**

---

**using global array memo[50][50][51] to store every position’s Maxmove.** 

**if reach boundary  ——> return 1.**

**if not reach             ——> using 4 direction to calculate how many ways to move to reach maxMove.**

**!! remember maxMove should minus 1 if it change its position !!**

**and result should % 1000000007  in order to prevent  overflow (the answer should be int but the answer of solution will return long long int, use this method will prevent RE).**

# 使用DP解

**Maxmove的答案會包含上一步的最大步數，舉例來說 : Maxmove( 2 ) = CurrentMove( 2 )  + Maxmove( 1 ), Maxmove( 3 ) = CurrentMove( 3 )  + Maxmove( 2 ) 。**

**開一個全域變數來儲存答案 memo[50][50][51]，兩個變數儲存m，n。**

**如果還沒到邊界   ———> 回傳上下左右的步數解(Maxmove應該-1)。**

**答案需要 % 1000000007 避免RE (因為題目需求是 int 而答案有可能會到long long int)。**