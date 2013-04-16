Lab 02: Pointers and Streams
===========================

### Design Document
There is no design writeup due with this lab.

### Grading
The lab exercise is worth 10 points. No design writeup is required for this lab.

This lab assignment *must be demonstrated to a TA or Course Producer (CP)*.

### Downloading The Lab
Follow the instructions listed in the [lab repository](https://github.com/usc-csci102-spring2013/labs) [README](https://github.com/usc-csci102-spring2013/labs/blob/master/README.md) file to clone the contents locally on your machine.

## Part 1 (2 points)
Copy [`lab2.cpp`](https://github.com/usc-csci102-spring2013/labs/blob/master/lab02/lab2.cpp) file to your local repository and open it in an editor (`emacs` or `gedit`).  You will find a class definition at the top for an Item. An Item has a `name` (`string`), a `quantity` (`int`), and a `price` (`double`).  These three data items are declared as private data members. We have provided declarations (prototypes) for a default constructor and a constructor that accepts initial values for each of the data members. We have also provided accessor (get) functions and mutator (set) functions.

Write the code for each of these functions just below the class definition.  The default constructor is complete and you need not modify it.

### Questions the TA/CP will ask you:
What does the `const` indicate in the prototype: 
```
string getName() const;
```

## Part 2 (6 points)
Copy the [`lab2data.txt`](https://github.com/usc-csci102-spring2013/labs/blob/master/lab02/lab2data.txt) file to your local repository and open it in an editor and view its contents. It contains text data for 5 Items. The first line contains the number of items that follow.  Next the data for each item appears on one line with the name first followed by the quantity and then the price. A copy of the file is shown below:
```
5
chair 1 1.25
table 2 4.30
book 3 0.55
laptop 4 10.25
widget 5 1.0
```

Your program will take as input the filname of the data as a command line argument and pass the filename to a function called `readData()`.  Read data should open the file, extract the number of Items in the data file and then allocate (dynamically usine the `new` operator) an array to store that many Items.  Next your program should iterate and extract the data for each item into temporary variables and fill in the Items array.

A pointer to the array should be returned and the length of the array should be assigned to the reference argument that was passed into the function along with the filename.

You may assume there are no format errors EXCEPT for the case that the filename provided does not name a valid file (i.e. you must check if it was successfully opened; or put another way that opening the file did not fail). If opening the file did fail, you should return NULL (i.e. 0) as the Item* pointer value immediately before progressing further.

The `main()` function is complete except for a statement at the end to deallocate the Item array returned
by `readData()`.  Thus you need to:
  1. Complete the code for `readData()` according to the specification in the previous paragraphs. You may remove the `return NULL;` statement in the `readData()` function which was acting as a placeholder to allow the code to compile.
  1. Write the one statement in `main()` to deallocate the array.

Go on to Part 3 and complete it before demo'ing for your TA/CP.


## Part 3 (2 points)
Write a function `printItems` which accepts as input arguments an array of Items (i.e. a pointer to the array) and the length of the array and iterates over each Item printing out its name, quantity, and price in a table format. The table should have a column header (e.g. "Name", "Qty", "Price") with the name field having width 15, quantity field having width 10, and price field having width 10 (see [this page](http://www.cplusplus.com/reference/iomanip/setw/)).
The price should be printed such that the number is printed with a fixed precision of 2 decimal points (see [this page](http://www.cplusplus.com/reference/iomanip/setprecision/) for details). You can use the default right justification for your display.

Your output should eventually look like this:
```
Read 5 Items from the file: lab2data.txt
           Name       Qty     Price
          chair         1      1.25
          table         2      4.30
           book         3      0.55
         laptop         4     10.25
         widget         5      1.00
```

Compile your program:
```shell
g++ -g -Wall -o lab2 lab2.cpp
```

Then run your program:
```shell
./lab2 lab2data.txt
```

Fix any errors that occur by using a debugger like ddd or kdbg or inserting print statements at helpful locations.

Before you demonstrate your code to the TA/CP be sure it correctly handles the case where the data file
does not exist (i.e. run your program again but with a filename that does not exist such as `lab3data.txt`)

Demonstrate your program to the TA/CP using both `lab2data.txt` and `lab2data2.txt`

### Questions the TA/CP will ask you
  - How do you check whether the file opened successfully?
  - Did you construct a temporary Item object and copy it into the array slot or just set the fields of the Items in the array?  Which option is more effecient?
  - Explain what would happen if the `len` parameter to `readData()` was not passed by reference, as in:
  ```
  Item* readData(const char *filename, int len);
  ```

## Extra Credit (1 point)
Use a debugger like `ddd` or `kdbg` to step through the execution of your program.

A debugger can be run by invoking it with the executable filename:
```shell
ddd lab2
```

Set a breakpoint at the line of code in main that calls `readData()` by right clicking on that line and choosing 'Set Breakpoint'. Then run the program by choosing Program..Run...  Enter `lab2data.txt` as the command line argument and run the program.  Then when the program breaks use Step to step into the function and execute it line by line.  Use print or watch to see the value of your temp variables at various points in time.

Show your TA/CP you know how to use a debugger like `ddd` or `kdbg` by perform the above tasks.

## Challenge (no points)
Use `getline(istream&, string &)` and `stringstream`s to extract the data fields for each item. Use online resources to findout more about `getline` and `stringstream`s. If successful you should replace all extractions (`>>`) operators performed on your ifstream object with `>>` operations on a `stringstream` object.

