*** Q1. How Will You Compare?

```
import java.util.Scanner;

class Comparator {

    // Method 1: Compare two integers
    public boolean compare(int a, int b) {
        return a == b;
    }

    // Method 2: Compare two strings
    public boolean compare(String a, String b) {
        if (a == null || b == null) {
            return false;
        }
        return a.equals(b);
    }

    // Method 3: Compare two integer arrays
    public boolean compare(int[] a, int[] b) {
        if (a == null || b == null) {
            return false;
        }
        if (a.length != b.length) {
            return false;
        }
        for (int i = 0; i < a.length; i++) {
            if (a[i] != b[i]) {
                return false;
            }
        }
        return true;
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        Comparator comp = new Comparator();
        
        int T = scanner.nextInt();  // Read number of test cases
        scanner.nextLine();  // Consume the newline character after T

        for (int i = 0; i < T; i++) {
            int comparisonType = scanner.nextInt();  // Read the comparison type
            scanner.nextLine();  // Consume the newline character after comparison type
            
            boolean result = false;
            switch (comparisonType) {
                case 1:
                    String str1 = scanner.nextLine();  // Read first string
                    String str2 = scanner.nextLine();  // Read second string
                    result = comp.compare(str1, str2);
                    break;
                    
                case 2:
                    int int1 = scanner.nextInt();  // Read first integer
                    int int2 = scanner.nextInt();  // Read second integer
                    result = comp.compare(int1, int2);
                    break;
                    
                case 3:
                    int n = scanner.nextInt();  // Read size of first array
                    int m = scanner.nextInt();  // Read size of second array
                    
                    int[] arr1 = new int[n];
                    int[] arr2 = new int[m];
                    
                    for (int j = 0; j < n; j++) {
                        arr1[j] = scanner.nextInt();  // Read elements of first array
                    }
                    for (int j = 0; j < m; j++) {
                        arr2[j] = scanner.nextInt();  // Read elements of second array
                    }
                    result = comp.compare(arr1, arr2);
                    break;
            }
            
            // Output result
            if (result) {
                System.out.println("Same");
            } else {
                System.out.println("Different");
            }
        }
        scanner.close();
    }
}

```


*** Q2. Java: Shape

```
// import java.io.*;
// import java.util.*;
// import java.text.*;
// import java.math.*;
// import java.util.regex.*;

// public class Solution {
//     public static void main(String args[] ) throws Exception {
//         /* Enter your code here. Read input from STDIN. Print output to STDOUT */
//     }
// }


import java.io.*;
import java.util.*;
import java.text.*;
import java.math.*;
import java.util.regex.*;

class Shape {
    public int length , breadth ;
    public Shape( int length , int breadth ) {
        this.length = length ;
        this.breadth = breadth ;
    }
    public void area() {
        System.out.print(length + " " + breadth);
    }
}

class Rectangle extends Shape {
    Rectangle(int l , int b) {
        super(l,b);
    }
    @Override
    public void area() {
        System.out.print("\n" + length*breadth);
    }
}

public class Solution {
    public static void main(String args[] ) throws Exception {
        Scanner sc = new Scanner(System.in);
        int l = sc.nextInt();
        int b = sc.nextInt();

        Shape shape = new Shape(l,b);
        shape.area();

        Shape rectangle = new Rectangle(l,b);
        rectangle.area();
    }
}
```



*** Q3. Java Static Analysis

** What is the output of the following Java code?
```
public class Test {
    public static void main(String[] args){
        int i = 010;
        int j = 07;
        System.out.println(i);
        System.out.println(j);
    }
}
```

8 7
10 7
Compilation fails with an error at line 3
Compilation fails with an error at line 5

Correct Answer: 8 7



*** Q4. Java Program Flow

**What is the output of the following program:

```
interface BaseI { void method(); }

class BaseC
{
   public void method()
   {
      System.out.println("Inside BaseC::method");
   }
}

class ImplC extends BaseC implements BaseI
{
   public static void main(String []s)
   {
      (new ImplC()).method();
   }
}
```
null
Compilation fails
Inside BaseC::method
None of the above

Correct Answer: Inside BaseC::method



*** Q.5 Static Code Analysis 5

**What will the output be?
```
try 
{
    Float f1 = new Float("3.0");
    int x = f1.intValue();
    byte b = f1.byteValue();
    double d = f1.doubleValue();
    System.out.println(x + b + d);
}
catch (NumberFormatException e) /* Line 9 */
{
    System.out.println("bad number"); /* Line 11 */
}

```

9.0
bad number
Compilation fails on line 9
Compilation fails on line 11

Correct Anser: 9.0



*** Q.6 Return Type

**What is Covariant return type?

**The overriding method can have derived type as the return type instead of the base type
**The overriding method can have base type as the return type instead of the derived type
**The return type is of the class type Covariant
**The return type is void

Correct Answer: The overriding method can have derived type as the return type instead of the base type
