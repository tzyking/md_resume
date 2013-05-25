------

###Recursion  

####String permutation:

```java
/*************************************************************************
 *  Compilation:  javac Permutations.java
 *  Execution:    java Permutations N
 *  
 *  Enumerates all permutations on N elements.
 *  Two different approaches are included.
 *
 *  % java Permutations 3
 *  abc
 *  acb
 *  bac 
 *  bca
 *  cab
 *  cba
 *
 *************************************************************************/

public class Permutations {

    // print N! permutation of the characters of the string s (in order)
    public  static void perm1(String s) { perm1("", s); }
    private static void perm1(String prefix, String s) {
        int N = s.length();
        if (N == 0) System.out.println(prefix);
        else {
            for (int i = 0; i < N; i++)
               perm1(prefix + s.charAt(i), s.substring(0, i) + s.substring(i+1, N));
        }

    }

    // print N! permutation of the elements of array a (not in order)
    public static void perm2(String s) {
       int N = s.length();
       char[] a = new char[N];
       for (int i = 0; i < N; i++)
           a[i] = s.charAt(i);
       perm2(a, N);
    }

    private static void perm2(char[] a, int n) {
        if (n == 1) {
            System.out.println(a);
            return;
        }
        for (int i = 0; i < n; i++) {
            swap(a, i, n-1);
            perm2(a, n-1);
            swap(a, i, n-1);
        }
    }  

    // swap the characters at indices i and j
    private static void swap(char[] a, int i, int j) {
        char c;
        c = a[i]; a[i] = a[j]; a[j] = c;
    }



    public static void main(String[] args) {
       int N = 7;
       String alphabet = "abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ";
       String elements = alphabet.substring(0, N);
       perm1(elements);
       System.out.println();
       perm2(elements);
    }
}


/*************************************************************************
 *  Compilation:  javac PermutationsK.java
 *  Execution:    java PermutationsK N k
 *  
 *  Enumerates all permutations of size k chosen from N elements.
 *
 *  % java PermutationsK 4 2 | sort
 *  ab
 *  ac
 *  ad
 *  ba 
 *  bc
 *  bd
 *  ca
 *  cb
 *  cd
 *  da
 *  db 
 *  dc 
 *
 *  Limitations
 *  -----------
 *    *  Assumes N <= 52
 *
 *************************************************************************/

public class PermutationsK {

    public static void choose(char[] a, int R) { enumerate(a, a.length, R); }

    private static void enumerate(char[] a, int n, int r) {
        if (r == 0) {
            for (int i = n; i < a.length; i++)
                System.out.print(a[i]);
            System.out.println();
            return;
        }
        for (int i = 0; i < n; i++) {
            swap(a, i, n-1);
            enumerate(a, n-1, r-1);
            swap(a, i, n-1);
         }
    }  

    // helper function that swaps a[i] and a[j]
    public static void swap(char[] a, int i, int j) {
        char temp = a[i];
        a[i] = a[j];
        a[j] = temp;
    }


    // sample client
    public static void main(String[] args) {
        int N = Integer.parseInt(args[0]);
        int k = Integer.parseInt(args[1]);
        String elements = "abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ";

        char[] a = new char[N];
        for (int i = 0; i < N; i++)
            a[i] = elements.charAt(i);
        choose(a, k);
    }

}



```   

------