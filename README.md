
# EX 4A Kadane's Algorithm - Dynamic Programming. 
## AIM:
To Write a Java program to solve the below problem using Kadane's Algorithm.
A solar company installs solar panels around a circular grid of n buildings. Each building either generates or consumes net energy, represented by integers (+ve for generated, -ve for consumed).

The company wants to find a contiguous sequence of buildings (possibly wrapping around from the end to the beginning) that maximizes the total net energy.

Write a program to compute the maximum net energy that can be collected from any contiguous block of buildings on the circular grid.

Input Format:
First line: Integer n (number of buildings)

Second line: n space-separated integers: net energy for each building

Output Format:
A single integer: Maximum net energy collectable from a contiguous block (wrapping allowed)

Constraints:
1 <= n <= 10^6
## Algorithm

1. Start the program and read the number of solar panels `n` and their energy values into an array.
2. Use Kadane’s algorithm (`kadane()`) to find the maximum subarray sum without wrapping around.
3. Calculate the total energy sum and use another Kadane’s algorithm (`kadaneMin()`) to find the minimum subarray sum.
4. Compute the maximum circular sum as `totalSum - minSubarraySum` and compare it with the non-circular maximum.
5. Print the greater value as the maximum solar energy that can be obtained.

## Program:
```
/*
Program to implement Reverse a String
Developed by: Vignesh M
Register Number: 212223240176
*/
import java.util.*;

public class SolarEnergyMaximizer {

    public static int maxCircularEnergy(int[] energy) {
        int maxKadane = kadane(energy); // Maximum subarray sum without wrapping
        int totalSum = 0;
        for (int num : energy) totalSum += num;

        // Find minimum subarray sum to calculate circular sum
        int minSubarraySum = kadaneMin(energy);
        int maxCircular = totalSum - minSubarraySum; // Maximum with wrapping

        // If all numbers are negative, maxCircular can be 0, so return maxKadane
        return maxCircular > 0 ? Math.max(maxKadane, maxCircular) : maxKadane;
    }

    // Standard Kadane's algorithm for max subarray sum
    private static int kadane(int[] arr) {
        int maxSoFar = arr[0], maxEndingHere = arr[0];
        for (int i = 1; i < arr.length; i++) {
            maxEndingHere = Math.max(arr[i], maxEndingHere + arr[i]);
            maxSoFar = Math.max(maxSoFar, maxEndingHere);
        }
        return maxSoFar;
    }

    // Kadane's algorithm for minimum subarray sum
    private static int kadaneMin(int[] arr) {
        int minSoFar = arr[0], minEndingHere = arr[0];
        for (int i = 1; i < arr.length; i++) {
            minEndingHere = Math.min(arr[i], minEndingHere + arr[i]);
            minSoFar = Math.min(minSoFar, minEndingHere);
        }
        return minSoFar;
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        int[] energy = new int[n];
        for (int i = 0; i < n; i++) {
            energy[i] = sc.nextInt();
        }
        System.out.println(maxCircularEnergy(energy));
    }
}


```

## Output:

<img width="425" height="234" alt="image" src="https://github.com/user-attachments/assets/22686834-fd7b-40ef-9110-e145238df6aa" />


## Result:
The program successfully Implemented and the output is verified. 



# EX 4B Frog Jump - Dynamic Programming.
## AIM:
To write a Java program to for given constraints.
A Frog Jump 1 or 2 steps at a time.
Problem Statement:

A frog is at the bottom of the stairs with n steps. It can jump either 1 or 2 steps at a time. Write a program to find the number of distinct ways the frog can reach the top (n-th step).

Input Format:

A single integer n (1 ≤ n ≤ 45) – number of steps.
 Output Format:

A single integer – number of distinct ways to reach step n.

## Algorithm

1. Start the program and read the integer `n` (number of steps) from the user.
2. If `n` equals 1, return 1; if `n` equals 2, return 2.
3. Initialize two variables: `first = 1` and `second = 2` to represent ways to reach steps 1 and 2.
4. Use a loop from 3 to `n`, updating `current = first + second`, then shift values (`first = second`, `second = current`).
5. After the loop ends, print the value of `current` as the total number of ways the frog can reach step `n`.
 

## Program:
```
/*
Program to implement Reverse a String
Developed by: Vignesh M
Register Number: 212223240176
*/
import java.util.Scanner;

public class FrogJump {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        int n = scanner.nextInt();
        scanner.close();

        System.out.println(countWays(n));
    }

    public static int countWays(int n) {
        if (n == 1) return 1;
        if (n == 2) return 2;

        int first = 1; // ways to reach step 1
        int second = 2; // ways to reach step 2
        int current = 0;

        for (int i = 3; i <= n; i++) {
            current = first + second; // ways to reach current step
            first = second;
            second = current;
        }

        return current;
    }
}

```

## Output:

<img width="354" height="194" alt="image" src="https://github.com/user-attachments/assets/ae308935-4cb9-482c-b8b8-131b47fed462" />


## Result:
The program successfully implemented and the expected output is verified.




# EX 4C Coin Change Problem - Dynamic Programming.
## AIM:
To write a Java program to for given constraints.
You are given an integer array coins representing coins of different denominations and an integer amount representing a total amount of money.

Return the fewest number of coins that you need to make up that amount. If that amount of money cannot be made up by any combination of the coins, return -1.

