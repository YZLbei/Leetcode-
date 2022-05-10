## DP

思路

> dp就是求出来每个位置左右最大高度，并保存

**dp是按照列计算雨水**

![42.接雨水3](https://buketyzl.oss-cn-qingdao.aliyuncs.com/20210223092732301.png)

注意

dp要初始化

```java
public int trap2(int[] height) {
    //左侧最大高度
    int []left = new int[height.length];

    //右侧
    int []right = new int[height.length];

    right[height.length-1] = height[height.length-1];
    left[0] = height[0];
    for (int i = 1; i < height.length; i++) {
        left[i] = Integer.max(left[i-1],height[i]);
    }
    for (int i = height.length-2; i >= 0;i--) {
        right[i] = Integer.max(right[i+1],height[i]);
    }

    for (int i = 0; i < height.length; i++) {
        System.out.println(left[i]);
    }
    int result = 0;
    for (int i = 0; i < height.length; i++) {
        int temp = Integer.min(left[i],right[i])-height[i];
        if (temp>0) {
            result +=temp;
        }
    }
    return result;

}
```

