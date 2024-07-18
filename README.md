# number-of-good-leaf-nodes-pairs
class Solution {
    public int countPairs(TreeNode root, int distance) {
       int[] result = new int[1];
        dfs(root, distance, result);
        return result[0];
    }

    private List<Integer> dfs(TreeNode node, int distance, int[] result) {
        List<Integer> distances = new ArrayList<>();

        if (node == null) {
            return distances;
        }

        if (node.left == null && node.right == null) {
            distances.add(1); // Distance from leaf to itself is 1
            return distances;
        }

        List<Integer> leftDistances = dfs(node.left, distance, result);
        List<Integer> rightDistances = dfs(node.right, distance, result);

        for (int ld : leftDistances) {
            for (int rd : rightDistances) {
                if (ld + rd <= distance) {
                    result[0]++;
                }
            }
        }

        for (int ld : leftDistances) {
            if (ld + 1 < distance) {
                distances.add(ld + 1);
            }
        }

        for (int rd : rightDistances) {
            if (rd + 1 < distance) {
                distances.add(rd + 1);
            }
        }

        return distances;  
    }
}
