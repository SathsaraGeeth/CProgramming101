# CProgramming101

## 0. Introduction
C is a general purpose, compiled language. It is simple yet powerful and one of the most widely used programming languages. It works closely with hardware, offering efficient and low level access to system resources.

### 0.1. Hello World

```c
#include <stdio.h> // this include directive makes sure that we can use the methods in stdio
int main(){
    printf("Hello World");
    return 0; // number 0 indicates that the program ran correctly if it is greater that it means the program failed
}
```

### 0.2. Remarks
1. logical operations:
    1. || - OR
    2. && - AND
    3.  ^ - XOR
2. comparisons:
<, >, ==, >=, <=
3. operations:
++, --

## 1. Computer Memory, Data Types, and Variables

### 1.0. Basic Data Types
1. Integers - char, int, short, long, long long
2. Unsinged integers - unsigned char, unsigned int, unsigned short, unsigned long, unsigned long long
3. Real numbers - double, float
4. Structures - struct

###### Remarks:
1. There is no boolean type in C, we usually define like following:
```c
#define BOOL char
#define FALSE 0
#define TRUE 1
```
2. The ranges of some types depends on the computer.

### 1.1. Variables
When we create a varaible a memory address is assigned to that variable. And the data is stored at the memory address.

###### Syntax:
```c
int a = 2;
char b; // we can define a variable without initializing
```

##### Pointers
A pointer is a type of integer variable that hold the memory address of a data instead of the memory address of the actuat data itself.

###### Syntax:
- The *pointer_var prefix indicates that pointer_var is a pointer variable.
- &a retrieves the memory address of the variable a.
- *pointer_var, known as the dereferencing operator, accesses the actual data the pointer refers to, rather than the memory address it holds.

```c
int a = 2;
int * pointer_to_a = &a; // * operator tells that 'pointer_to_a' is a pointer variable and '&' operator gives the memory address of 'a'
*pointer_to_a += 1; //increase the value of a by 1 (now a == 3)
```

##### Pointer arithmatics
Since pointers are integer variables we can perform ++/--/+/- with non-negative interges and also we perform arithmatic between pointers.

##### Arrays
An array is just a pointer, which points to the first element. Where the each consequetive element have the memory address one more than the previous one. Arrays can hold just one type of elements (ina contaiguusly allocated emmory block), but since the sequential nature of the memory (just described) accessing if a specific element is efficient.

###### Syntax: 
```c
/* Example - arrays */
int nums[2]; // defining an array of of 2 integers
/* populating elements */
nums[0] = 1;
nums[1] = 2;
nums[2] = 3;
printf(nums[1]); // accessing second element of array nums
```
```c
/* Example - mulit dimensional arrays */
int matrix[][3] = {{1, 2, 3}, {4, 5, 6}, {7, 8, 9}}; // definition and initiating of array matrix of integers. note that the complier can figureout that matrix[][3] == matrix[3][3]
printf(matrix[1][2]); // accessing third element of second sub array of array matrix
```
```c
/* Example - pointers & arrays */
int * pt = &nums; // same as int * pt = &nums[0]
printf(*(pt + 1)); // pointer arithmatic. same as printf(nums[1])
```

##### Strings
A string is just an array of char, where we add a ```'\0'``` to mark the end of string.

###### Syntax:
```c
* text = "Hello World"; // to define simple strings with pointer notation - with this method strings are read only
text[] = "Hello World"; // define as a local char array - so we can manipulate strings. Note that fiugre out that text[] == text[12]
```

###### Some Standard Library Methods for Strings
1. ```strlen(string)``` - returns the length.
```c
int len = strlen(text); // length of the string
printf("The text: %s has %d characters.\n", text, len);
```
2. ```strncmp(string1, string2, max_cmp_len)``` - returns number 0 if string1, string2 are equal up untill the max_cmp_len and a different number otherwise. (strcmp is an another unsafe method to do the same).
3. ```strncat(src_str, dest_str, max_chars_append)``` - appends first n chars of src_str to dest_src where n = min(n, length(src_str)).

###### Scope of a Variable
- Scope is the region in where a variable is accessible. In C, scope depends on where the variable is declared.
    1. Local Scope:
        - A variable defined inside a function or a block (a ```{}```) has the scope of that funciton or the block.
    2. Global Scope:
        - A variable defined outside every function has the scope of entire file.
    3. Block Scope:
        - A variable defined inside a block (ex: for, while, if) has the scope of that particular block.
    4. Function Scope:
        - In C lables (used with ```goto```) has the scope of function they are defined.

