
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
