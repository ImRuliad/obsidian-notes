*Templates are a powerful tool for creating generic classes or functions. Allows to write code that works for any data type without rewriting it for each type.*

---

# <u> Key Features of Templates </u>
- Avoid code duplication by allowing one functions or class to work with multiple data types, mainly allowing generic functions and classes
- Provide type safety, unlike using void* pointers or macros
- Can be specialized for specific data types when needed
- Forms the basis of STL Containers and algos like vector, map, and sort

```cpp
template <typename T> T myMax(T x, T y)
{
	return (x > y) ? x : y;
}

int main()
{
	std::cout << "Max of 3 and 7 is: " << myMax<int>(3, 7) << endl;
	std::cout << "Max of 10 and 11 is: " << myMax<double>(10.1, 11.2) << endl;
	std::cout << "Max of 'g' and 'e': " << myMax<char>('g', 'e') << endl;
	
	return 0
} 
```

# <u> Define Templates </u>
```cpp
template <typename A, typename B, ...>
entity_definition
```

> [!Danger] The above syntax can define templates for three components (entities) of C++ language.
> - Function Templates
> - Class Templates
> - Variable Templates (Since C++ 14)

# <u> Function Templates </u>
*In c++, templates allow us to write generic code for functions that can be used with different data types, and this can be achieved with templates.*
```cpp
#include <iostream>

template <typename T> T myMax(T x, T y) {
	return (x > y) ? x : y;
}

int main() {
	std::cout << myMax<int>(3, 7) << std::endl;            // 7
	std::cout << myMax<double>(1.2, 3.4) << std::endl;     // 3.4
	std::cout << myMax<char>('a', 'b') << std::endl;       // 'b'
	return 0;
}
```

