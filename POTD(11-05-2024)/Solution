
class Solution {
    
    class Pair implements Comparable<Pair> {
        double ratio; // The ratio of wage to quality
        int quality; // The quality of the worker

        
        public Pair(double d, int q) {
            this.ratio = d;
            this.quality = q;
        }

        @Override
        public int compareTo(Pair p2) {
            return Double.compare(this.ratio, p2.ratio);
        }
    }
  
    public double mincostToHireWorkers(int[] quality, int[] wage, int k) {
        int n = quality.length;
        Pair[] a = new Pair[n];

        // Populate the array with ratio and quality pairs
        for (int i = 0; i < n; i++) {
            double ratio = (double) wage[i] / (double) quality[i];
            a[i] = new Pair(ratio, quality[i]);
        }

        // Sort the array of pairs based on ratio
        Arrays.sort(a);

        // Priority queue to maintain top k qualities in reverse order
        PriorityQueue<Integer> pq = new PriorityQueue<>(Collections.reverseOrder());

        // Variable to store the minimum cost
        double ans = Double.MAX_VALUE;
        int totalQuality = 0;

        for (Pair p : a) {
            double ratio = p.ratio; // Get the ratio of the current pair

            // Update the total quality and add current quality to priority queue
            totalQuality += p.quality;
            pq.add(p.quality);

            // If the size of the priority queue exceeds k, remove the worker with maximum quality
            if (pq.size() > k) {
                totalQuality -= pq.poll();
            }

            // If the size of the priority queue is equal to k, calculate the minimum cost
            if (pq.size() == k) {
                ans = Math.min(ans, totalQuality * ratio);
            }
        }
        return ans; // Return the minimum cost
    }
}
