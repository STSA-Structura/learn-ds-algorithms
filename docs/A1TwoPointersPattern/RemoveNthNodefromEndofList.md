# Remove Nth Node from End of List

Here is a refined review, explanation, and breakdown of your solution for "Remove Nth Node from End of List."

## Solution Overview

The task is to remove the `n`th node from the end of a singly linked list and return the head of the modified list. This solution uses a two-pointer technique, where one pointer (`right`) is advanced by `n` nodes first, and then both pointers (`right` and `left`) move together until `right` reaches the end. This allows `left` to land on the node just before the target node, making it possible to skip the target node with `left.next = left.next.next`.

### Code Structure and Explanation

1. **Class Definitions**:

   - `LinkedListNode`: Represents a node in the linked list with a `data` attribute and a `next` pointer to the next node.
   - `LinkedList`: Represents a singly linked list with helper methods to add nodes (`insertNodeAtHead`) and initialize the list from an array (`createLinkedList`).
   - `PrintList`: Contains a utility method to print the linked list in a readable format.

2. **Algorithm** (`removeNthLastNode` method in `RemoveNthNode` class):

   - **Step 1**: Move the `right` pointer `n` nodes forward from the head.
   - **Step 2**: If `right` reaches `null` after advancing `n` steps, it means we need to remove the head node (i.e., the list has exactly `n` nodes). In this case, we return `head.next` as the new head.
   - **Step 3**: Advance both `right` and `left` pointers until `right` reaches the end. At this point, `left.next` is the target node to remove.
   - **Step 4**: Remove the target node by adjusting `left.next` to `left.next.next`.

3. **Driver Code (main method)**:
   - Initializes multiple test cases with predefined lists and values of `n`.
   - For each test case, creates a linked list, removes the `n`th node from the end, and prints the modified list.

### Complete Code with Minor Enhancements

Here's a streamlined version of your solution with improved comments and formatting.

```java
// Node class for the linked list
class LinkedListNode {
    public int data;
    public LinkedListNode next;

    // Constructor to initialize node with data
    public LinkedListNode(int data) {
        this.data = data;
        this.next = null;
    }
}

// Template for the linked list
class LinkedList<T> {
    public LinkedListNode head;

    // Constructor to initialize an empty linked list
    public LinkedList() {
        this.head = null;
    }

    // Method to insert a node at the head of the list
    public void insertNodeAtHead(LinkedListNode node) {
        if (this.head == null) {
            this.head = node;
        } else {
            node.next = this.head;
            this.head = node;
        }
    }

    // Method to create the linked list from an integer array
    public void createLinkedList(int[] lst) {
        for (int i = lst.length - 1; i >= 0; i--) {
            LinkedListNode newNode = new LinkedListNode(lst[i]);
            insertNodeAtHead(newNode);
        }
    }
}

// Utility class to print the linked list
class PrintList {
    public static void printListWithForwardArrow(LinkedListNode head) {
        LinkedListNode temp = head;
        while (temp != null) {
            System.out.print(temp.data);
            temp = temp.next;
            if (temp != null) {
                System.out.print(" → ");
            }
        }
        System.out.println(" → null");
    }
}

// Main class containing the algorithm to remove the nth node from the end
class RemoveNthNode {

    // Method to remove the nth node from the end of the list
    public static LinkedListNode removeNthLastNode(LinkedListNode head, int n) {
        LinkedListNode right = head;
        LinkedListNode left = head;

        // Move `right` pointer `n` steps ahead
        for (int i = 0; i < n; i++) {
            right = right.next;
        }

        // If `right` is null, the head node is the one to be removed
        if (right == null) {
            return head.next;
        }

        // Move both pointers until `right` reaches the end
        while (right.next != null) {
            right = right.next;
            left = left.next;
        }

        // Remove the nth node from end
        left.next = left.next.next;

        return head;
    }

    // Driver code for testing the solution
    public static void main(String[] args) {
        int[][] inputs = {
            {23, 89, 10, 5, 67, 39, 70, 28},
            {34, 53, 6, 95, 38, 28, 17, 63, 16, 76},
            {288, 224, 275, 390, 4, 383, 330, 60, 193},
            {1, 2, 3, 4, 5, 6, 7, 8, 9},
            {69, 8, 49, 106, 116, 112, 104, 129, 39, 14, 27, 12}
        };

        int[] n = {4, 1, 6, 9, 11};

        // Process each test case
        for (int i = 0; i < inputs.length; i++) {
            LinkedList<Integer> inputLinkedList = new LinkedList<>();
            inputLinkedList.createLinkedList(inputs[i]);
            System.out.print((i + 1) + ". Linked List: ");
            PrintList.printListWithForwardArrow(inputLinkedList.head);
            System.out.println("n = " + n[i]);
            System.out.print("Updated Linked List: ");
            PrintList.printListWithForwardArrow(removeNthLastNode(inputLinkedList.head, n[i]));
            System.out.println(new String(new char[50]).replace('\0', '-'));
        }
    }
}
```

### Explanation of Enhancements

- **Comments and Clarity**: Added detailed comments for readability and to clarify the purpose of each method.
- **Refined Print Formatting**: Adjusted the arrow print method to ensure clarity in list structure.
- **Reusable Code**: Helper methods (`insertNodeAtHead`, `createLinkedList`, `printListWithForwardArrow`) make the code modular, easier to test, and reusable.

### Test Output

When executed, the program will print the initial and updated linked lists for each test case, along with the node number (`n`) to remove from the end.

Example Output (format varies by input):

```
1. Linked List: 23 → 89 → 10 → 5 → 67 → 39 → 70 → 28 → null
n = 4
Updated Linked List: 23 → 89 → 10 → 5 → 39 → 70 → 28 → null
--------------------------------------------------
...
```

### Complexity Analysis

- **Time Complexity**: \(O(k)\), where \(k\) is the number of nodes in the list, as it traverses the list a constant number of times.
- **Space Complexity**: \(O(1)\), since it operates in place with two pointers.

### Notes for Further Testing

Ensure to run edge cases such as:

- Removing the only node in a single-node list.
- Removing the first or last node in a list with multiple elements.
- Lists of varying lengths and different values of \(n\).

This solution handles cases effectively while maintaining simplicity and efficiency.