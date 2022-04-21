回溯法和dp求排列的区别
只求个数用DP
把所有排列组合的情况列出用回溯
public int combinationSum4(int[] nums, int target) {
        int []dp =new int[target+1];
        dp [0]  =1;
        for (int i = 0; i<=target ; i++) {
            for (int j = 0; j < nums.length; j++) {
                if (i>=nums[j])
                    dp[i] +=dp[i-nums[j]];
            }
        }
        return dp[target];
    }
