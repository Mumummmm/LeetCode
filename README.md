# LeetCode
# List
#605. Can Place Flowers 
#581. Shortest Unsorted Continous Subarray 
#566. Reshape the Matrix 
#624. Maximum Distance in Arrays 
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
**better solution:**
```
public class Solution {
    public int findUnsortedSubarray(int[] nums) {
        int n = nums.length, beg = -1, end = -2, min = nums[n-1], max = nums[0];
        for(int i=1;i<n;i++){
            max = Math.max(max,nums[i]);
            min = Math.min(min,nums[n-i-1]);
            if(nums[i]<max){
                end = i;
            }
            if(nums[n-i-1]>min){
                beg = n-i-1;
            }
        }
        return end-beg+1;
    }
}
```

### #566. Reshape the Matrix 

**Problem description:**
>In MATLAB, there is a very useful function called 'reshape', which can reshape a matrix into a new one with different size but keep its original data. 
You're given a matrix represented by a two-dimensional array, and two positive integers r and c representing the row number and column number of the wanted reshaped matrix, respectively.
The reshaped matrix need to be filled with all the elements of the original matrix in the same row-traversing order as they were. 
If the 'reshape' operation with given parameters is possible and legal, output the new reshaped matrix; Otherwise, output the original matrix. 

**solution:**
```
public class Solution {
    public int[][] matrixReshape(int[][] nums, int r, int c) {
        int m = nums.length, n = nums[0].length, tempr = 0, tempc = 0;
        if(m*n!=r*c){
            return nums;
        }
        int reshape[][] = new int[r][c];
        for(int i=0;i<r;i++){
            for(int j=0;j<c;j++){
                if(tempc<n){
                    reshape[i][j] = nums[tempr][tempc];
                    tempc++;
                }else{
                    tempr++;
                    tempc = 0;
                    reshape[i][j] = nums[tempr][tempc];
                    tempc++;
                }
            }
        }
        return reshape;
    }
}
```

### #624. Maximum Distance in Arrays 

**Problem description:**
>Given m arrays, and each array is sorted in ascending order. Now you can pick up two integers from two different arrays (each array picks one) and calculate the distance. We define the distance between two integers a and b to be their absolute difference |a-b|. Your task is to find the maximum distance. 

**solution:**
```
public class Solution {
    public int maxDistance(List<List<Integer>> arrays) {
        int result = Integer.MIN_VALUE;
        int max = arrays.get(0).get(arrays.get(0).size() - 1);
        int min = arrays.get(0).get(0);
        
        for (int i = 1; i < arrays.size(); i++) {
            result = Math.max(result, Math.abs(arrays.get(i).get(0) - max));
            result = Math.max(result, Math.abs(arrays.get(i).get(arrays.get(i).size() - 1) - min));
            max = Math.max(max, arrays.get(i).get(arrays.get(i).size() - 1));
            min = Math.min(min, arrays.get(i).get(0));
        }
        
        return result;
    }
}
```