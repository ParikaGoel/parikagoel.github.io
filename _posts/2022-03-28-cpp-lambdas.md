## C++ Lambda Functions

### Introduction

Lambda functions are inline functions that are designed to be used for small code which will not be reused and thus is not worth naming. 

The basic syntax of lambda functions is as below:

```
[capture clause] (parameters) -> return type
{
  function body
}
```

#### Capture Clause
Lambda functions can capture the variables from the enclosing scope. By capture, we mean if a particular variable can be used inside a lambda function.

The variables can be captured in three ways:
- Capture by reference 
  - [&] -> All the variables from the enclosing scope will be captured by reference.
  - [&a] -> Instead of capturing all the variables, one specific variable a can also be captured by reference. Then no other variable will be accessible inside
  the lambda function.
- Capture by value 
  - [=] -> All the variables from the enclosing scope will be captured by value.
  - [a] -> Instead of capturing all the variables, one specific variable a can also be captured by value. Then no other variable will be accessible inside
  the lambda function.
- Mixed capture 
  - The above two mentioned captures can be used in any possible combination.
  - [a,&b] -> Variable a is captured by value, variable b is captured by reference.
  - [=,&b] -> Variable b is captured by reference. All other variables are captured by value.

An empty [] means that no variable from enclosing scope is accessible inside the lambda body.

#### Return Type
It is optional to specify the return type of the function. The compiler can deduce automatically what would be the return type. But in some complex cases, it might
be helpful to specify it explicitly.

#### Example

The code below shows a simple example of lambda usage. A number defined by variable 'noToAdd' is added to each entry in a vector.

```
#include <algorithm>
#include <vector>

int main()
{
	int noToAdd = 8;
	std::vector<int> vecOfNums{3,2,7,8,4,6};

	// noToAdd captured by reference
	std::for_each(vecOfNums.begin(), vecOfNums.end(), [&noToAdd](int num) {return num + noToAdd; });

	// noToAdd captured by value
	std::for_each(vecOfNums.begin(), vecOfNums.end(), [noToAdd](int num) {return num + noToAdd; });
	return 0;
}
}
```

