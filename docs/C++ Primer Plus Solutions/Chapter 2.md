## Review Questions

> What are the modules of C++ programs called?

Functions

> What does the following preprocessor directive do?

> `#include <iostream>`

It links the source code and head file `iostream`. the contents of the head file will be added to the source code before compilation.

> What does the following statement do?

> `using namespace std;`

It makes the definitions in std namespace available to the program.

> What statement would you use to print the phrase “Hello, world” and then start a new line?

```cpp
using namespace std;
cout << "Hello, world" << endl; 
```

> What statement would you use to create an integer variable with the name cheeses?

```cpp
int cheeses;
```

> What statement would you use to assign the value 32 to the variable cheeses?

```cpp
cheeses = 32;
```

> What statement would you use to assign the value read from keyboard to the variable cheeses?

```cpp
cin >> cheeses;
```

> What statement would you use to print "We have X varieties of cheese,", where X is the value of the variable cheeses?

```cpp
cout << "We have " << cheeses << " varieties of cheese,";
```

> What do the function prototypes tell us about the functions?

> `int froop(double t);`

> `void rattle(int n);`

> `int prune(void)`

1. `int froop(double t);`, the return type is `int`, function name is `froop`, it accepts one argument of type `double`.
2. `void rattle(int n);`, the function has no return value, function name is `rattle`, it accepts one argument of type `int`.
3. `int prune(void)`, the return type is `int`, function name is `prune`, it doesn't take any arguments.

> When is return not needed when you defining a function?

1. When the function has no return value.
2. When you are writing `main` function and want to return `0`.

> When you are writing `main` function, it has the statement `cout << "Please enter your PIN: ";`. The compiler says `cout` is an undeclared identifier. What is the cause of the issue? How can it be solved?

The issue is caused because we don't specify the namespace where `cout` is defined. To solve the issue, we could,
1. add `using namespace std;`
2. add `using std::cout;`
3. change it to `std::cout << "Please enter your PIN: ";`

## Coding Exercise

### 2.1

```cpp
#include <iostream>

/*
 * Write a C++ program that displays your name 
 * and address (or if you value your privacy, 
 * a fictitious name and address).
 */
int main() {
    using namespace std;
    cout << "Lionel Messi" << endl;
    cout << "12 Abc St, Sydney, NSW, 2000" << endl;
    return 0;
}
```

### 2.2

```cpp
#include <iostream>

int furlongToYard(int furlong) {
    return furlong * 220;
}

/*
 * Write a C++ program that asks for a distance
 * in furlongs and converts it to yards. (One
 * furlong is 220 yards.)
 */
int main() {
    using namespace std;
    int furlongs;
    cout << "Enter furlongs: ";
    cin >> furlongs;
    cout << "Yards: " << furlongToYard(furlongs) << endl;
    return 0;
}
```

### 2.3

```cpp
#include <iostream>

using namespace std;

void printFirstTwoLines() {
    for(int i = 0; i < 2; i ++) {
        cout << "Three blind mice" << endl;
    }
}

void printLastTwoLines() {
    for(int i = 0; i < 2; i ++) {
        cout << "See how they run" << endl;
    }
}

/*
 * Write a C++ program that uses three user-defined
 * functions (counting main() as one) and produces
 * the following output:
 * 
 *  Three blind mice
 *  Three blind mice
 *  See how they run
 *  See how they run
 *  
 * One function, called two times, should produce
 * the first two lines, and the remaining function,
 * also called twice, should produce the remaining
 * output.
 */
int main() {
    printFirstTwoLines();
    printLastTwoLines();
    return 0;
}
```

### 2.4

```cpp
#include <iostream>

int yearToMonth(int year) {
    return year * 12;
}

/*
 * Write a program that asks the user to enter
 * his or her age. The program then should
 * display the age in months:
 *
 *  Enter your age: 29
 *  Your age in months is 348.
 */
int main() {
    using namespace std;
    cout << "Enter your age: ";
    int age;
    cin >> age;
    cout << "Your age in months is "
         << yearToMonth(age)
         << '.' << endl;
    return 0;
}
```

### 2.5

```cpp
#include <iostream>

double celsiusToFahrenheit(double celsius) {
    return 1.8 * celsius + 32;
}

/*
 * Write a program that has main() call a user-defined
 * function that takes a Celsius temperature value as an
 * argument and then returns the equivalent Fahrenheit
 * value. The program should request the Celsius value
 * as input from the user and display the result, as shown
 * in the following code:
 * 
 *  Please enter a Celsius value: 20
 *  20 degrees Celsius is 68 degrees Fahrenheit.
 *  
 * For reference, here is the formula for making the
 * conversion:
 * 
 *  Fahrenheit = 1.8 × degrees Celsius + 32.0
 */
int main() {
    using namespace std;
    cout << "Please enter a Celsius value: ";
    double celsius;
    cin >> celsius;
    cout << celsius
         << " degrees Celsius is "
         << celsiusToFahrenheit(celsius)
         << " degrees Fahrenheit." << endl;
    return 0;
}
```

### 2.6

```cpp
#include <iostream>

double convert(double lightYear) {
    return lightYear *63240;
}

/*
 * Write a program that has main() call a user-defined
 * function that takes a distance in light years as an
 * argument and then returns the distance in astronomical
 * units. The program should request the light year value
 * as input from the user and display the result, as shown
 * in the following code:
 *
 *  Enter the number of light years: 4.2
 *  4.2 light years = 265608 astronomical units.
 *
 *  An astronomical unit is the average distance from the
 *  earth to the sun (about 150,000,000 km or 93,000,000
 *  miles), and a light year is the distance light travels
 *  in a year (about 10 trillion kilometers or 6 trillion
 *  miles). (The nearest star after the sun is about 4.2
 *  light years away.) Use type double (as in Listing 2.4)
 *  and this conversion factor:
 *
 *   1 light year = 63,240 astronomical units
 */
int main() {
    using namespace std;
    cout << "Enter the number of light years: ";
    double lightYears;
    cin >> lightYears;
    cout << lightYears
         << " light years = "
         << convert(lightYears)
         << " astronomical units." << endl;
    return 0;
}
```

### 2.7

```cpp
#include <iostream>

using namespace std;

void printTime(int hours, int minutes) {
    cout << "Time: "
         << hours
         << ":"
         << minutes
         << endl;
}

/*
 * Write a program that asks the user to enter
 * an hour value and a minute value. The main()
 * function should then pass these two values
 * to a type void function that displays the two
 * values in the format shown in the following
 * sample run:
 *
 *  Enter the number of hours: 9
 *  Enter the number of minutes: 28
 *  Time: 9:28
 */
int main() {
    cout << "Enter the number of hours: ";
    int hours;
    cin >> hours;
    cout << "Enter the number of minutes: ";
    int minutes;
    cin >> minutes;
    printTime(hours, minutes);
    return 0;
}
```