# 16Practical



public class tryheapsort {
    static void heapify(String[] arr, int n, int i) {
        int largest = i;
        int left = (2 * i) + 1;
        int right = (2 * i) + 2;

        if (left < n && arr[left].compareTo(arr[largest]) > 0) {
            largest = left;
        }
        if (right < n && arr[right].compareTo(arr[largest]) > 0) {
            largest = right;
        }
        if (largest != i) {
            String temp = arr[i];
            arr[i] = arr[largest];
            arr[largest] = temp;

        }
    }

    static void build_heap_bottom_up(String[] arr) {
        int n = arr.length;

        for (int i = n / 2 - 1; i >= 0; i--) {
            heapify(arr, n, i);

        }
    }

    static void heap_sort(String[] arr) {
        int n = arr.length;
        build_heap_bottom_up(arr);

        for (int i = n - 1; i > 0; i--) {
            String temp = arr[i];
            arr[i] = arr[0];
            arr[0] = temp;
            heapify(arr, i, 0);

        }
    }

    static void insert(String[] heap, String value) {
        int i = heap.length - 1;
        heap[i] = value;

        while (i > 0) {
            int parent = (i - 1) / 2;

            if (heap[parent].compareTo(heap[i]) < 0) {
                String temp = heap[parent];
                heap[parent] = heap[i];
                heap[i] = temp;
                i=parent;
            } else {
                break;

            }
        }
    }

    static void build_heap_top_down(String[] arr) {
        for (String word : arr) {
            insert(arr, word);
        }

    }

    static void heap_sort_top_down(String[] arr) {
        build_heap_top_down(arr);
        int n = arr.length;

        for (int i = n - 1; i > 0; i--) {
            String temp = arr[i];
            arr[i] = arr[0];
            arr[0] = temp;
            heapify(arr, i, 0);

        }
    }

    public static void main(String[] args){
    String[] words={ "apple","orange","banana","grape","cherry","mango","pear","peach","plum","melon"};

    System.out.println("Original: "+java.util.Arrays.toString(words));

    String[]words1=words.clone();
    heap_sort(words1);
    System.out.println("Bottom up sort: "+java.util.Arrays.toString(words1));

    String[]words2=words.clone();
    heap_sort_top_down(words2);
    System.out.println("Top down sort: "+java.util.Arrays.toString(words2));

        long start1 = System.nanoTime();

        String[] words1 = words.clone();
        heap_sort(words1);

        long end1 = System.nanoTime();
        long bottomUpTime = end1 - start1;

        long start2 = System.nanoTime();

        String[] words2 = words.clone();
        heap_sort_top_down(words2);

        long end2 = System.nanoTime();
        long topDownTime = end2 - start2;

        System.out.println("Bottom-up heap sort time: " + bottomUpTime + " ns");
        System.out.println("Top-down heap sort time: " + topDownTime + " ns");
    }
}
