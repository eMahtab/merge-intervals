# Merge Intervals

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