- Static Variables: by adding static keyword in prefix
    1. Local Static Variable:
        - When declared inside a staic variable retians its value between function calls but scoped to that function.
    2. Global Static Variables:
        - When declared outside of every function a staic variable has the scope to the file containg it, i.e., can't accessed from another file eventhough included.

### 1.2. User Defined Data Types

##### Structures
- Structures are user defined data types that allows to group together several vaiables(called members/fields) (can be different types).
- We can use them to pass in/out multiple arguments to functions and for data sturctures/
- We can access memebers using the dot ```.``` notations, or using ```->``` if pointer.
- typedef keyword

###### Syntax:
```c
struct StructName {
    type member1;
    type member2;
    // ... other members
};
```
```c
/* Example */
#include <stdio.h>
// Define a structure to represent a point in 2D space
struct Point {
    int x;
    int y;
};
int main() {
    // Declare a variable of type struct Point
    struct Point p1;

    // Assign values to the members of the structure
    p1.x = 5;
    p1.y = 10;

    // Access and print the members of the structure
    printf("Point p1: (%d, %d)\n", p1.x, p1.y);

    return 0;
}
```
```c
/* Example - structures with pointers */
#include <stdio.h>

struct Point {
    int x;
    int y;
};

int main() {
    struct Point p1 = {5, 10};
    struct Point *p2 = &p1;  // Pointer to the structure

    // Access members via the pointer (here p2->x == (*p2).x)
    printf("Point p2: (%d, %d)\n", p2->x, p2->y);

    return 0;
}
```
```c
/* Example - typedef keyword */
#include <stdio.h>

typedef struct {
    int x;
    int y;
} Point;  // Alias for struct definition

int main() {
    Point p1;  // Use 'Point' instead of 'struct Point'
    p1.x = 5;
    p1.y = 10;

    printf("Point p1: (%d, %d)\n", p1.x, p1.y);
    return 0;
}
```

##### Union
- A user defined data type that allows to store different types of data in a same memory location.
- Similar to structures but the difference is in structures for eaxh member allocates a different memory as while in union allocates a single memory location for all the members.

--  todo  --

##### Enum
-- todo --