You may assume that you have an infinite number of each kind of coin.

## Algorithm

1. Read the coin denominations and target amount as input.
2. Initialize a `dp` array of size `amount + 1` with a large value (`amount + 1`), and set `dp[0] = 0`.
3. For each amount `i` from `1` to `amount`, iterate through all coin values.
4. If `i - coin >= 0`, update `dp[i] = min(dp[i], dp[i - coin] + 1)` to track the minimum coins needed.
5. After filling the `dp` array, print `dp[amount]` if it’s valid; otherwise, print `-1` if the amount cannot be formed.


## Program:
```
/*
Program to implement Reverse a String
Developed by: Vignesh M
Register Number: 212223240176
*/
import java.util.*;

public class Solution {
    public int coinChange(int[] coins, int amount) {
        int max = amount + 1;
        int[] dp = new int[amount + 1];
        Arrays.fill(dp, max);  // Initialize with a value greater than any possible answer
        dp[0] = 0;  // Base case: 0 coins needed to make amount 0

        for (int i = 1; i <= amount; i++) {
            for (int coin : coins) {
                if (i - coin >= 0) {
                    dp[i] = Math.min(dp[i], dp[i - coin] + 1);
                }
            }
        }

        return dp[amount] > amount ? -1 : dp[amount];
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        Solution solution = new Solution();

        String coinsLine = scanner.nextLine(); 
        String amountLine = scanner.nextLine();

        coinsLine = coinsLine.replaceAll("[^0-9,]", ""); 
        String[] coinsStr = coinsLine.split(",");
        int[] coins = new int[coinsStr.length];
        for (int i = 0; i < coinsStr.length; i++) {
            coins[i] = Integer.parseInt(coinsStr[i]);
        }

        int amount = Integer.parseInt(amountLine.replaceAll("[^0-9]", ""));
        int result = solution.coinChange(coins, amount);
        System.out.println(result);

        scanner.close();
    }
}

```

## Output:
<img width="381" height="233" alt="image" src="https://github.com/user-attachments/assets/5e89c89e-b032-4cbf-be3d-96755cc94f62" />



## Result:
The program successfully implemented and the expected output is verified.




# EX 4D Longest Common SubSequence - Dynamic Programming.
## AIM:
To write a Java program to for given constraints.
Given two strings text1 and text2, return the length of their longest common subsequence. If there is no common subsequence, return 0.
A subsequence of a string is a new string generated from the original string with some characters (can be none) deleted without changing the relative order of the remaining characters.

For example, "ace" is a subsequence of "abcde".
A common subsequence of two strings is a subsequence that is common to both strings.

Input: text1 = "abcde", text2 = "ace" 
Output: 3  
Explanation: The longest common subsequence is "ace" and its length is 3.
Constraints:

1 <= text1.length, text2.length <= 1000
text1 and text2 consist of only lowercase English characters.

## Algorithm
✅ **Procedure:**

1. **Input:**

   * Read two strings, `text1` and `text2`, from the user.

2. **Initialization:**

   * Let `m` = length of `text1` and `n` = length of `text2`.
   * Create a 2D array `dp[m+1][n+1]`, where `dp[i][j]` stores the length of the longest common subsequence (LCS) between `text1[0..i-1]` and `text2[0..j-1]`.

3. **Filling the DP Table:**

   * For each `i` from `1` to `m`:

     * For each `j` from `1` to `n`:

       * If characters match (`text1.charAt(i-1) == text2.charAt(j-1)`):
         → `dp[i][j] = 1 + dp[i-1][j-1]`
       * Else:
         → `dp[i][j] = max(dp[i-1][j], dp[i][j-1])`

4. **Result:**

   * The value `dp[m][n]` gives the **length of the longest common subsequence**.

5. **Output:**

   * Print the result:
     `"Length of Longest Common Subsequence: " + dp[m][n]`
  

## Program:
```
/*
Program to implement Reverse a String
Developed by: Vignesh M
Register Number: 212223240176
*/
import java.util.Scanner;

public class Solution {

    public int longestCommonSubsequence(String text1, String text2) {
        int m = text1.length();
        int n = text2.length();

        int[][] dp = new int[m + 1][n + 1]; // dp[i][j] = LCS of text1[0..i-1] & text2[0..j-1]

        // Fill dp table
        for (int i = 1; i <= m; i++) {
            for (int j = 1; j <= n; j++) {
                if (text1.charAt(i - 1) == text2.charAt(j - 1)) {
                    dp[i][j] = 1 + dp[i - 1][j - 1];
                } else {
                    dp[i][j] = Math.max(dp[i - 1][j], dp[i][j - 1]);
                }
            }
        }

        return dp[m][n];
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        Solution sol = new Solution();

        String text1 = sc.nextLine().replaceAll("\"", "");
        String text2 = sc.nextLine().replaceAll("\"", "");

        int lcsLength = sol.longestCommonSubsequence(text1, text2);
        System.out.println("Length of Longest Common Subsequence: " + lcsLength);

        sc.close();
    }
}

```

## Output:
<img width="833" height="255" alt="image" src="https://github.com/user-attachments/assets/f08d14f5-2d4e-454b-a4c0-ecbe868c1ad3" />



## Result:
The program successfully implemented and the expected output is verified.




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
Developed by: Vignesh M
Register Number: 212223240176
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



