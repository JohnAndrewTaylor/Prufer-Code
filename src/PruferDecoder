/**
 * Outputs the list of edges that define a tree by its given Prufer code.
 *
 * @author John A. Taylor
 * @github github.com/JohnAndrewTaylor
 * @version 1.0
 * @date 15/5/2019
 */

//import java.util.Collections;
import java.util.LinkedList;
import java.util.Scanner;
import java.util.concurrent.TimeUnit;

public class PruferDecoder {

    public static void main(String[] args) {
        Scanner scan = new Scanner(System.in);
        LinkedList<Integer> code = new LinkedList<Integer>();
        String input = scan.nextLine();
        scan.close();
        // Time: O(n) with n entries in Prufer code
        for (String a :input.split(",")) {
            // Adding to a Linked List is O(1)
            code.add(Integer.parseInt(a));
        }

        long startTime = System.nanoTime();
        /**
         * Simply knowing the existence of a number in the Prufer code is needed
         * to create the leaf set. A boolean array would be spatially the most
         * optimal for this purpose. However, since we need to know about the
         * repetition of a number in the Prufer code during the decoding, an
         * integer array tracking the count of each number would eliminate the
         * need to search through the code's linked list, therefore improving
         * the time complexity.
         */
        int[] vertexSet = new int[code.size() + 2];
        LinkedList<Integer> leaf = new LinkedList<Integer>();

        // Time: O(n) with n entries in Prufer code
        for (Integer num: code) {
            vertexSet[num - 1] +=1;
        }
        // Time: O(n+2) with n entries in Prufer code
        for (int i = 1; i <= code.size() + 2; i++) {
            if (vertexSet[i - 1] == 0) {
                leaf.add(i);
            }
        }

        // Removes every entry in the code - Time: O(n) with n entries
        while (!code.isEmpty()) {
            int a = code.remove(); // O(1)
            vertexSet[a - 1]--;
            int b = leaf.remove(); // O(1)
            System.out.println(a + " - " + b); // Prints an edge
            // Must check for non-recurrence to add to the leaf list
            if (vertexSet[a - 1] == 0) {
                /**
                 * To keep the removal from the leaf linked list at O(1), the
                 * head of the list needs to be the minimal value. Searching for
                 * the minimum in every iteration would forgo this step,
                 * allowing it to use O(1) addition, but that is more likely to
                 * decrease efficiency since this section of the code will only
                 * occasionally be run. There are two simple ways to maintain
                 * the list in a sorted form: add the entry in its correct
                 * position or add it and then sort the whole list. The former
                 * method is used below by adding every element in the leaf list
                 * again and checking if the given number from the code needs to
                 * be added first. Since this iterates through every element, it
                 * runs at O(n), however n is expected to be quite small since
                 * the list of leafs should be much smaller than the original
                 * code's length. One very simple form of the latter method with
                 * time complexity O(n*log(n)) is described and provided in the
                 * paragraph comment below, but an alternative O(n) or better
                 * sorting algorithm could easily be implemented.
                 */

                LinkedList<Integer> leafSorted = new LinkedList<Integer>();
                //Boolean needed to ensure that the number is added exactly once
                boolean added = false;
                for (Integer num: leaf) {
                    // Adds boolean in between numbers
                    if (a < num && added == false) {
                        leafSorted.add(a);
                        added = true;
                    }
                    leafSorted.add(num);
                }
                // Number is added last if it is larger than any other in list
                if (added == false) {
                    leafSorted.add(a);
                }
                leaf = leafSorted;

                /**
                 * An alternative approach is to add the unrepeated number from
                 * the code and then sort the whole leaf linked list to ensure
                 * that the minimal value is always in the front so that it can
                 * be removed in O(1). According to
                 * documentation, the Collections sort method is a modified
                 * mergesort which guarantees O(n*log(n)) performance. Remember
                 * to import Collections for this approach.
                 *
                 * leaf.add(a);
                 * Collections.sort(leaf);
                 *
                 */
            }
        }

        // With this algorithm two joined vertices remain inside the leaf list
        System.out.println(leaf.remove() + " - " + leaf.remove());

        long endTime = System.nanoTime();
        System.out.println(endTime - startTime);
    }
}
