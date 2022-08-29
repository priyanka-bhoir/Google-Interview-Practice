# 121. Best Time to Buy and Sell Stock
 
 `` Problem Statement
 You are given an array prices where prices[i] is the price of a given stock on the ith day.

You want to maximize your profit by choosing a single day to buy one stock and choosing a different day in the future to sell that stock.

Return the maximum profit you can achieve from this transaction. If you cannot achieve any profit, return 0.

 ``
https://leetcode.com/problems/best-time-to-buy-and-sell-stock/

## Solution

Remember one rule :- You can only buy one time & sell one time

So, if buy at 7 & sell at any time in the future, we'll face loss. Because buying price is way higher then selling price available we have

Now, I have seen a dip & I buy at 1 & sell at 5 my overall profit will be 5 - 1 = 4

But what if, I had buy at 1 & sell at 6 my profit will be 6 - 1 = 5. Which is greater then my overall profit. So, i will update my overall profit with new value.

Now we have done as further we don't have any higher point to sell. We will return our answer.

----------------------------------------

class Solution {
    public int maxProfit(int[] prices) {
        int lsf = Integer.MAX_VALUE;
        int op = 0;
        int pist = 0;
        
        for(int i = 0; i < prices.length; i++){
            if(prices[i] < lsf){
                lsf = prices[i];
            }
            pist = prices[i] - lsf;
            if(op < pist){
                op = pist;
            }
        }
        return op;
    }
}


---------------------------------------------

class Solution {
    public int maxProfit(int[] prices) {
        int buy=Integer.MAX_VALUE,sell=0;
        for(int i=0;i<prices.length;i++){
            buy=Math.min(buy,prices[i]);
            sell=Math.max(sell,prices[i]-buy);
        }
       return sell;
    }
}

-------------------------------------------------


public int maxProfit(int[] prices) {
        int profit = 0;
        int len = prices.length;
        int iBuy = 0; // index when buying
        for(int i=0;i<len;i++){
            if(prices[iBuy] > prices[i]) iBuy = i;
            profit = Math.max(profit, prices[i] - prices[iBuy]);
        }
        return profit;
    }


