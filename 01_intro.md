#cs2040c

[[_main|<-- Back to main]]

# Memory Allocation
#pointers #memory
```c
#include <iostream>
using namespace std;

int main() {  
	int num;  
	double *student_mark;  
	cout << “How many students do you have?" << endl;  
	cin >> num;  
	student_mark = new double [num]  
	for (int i = 0; i< num; i++)  
		cout << “Enter the mark of Student “ << i + 1 << “: “;  
		cin >> student_mark[i];  
	}  
	// do something about the mark  
	delete [] student_mark;  
	return 0;  
}
```
# Pass by Values in C
#pass_by_value
```C
void swap(int* a, int* b) {
	int temp = *a;
	*a = *b;
	*b = temp; 
}

int main() {
	int x, y;
	x = 1;
	y = 2;
	swap(&x, &y);
}
```
# Pass by Reference in C++
#pass_by_reference
```C
void swap(int& a, int& b) {
	int temp = a;
	a = b;
	b = temp; 
}

int main() {
	int x, y;
	x = 1;
	y = 2;
	swap(x, y);
}
```
# Various Parameter Passing in C++
Consider the three functions below:
```c
function1(int a) {  
	a = 10;  
}  
function2(int& a) {  
	a = 10;  
}  
function3(int* a) {  
	*a = 10;  
}  
```
and the calling:
```c
int main() {  
	int x1 = 1;  
	int x2 = 1;  
	int x3 = 1;  
	function1(x1);  
	function2(x2);  
	function3(&x3);  
	cout << x1 << endl;  
	cout << x2 << endl;  
	cout << x3 << endl;  
}  
```
the output will be:
```c
1  
10  
10
```

# OOP
#oop
- In procedural languages (like C), the data (struct) and process (functions) are **separate** entities
- However in OOP, there is encapsulation
	- Data + Function abstraction
	- Representation of data is encapsulated in the object
	- No direct access to data
		- therefore safer since we can't just directly modify the private attributes
	- Only access using functions
	- Class defines new data type -> instance is an object of the class
- Class
	- specifies the common behaviour of entities
	- stores some common storages
		- common -> every instance has one own copy
		- not every instance shares the same copy

> [!info] Naming Convention in C++
> #convention
> Class names are usually in *camel case*
> (e.g. BankAcct)
> 
> Attribute names are usually start with "_" and are in *snake case*
> (e.g. _balance)
### Example implementation
```c
class BankAcct {
	private:
		// "private" indicates no visibility from outside
		// i.e. private attributes CANNOT be directly modified
		// "variables" are called "attributes" or "properties"
		int _acc_num;
		double _balance;
		
	public:
		// publicly accessible definitions
		// functions are called "methods"
		// methods can access all "attributes"
		int withdraw(double amt) {
			if (_balance < amt) return 0;
			_balance -= amt;
			return 1;
		}
		void deposit (double amt) {
			...
		}
}
```
### (More Common) Alternate implementation
```c
class BankAcct {
	private:
		int _acc_num;
		double _balance;
		
	public:
		// add the header in the class definition only
		// separates the implementation (code body)
		// which makes the header more readable
		int withdraw(double amt);
		void deposit (double amt) {
		...
		}
}

// leave the body of your code here
int BankAcct::withdraw(double amt) {
	if (_balance < amt) return 0;
	_balance -= amt;
	return 1;
}
```
### Example usage
```c
int main() {
	BankAcct AlanAcc, BillyAcc, PeterAcc;

	AlanAcc.deposit(1000);
	AlanAcc.withdraw(500);
	
	BillyAcc.deposit(9000);
	BillyAcc.withdraw(1000);
	
	PeterAcc.deposit(100);
	PeterAcc.withdraw(10);
}
```
# Pointers
>[!info] Pointer Convention in C++
>#convention
> The preferred convention for the * operator (at least in C++) is
>```c 
>int* ptr  // read as "ptr is of type int*"
>``` 
> rather than
>```c 
>int *ptr 
>// this is a declaration, which consists of:
>// a declaration-specifier int, followed by
>// a declarator, *ptr
>```
### Definition
```c
int *ptr = new int // pointer declaration
int *arr = new int [6]; // array declaration
```
### Free memory
```c
delete ptr; //for pointer
delete [] arr; //for array
```
