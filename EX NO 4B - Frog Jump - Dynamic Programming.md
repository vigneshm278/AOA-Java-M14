
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
Developed by: K ABHINESWAR REDDY
Register Number:  212223040084
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
