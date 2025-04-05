# leetcode----502
IPO
//code in java
import java.util.*;

public class Solution {
    public int findMaximizedCapital(int k, int w, int[] profits, int[] capital) {
        // PriorityQueue to store projects based on profit (max heap)
        PriorityQueue<Integer> maxHeap = new PriorityQueue<>((a, b) -> b - a);
        
        // Array of project indices sorted by their capital requirement
        int n = profits.length;
        int[][] projects = new int[n][2];
        for (int i = 0; i < n; i++) {
            projects[i] = new int[]{capital[i], profits[i]};
        }
        Arrays.sort(projects, Comparator.comparingInt(a -> a[0]));

        int index = 0;
        for (int i = 0; i < k; i++) {
            // Add projects to maxHeap that can be done with the available capital
            while (index < n && projects[index][0] <= w) {
                maxHeap.offer(projects[index][1]);
                index++;
            }

            // If no projects are feasible, break
            if (maxHeap.isEmpty()) {
                break;
            }

            // Select the most profitable project
            w += maxHeap.poll();
        }

        return w;
    }
}
