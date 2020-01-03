# Merge Intervals
## https://leetcode.com/problems/merge-intervals
Given a collection of intervals, merge all overlapping intervals.

```
Example 1:

Input: [[1,3],[2,6],[8,10],[15,18]]
Output: [[1,6],[8,10],[15,18]]
Explanation: Since intervals [1,3] and [2,6] overlaps, merge them into [1,6].

Example 2:

Input: [[1,4],[4,5]]
Output: [[1,5]]
Explanation: Intervals [1,4] and [4,5] are considered overlapping.

```
### Approach :
We can solve this problem by following below approach:
1. First sort all the intervals according to their start times.
2. Next iterate over the sorted intervals and handle the below 2 cases :
   
   1. If the start time of current interval is greater than or equal to the end time of the last interval in the list, this means that there is no overlap among the intervals and we don't need to merge intervals in this case. So we add the current interval to the output list as is.
   
   2. Otherwise, it means there is an overlap between intervals and in this case, we update the end time of the last interval in the list with the **maximum among last interval's end time and current interval's end time**

![Merge Intervals Scenarios](merge-intervals.PNG?raw=true "Merge Intervals Scenarios")

### Implementation

```java
public int[][] merge(int[][] intervals) {
    if(intervals == null || intervals.length <= 1) {
	return intervals;
    }
		
    Arrays.sort(intervals, (interval1, interval2) -> interval1[0] - interval2[0]);
		
    List<int[]> merged = new ArrayList<int[]>();
    for(int[] interval : intervals) {
	  if (merged.isEmpty() || merged.get(merged.size()-1)[1] < interval[0]) {
	           merged.add(interval);
	  } else {
             int lastMeetingEnd = merged.get(merged.size()-1)[1];
	     merged.get(merged.size()-1)[1] = Math.max(lastMeetingEnd, interval[1]);
	  }
    }
		
   return merged.toArray(new int[merged.size()][]);
}
```

** Implementation Tips  :flushed: **
toArray() is handy if you need to convert from list to array

### Complexity Analysis

**Time complexity : O(nlogn)**

Other than the sort invocation, we do a simple linear scan of the list, so the runtime is dominated by the O(nlogn) complexity of sorting.

**Space complexity : O(1) or O(n)**

If we can sort intervals in place, we do not need more than constant additional space. Otherwise, we must allocate linear space to store a copy of intervals and sort that.

## References :
https://leetcode.com/articles/merge-intervals

https://massivealgorithms.blogspot.com/2014/06/leetcode-merge-intervals.html

