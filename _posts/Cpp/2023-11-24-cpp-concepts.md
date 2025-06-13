## Concepts

Concepts are a mechanism to put constraints on template type parameters
For example if we want our templated function to only be called with an int, we can use concepts
and it will give compiler error in case any other data type is used.   
To use concepts, include "concepts" header file in your program.

The functionality provided by concepts can be achieved using static_assert and type_traits as well. For example, we can put constraint on template parameters in following way:

```
template <typename T>
void print_number(T n)
{
    static_assert(std::is_integral_v, "Must pass an integral value");
    std::cout << "n: " << n << "\n";
}
```

Concepts provide a more neater and readable way to add these constraints.

### Adding concept to function template
Example using built-in concepts

```
template <typename T>
requires std::integral<T>
T sum(T a, T b)
{
    return a+b;
}

int a0 = 10;
int a1 = 20;
std::cout << sum(a0,a1) << "\n"; // 30

double b0 = 1.3;
double b1 = 2.6;
std::cout << sum(a0,a1) << "\n"; // Compiler Error: integral concept is not satisfied
```


Below are two other way/syntax to write the same concept
```
template <std::integral T>
T sum(T a, T b)
{
    return a+b;
}

auto add(std::integral auto a, std::integral auto b)
{
    return a + b;
}

template <typename T>
T add (T a, T b) -> requires std::integral<T>
{
    return a + b;
}
```


### Custom Concepts

Different ways to write custom concepts

```
template <typename T>
concept MyIntegral = std::is_integral_v<T>;

template <typename T>
concept Multipliable = requires(T a, T b){
    a * b;
};

template <typename T>
concept Incrementable = requires(T a){
    // it makes sure that below three statements are valid syntax
    // for the template parameter type T
    // e.g. int would be ok but string would fail
    a+=1;
    a++;
    ++a;
};
```

Once our custom concepts have been created, they can be used in the same way as we used built-in concepts
Example Below:

```
#include <concepts>
#include <iostream>
#include <type_traits>
#include <string>

template <typename T>
concept Incrementable = requires (T a){
    a+=1;
    a++;
    ++a;
};

template <typename T>
requires Incrementable<T> 
T add(T a, T b)
{
    return a + b;
}

int main()
{
    int a{1};
    int b{19};
    std::cout << add(a,b) << "\n"; // 20

    std::string c{"Hello"};
    std::string d{"World"};
    //std::cout << add(c,d) << "\n"; // Compiler Error
    return 0;
}
```