Maximum Profit by Buying And Selling a Share Atmost twice in Java
Here, in this page we will discuss the program to find maximum profit by buying and selling a share atmost twice in Java .
In daily share trading, a buyer buys shares in the morning and sells them on the same day. If the trader is allowed to make at most 2 transactions in a day, whereas the second transaction can only start after the first one is complete Buy->Sell->Buy->Sell. We are given with stock prices throughout the day, We need to  find out the maximum profit that a share trader could have made.

Program to find Maximum profit by buying and selling a share atmost twice
Method 1 
Create an array say profit of size n and initialize all its value to 0.
Iterate price[] from right(n-1) to left(0) and update profit[i] such that profit[i] stores maximum profit achievable from one transaction in sub-array price[i..n-1].
Iterate price[] from left to right and update profit[i] such that profit[i] stores maximum profit such that profit[i] contains maximum achievable profit from two transactions in sub-array price[0..i].
After completing the iteration print value of profit[n-1].
Program to find Maximum profit by buying and selling a share atmost twice
Time-Space Complexities
Time - complexity : O(n) Space - complexity : O(n)
Code to find Maximum profit by buying and selling a share atmost twice in Java
Run
public
class Main {
    static int maxProfit(int price[], int n) {
        // Create profit array
        // and initialize it as 0
        int profit[] = new int[n];

        for (int i = 0; i < n; i++) profit[i] = 0;
        int max_price = price[n - 1];

        for (int i = n - 2; i >= 0; i--) {
            // max_price has maximum
            // of price[i..n-1]

            if (price[i] > max_price) max_price = price[i];
            profit[i] = Math.max(profit[i + 1], max_price - price[i]);
        }
        int min_price = price[0];
        for (int i = 1; i < n; i++) {

            // min_price is minimum
            // price in price[0..i]

            if (price[i] < min_price) min_price = price[i];
            profit[i] = Math.max(profit[i - 1], profit[i] + (price[i] - min_price));
        }

        int result = profit[n - 1];
        return result;
    }

    // Driver Code
    public
    static void main(String args[]) {
        int price[] = {2, 30, 15, 10, 8, 25, 80};
        int n = price.length;
        System.out.println("Maximum Profit = " + maxProfit(price, n));
    }
}
Maximum Profit = 100
Related Pages
Given an array which consists of only 0, 1 and 2

Move all the negative elements to one side of the array

Find the Union and Intersection of the two sorted arrays

Find Largest sum contiguous Subarray

Minimize the maximum difference between heights 

Method 2 
Initialize four variables for taking care of the first buy, first sell, second buy, second sell.
Set first buy and second buy as INT_MIN and first and second sell as 0.
This is to ensure to get profit from transactions.
Iterate through the array and return the second buy as it will store maximum profit.
Time-Space Complexities
Time - complexity : O(n) Space - complexity : O(1)
Run
public

class Main {

    static int maxtwobuysell(int arr[], int size) {

        int first_buy = Integer.MIN_VALUE;
        int first_sell = 0;

        int second_buy = Integer.MIN_VALUE;
        int second_sell = 0;

        for (int i = 0; i < size; i++) {
            first_buy = Math.max(first_buy, -arr[i]);
            first_sell = Math.max(first_sell, first_buy + arr[i]);

            second_buy = Math.max(second_buy, first_sell - arr[i]);
            second_sell = Math.max(second_sell, second_buy + arr[i]);
        }
        return second_sell;
    }

    public
    static void main(String[] args) {
        int arr[] = {2, 30, 15, 10, 8, 25, 80};
        int size = arr.length;
     System.out.print("Maximum Profit= "+maxtwobuysell(arr, size));
    }
}
Output
Maximum Profit = 100
