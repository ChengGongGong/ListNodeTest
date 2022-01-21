# 动态规划
1. 动态规划问题的一般形式就是求最值，核心问题是穷举：把所有可行的答案穷举出来，在其中找最值

    1. 这类问题存在“重叠子问题”，如果暴力穷举的话效率会极其低下，所以需要「备忘录」或者「DP table」来优化穷举过程，避免不必要的计算。
    2. 具备“最优子结构”，通过子问题的最值得到原问题的最值,且子问题间必须互相独立。
    3. 列出正确的“状态转移方程”：
        明确 base case -> 明确「状态」-> 明确「选择」 -> 定义 dp 数组/函数的含义。
        
            初始化 base case
            dp[0][0][...] = base
            进行状态转移
            for 状态1 in 状态1的所有取值：
                for 状态2 in 状态2的所有取值：
                    for ...
                        dp[状态1][状态2][...] = 求最值(选择1，选择2...)
  2. dp数组的遍历方向
  
        1.正向遍历：
        
            int[][] dp = new int[m][n];
            for (int i = 0; i < m; i++)
                for (int j = 0; j < n; j++)
                    // 计算 dp[i][j]
        2.反向遍历：
        
            for (int i = m - 1; i >= 0; i--)
                for (int j = n - 1; j >= 0; j--)
                    // 计算 dp[i][j]
        3.斜向遍历：
         
            // 斜着遍历数组
            for (int l = 2; l <= n; l++) {
                for (int i = 0; i <= n - l; i++) {
                    int j = l + i - 1;
                    // 计算 dp[i][j]
                }
            }
        4.遍历的过程中，所需的状态必须是已经计算出来的；遍历的终点必须是存储结果的那个位置。
3. dp数组模板

    1. 一个一维的 dp 数组：
        
        int n = array.length;
        int[] dp = new int[n];
        
        for (int i = 1; i < n; i++) {
            for (int j = 0; j < i; j++) {
                dp[i] = 最值(dp[i], dp[j] + ...)
            }
        }
    
    2.一个二维的 dp 数组：
        
        int n = arr.length;
        int[][] dp = new dp[n][n];

        for (int i = 0; i < n; i++) {
            for (int j = 0; j < n; j++) {
                if (arr[i] == arr[j]) 
                    dp[i][j] = dp[i][j] + ...
                else
                    dp[i][j] = 最值(...)
            }
        }


