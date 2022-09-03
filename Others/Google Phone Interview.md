# Google Phone Interview

https://medium.com/@gupta.samriti1991/google-phone-interview-fb0ba544a48d

Last year I gave google telephonic interview. The question was pretty simple I solved it within 5mins but that was not all. When interviewer asked me to improve its time average complexity suddenly that became the turning point of the interview. At first glance all the sometimes questions seems pretty simple but after this interview, it totally changed my perspective how I prepare and approach the problem. Now, while solving questions on leetcode, I always check for the best solution and check for all the weird solution even if its improve the average case.

Question

Given an integer array nums and an integer k, return the kth largest element in the array.

Solution-1

The obvious solution will be sorting and what’s better than priority queue in this case. That will make out worst and average case to be O(nLogn)

class Solution {
  public int findKthLargest(int[] nums, int k) {
 
     PriorityQueue<Integer> pq = new PriorityQueue<Integer>((first ,second) -> Integer.compare(first, second));
 
     for(int num : nums){
         pq.add(num);
         if(pq.size() > k)
             pq.poll();
     }
 
     return pq.poll();
  }
}
But Here comes the twist, can you bring it’s average case to O(n)??

.

.

.

Solution-2

All the kth problem that I earlier used to solve using priority queue, I figured out they can be solved using quicksort also. Using Quicksort time complexity for worst case is O(n²) but for average case it is O(n).

class Solution {
   public int findKthLargest(int[] nums, int k) {
      return quickSelect(nums, 0, nums.length-1, k);
   }
 
   private int quickSelect(int[] nums, int start, int end, int k){
       if(start == end)
           return nums[start];
       int pivot = nums[(start+end)/2];
       int left = start, right = end;
       while(left<=right){
            while(left<=right && nums[left]>pivot){
                 left++;
            }
       while(left<=right && nums[right]<pivot){
            right--;
       }
       if(left<=right){
            int tmp = nums[left];
            nums[left] = nums[right];
            nums[right] = tmp;
            left++;
            right--;
        }
   }
   if(right-start+1>=k){
        return quickSelect(nums, start, right, k);
   }
   if(left-start+1<=k)
        return quickSelect(nums, left, end, k-(left-start));
   return nums[right+1];
 }
}
Similarly, for all the Kth problem can be solved using quicksort also. Some sample problems are given below:

Given an integer array nums and an integer k, return the k most frequent elements. You may return the answer in any order.
Given an array of points where points[i] = [xi, yi] represents a point on the X-Y plane and an integer k, return the k closest points to the origin (0, 0).

https://leetcode.com/problems/kth-largest-element-in-an-array/