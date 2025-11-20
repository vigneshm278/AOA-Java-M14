
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
Developed by: K ABHINESWAR REDDY
Register Number: 212223040084
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
