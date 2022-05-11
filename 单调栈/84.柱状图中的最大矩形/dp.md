## [84. 柱状图中最大的矩形](https://leetcode.cn/problems/largest-rectangle-in-histogram/)

### DP（错误的思路）

五部曲

1. dp定义

   dp[i] [0]表示要height[i]的最大矩形

   dp[i] [1]表示不要height[i]的最大矩形,但是可能会勾勒矩形

   

2. 状态转移方程

   dp[i] [0] 

   - dp[i-1] [0]
   - - if（height[i]>height[i-1]) dp[i] [0]  = height[i]
     - else dp[i] [0] = dp[i-1] [0] +min0
   - dp[i-1] [1]
   - -  dp[i] [0]  = height[i]

   dp[i] [1] 

   - dp[i-1] [0]
   - - if（height[i]>height[i-1]) 
     - dp[i] [1]  = dp[i-1] [0]+min1
   - dp[i-1] [1]
   - -  dp[i] [0]  =  dp[i-1] [1]+min

3. 初始化

4. 遍历顺序

### dp正确的思路

跟接雨水类似

不同的是

- 这道题是求左边第一个更小，右边第一个更大；接雨水是求左边最大和右边最大
- 求的是下标，不是高度

相当于求出每一个位置，能勾勒出的最大矩形

```java
public int largestRectangleArea(int[] heights) {
        //左边第一个更小的下标
        int []minLeftIndex = new int[heights.length];

        //
        int[] minRightIndex = new int[heights.length];

        minLeftIndex[0] = -1;
        for (int i = 1; i < heights.length; i++) {
            int t=i-1;
            while(t>=0&&heights[t]>=heights[i]){
                t = minLeftIndex[t];
            }
            minLeftIndex[i] = t;
        }
        minRightIndex[heights.length-1] = heights.length;
        for (int i = heights.length-2; i>=0 ; i--) {
            int t=i+1;
            while(t<=heights.length-1&&heights[t]>=heights[i]){
                t = minRightIndex[t];
            }
            minRightIndex[i] = t;
        }

//        for (int i = 0; i < heights.length; i++) {
//            System.out.println(minRightIndex[i]);
//        }
        int result = 0;
        for (int i = 0; i < heights.length; i++) {
            //-2+1,因为minLeft和minRight都多算了1，要-1；因为要计算minleft到minRIgt之间，左闭右闭要+1
            result = Integer.max(result,heights[i]*(minRightIndex[i]-minLeftIndex[i]-1));
        }
        return result;
    }
```

