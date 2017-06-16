# LeetCode
# List
#605. Can Place Flowers
#581. Shortest Unsorted Continous Subarray
# Detail
### #605. Can Place Flowers

**Problem description:**
>Suppose you have a long flowerbed in which some of the plots are planted and some are not. However, flowers cannot be planted in adjacent plots - they would compete for water and both would die.
Given a flowerbed (represented as an array containing 0 and 1, where 0 means empty and 1 means not empty), and a number n, return if n new flowers can be planted in it without violating the no-adjacent-flowers rule.

**solution:**
```
public class Solution {
    public boolean canPlaceFlowers(int[] flowerbed, int n) {
        int count = 0;
        boolean output = false;
        int countZero = 1;  //处理开头为0
        boolean beginCountZero = false;
        for(int flower = 0;flower<flowerbed.length && count < n;flower++){
            if(flowerbed[flower] == 1){
                if(beginCountZero && countZero-2>0){
                    count += ((countZero-3)/2+1);
                    beginCountZero = false;
                }
                countZero = 0;
            }else{
                beginCountZero = true;
                countZero++;
                //处理结尾为0
                if((flower+1) == flowerbed.length){
                    countZero++;
                    if(countZero-2>0){
                        count += ((countZero-3)/2+1);
                        beginCountZero = false;
                    }
                }
            }
        }
        if(count >= n){
            output = true;
        }
        return output;
    }
}
```

### #581. Shortest Unsorted Continous Subarray

**Problem description:**
>Given an integer array, you need to find one continuous subarray that if you only sort this subarray in ascending order, then the whole array will be sorted in ascending order, too. 
You need to find the shortest such subarray and output its length.

**solution:**
```
public class Solution {
    public int findUnsortedSubarray(int[] nums) {
        int l = nums.length, r = 0;
        for (int i = 0; i < nums.length - 1; i++) {
            for (int j = i + 1; j < nums.length; j++) {
                if (nums[j] < nums[i]) {
                    r = Math.max(r, j);
                    l = Math.min(l, i);
                }
            }
        }
        return r - l < 0 ? 0 : r - l + 1;
    }
}
```