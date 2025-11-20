
# EX 4E Longest Increasing Subsequence - Dynamic Programming.
## AIM:
To write a Java program to for given constraints.
Given an integer array nums, return the length of the longest strictly increasing subsequence.
Example 1:
Input: nums = [10,9,2,5,3,7,101,18]
Output: 4
Explanation: The longest increasing subsequence is [2,3,7,101], therefore the length is 4.
## Algorithm

1. **Input:**

   * Read the integer `n` (size of array).
   * Read `n` integers into the array `nums`.

2. **Initialization:**

   * Create an array `dp[n]`, where `dp[i]` stores the **length of the longest increasing subsequence (LIS)** ending at index `i`.
   * Initialize all values of `dp` to `1`, since each element is an LIS of length `1` by itself.
   * Initialize `maxLen = 1` to keep track of the overall maximum LIS length.

3. **Dynamic Programming Logic:**

   * For each element `nums[i]` (from index `1` to `n-1`):

     * Compare it with all previous elements `nums[j]` (where `j < i`).
     * If `nums[i] > nums[j]`, it means we can extend the subsequence ending at `j`.
       → Update `dp[i] = max(dp[i], dp[j] + 1)`
   * After each iteration, update `maxLen = max(maxLen, dp[i])`.

4. **Output:**

   * Print `maxLen`, which represents the **length of the longest increasing subsequence**.
 

## Program:
```
/*
Program to implement Reverse a String
Developed by: K ABHINESWAR REDDY
Register Number: 212223040084
*/
import java.util.*;

public class LongestIncreasingSubsequence {

    public static int lengthOfLIS(int[] nums) {
        if (nums == null || nums.length == 0) return 0;

        int n = nums.length;
        int[] dp = new int[n];  // dp[i] = length of LIS ending at nums[i]
        Arrays.fill(dp, 1);     // Each element is a LIS of length 1 by itself

        int maxLen = 1;

        for (int i = 1; i < n; i++) {
            for (int j = 0; j < i; j++) {
                if (nums[i] > nums[j]) {
                    dp[i] = Math.max(dp[i], dp[j] + 1);
                }
            }
            maxLen = Math.max(maxLen, dp[i]);
        }

        return maxLen;
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        int n = scanner.nextInt();
        int[] nums = new int[n];

        for (int i = 0; i < n; i++) {
            nums[i] = scanner.nextInt();
        }

        int result = lengthOfLIS(nums);
        System.out.println("Length of Longest Increasing Subsequence: " + result);

        scanner.close();
    }
}

```

## Output:
<img width="812" height="257" alt="image" src="https://github.com/user-attachments/assets/520c0acf-b436-422b-9aff-b9e07ce4377b" />



## Result:
The program successfully implemented and the expected output is verified.
