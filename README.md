# Merge Intervals
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