### 1.3. Dynamic Memory Allocation
Dynamic memory allocation allows a program to request memory at run time instead of at compile time and manage it explicitly. Useful when they memory needed for a data is not known beforehand. (for instance when defining a array whom size we don't beforehand). 
- To archive this we use the following functions defined in  stlib header.
    1. ```malloc``` - Memory allocaton
        - Allocates a block of memory of a specified size un bytes and returns a pointer to the begining of the block. And the memory is uninitialized.
        - Syntax:
            ```c
            void* malloc(size_t size);
            ```
        - Example:
            ```c
            int *arr = (int *)malloc(10 * sizeof(int)); // Allocates memory for 10 integers
            if (arr == NULL) {
                printf("Memory allocation failed!\n");
            }
            
            // Remarks:
            /* Functions like malloc and calloc return a void * (a generic pointer that can point to any type of data). Since C is strongly typed, you need to cast this void * to the desired type. */
            /* In C, size_t is an unsigned integer type used to represent sizes and lengths, such as the number of bytes in a block of memory. It is defined in the <stddef.h> and <stdlib.h> headers. */
            /* sizeof is not actual function the compiler interprets it it to the memory size. */
            /* Always check for NULL: Functions like malloc and calloc return NULL if memory allocation fails. */
            ```
    2. ```calloc``` - Contagious allocation
        - Allocates memory for an array of elements, initializes all bits to zero, and returns a pointer to the allocated memory.
        - Syntax:
            ```c
            void* calloc(size_t num, size_t size);
            ```
        - Example:
            ```c
            int *arr = (int *)calloc(10, sizeof(int)); // Allocates and zeroes memory for 10 integers
            if (arr == NULL) {
                printf("Memory allocation failed!\n");
            }
            ```
    3. ```realloc``` - Reallocate memory
        - Resizes a previously allocated memory block to a new size. It may move the memory block to a new location if necessary.
        - Syntax:
            ```c
            void* realloc(void *ptr, size_t new_size);
            ```
        - Example:
            ```c
            arr = (int *)realloc(arr, 20 * sizeof(int)); // Resizes memory to hold 20 integers
            if (arr == NULL) {
                printf("Memory reallocation failed!\n");
            }
            ```
    4. ```free``` - Deallocate memory
        - Frees the memory previously allocated with malloc, calloc, or realloc. But does't delete the variable.
        - Syntax:
            ```c
            void free(void *ptr);
            ```
        - Example:
            ```c
            free(arr); // Deallocates memory
            arr = NULL; // Good practice to avoid dangling pointers
            
            // Reamrks:
            /* Dangaling pointers: Always set a pointer to NULL after freeing it to avoid accessing freed memory. */
            /* Memory leaks: Forgetting to free allocated memory can lead to memory leaks, which can degrade program performance. */
            ```
##### Examples:
```c
typedef struct {
    char * name;
    int age;
} person;

int main(){
    person * myperson = (person *) malloc(sizeof(person));
    myperson->name = "John";
    myperson->age = 27;
    free(myperson);
}
```
```c
#include <stdio.h>
#include <stdlib.h>

int main() {
    size_t num_elements = 5; // Define a size_t variable for the number of elements

    // Allocate memory dynamically for an array of integers
    int *arr = (int *)malloc(num_elements * sizeof(int));
    if (arr == NULL) {
        printf("Memory allocation failed!\n");
        return 1;
    }

    // Initialize and print the array
    for (size_t i = 0; i < num_elements; i++) {
        arr[i] = i + 1;
        printf("arr[%zu] = %d\n", i, arr[i]); // Use %zu for size_t
    }

    free(arr); // Free allocated memory
    return 0;
}
```

### 1.4. Bitmasks
--  todo  --

## 2. Control Structures

### 2.1. Selections

#### 1. ```if, else if, and else```
- Can used to execute different statements by evealuating conditions

###### Syntax:
```c
if (condition_1){
/* executes if condition_1 is true */
}
else if (condition_2){
    /* executes if condition_1 is false and if condition_1 is true */
}
else {
    /* executes if condition_1 is false and if condition_1 is false */
}
```

#### 2. ```switch case```
-- todo --

### 2. Loops - ```for```

###### Syntax:
```c
for (initialization (optional); condition (loop while this is true); operation (performed at the end of each iteration)) {
    /* statements go here */
}
```
```c
/* Example - prints 0, 1, 2 in newlines */
for (int i = 0; i < 3; i++){
    printf(i, '\n');
}
```

### 3. Loop - ```while```

###### Syntax:
```c
while (conditions){
    /* executes if condition(s) evaluates true */
    /* statements go here */
}
```

###### Remarks:
1. Loop derivatives:
    1.  continue - "forces to go to the next operation"
    2. break - "breaks out the loop"
2. do while
3. Loops are useful when iterating over sequential data (for insatance arrays with of pointer/or index)
4. Bad implementation of loops can leads to infinite loops

## 3. Abstraction, Encapsulating, and Reusalbulity
- In C functions provide abstraction by hiding implementation details and encapsulating by restricting direct acess to some components (ex: limiting variable scope) and enable reusable modular codes.
- In C functions recive either a fixed or varying amount arguments, and can return only one no value.
- In C arguments are copied by value to function so we can't chage/mutate the their value outside of scope of the function. If we want to archive that we can pass pointers to the functions instead.
- In C function can either declared first and implement later using a header file or in the begin in C file, or can implement in the order of use.
- In C, the main function is necessary as the entry point for execution, while other functions are optional.

###### Syntax:
```c
return_type function_name(parameter_type1 parameter1, parameter_type2 parameter2, ...); // function decleartion
return_type function_name(parameter_type1 parameter1, parameter_type2 parameter2, ...){
    /* function implementations */
    return ret; // void functions return nothing
}
```

###### Remark:
- By default functions are global in C, but if we decalred a fucntion as static (sytax: adding a static keyword prefix to the return_type). Staic function are cannot be accesible outside the function (in contrast to global) even if the file in included in another file.

#### Funciton Pointers:

###### Syntax:
- ```char* (*pf)(int*)```:
    1. ```char*``` means we return pointer to a ```char``` variable
    2. ```(*pf)``` means ```*pf``` is a function pointer. (```pf``` is the pointer, ```*pf``` is the function).
    3. ```int*``` means function arguments is a ```int``` variable
```c
/* Example - an use of function pointers */
#include <stdio.h>
#include <stdlib.h>

// Comparison function
int cmp(const void *a, const void *b) {
    return (*(int*)a - *(int*)b);  // Compare integers
}

int main() {
    int arr[] = {5, 3, 8, 1, 2};
    int n = sizeof(arr) / sizeof(arr[0]);

    // Declare a function pointer and assign the cmp function to it
    int (*cmp_ptr)(const void*, const void*) = cmp;

    // Sort the array using the cmp function via the function pointer
    qsort(arr, n, sizeof(int), cmp_ptr);

    // Print the sorted array
    for (int i = 0; i < n; i++) {
        printf("%d ", arr[i]);
    }

    return 0;
}
```

##### References:
1. [Learn C](https://www.learn-c.org/)
2. B. W. Kernighan and D. M. Ritchie, *The C Programming Language*, 2nd ed., Englewood Cliffs, NJ: Prentice Hall, 1988.