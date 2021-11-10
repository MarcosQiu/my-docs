## Review Questions

> Why C++ has different types for integers?

Different integer types have different ranges, thus take different memory space. Having these different types provides us flexibility when writing code.

> Declare variables as stated below:

> a. `short` type integer, with value 80

`short val = 80;`

> b. `unsigned int` type integer, with value 42110

`unsigned int val = 42110;`

> c. integer with value 3000000000

`long val = 3000000000;`

> How does C++ prevent the integers from being out of ranges?

When the integer value already reaches the upper bound of the range, increasing by one would make the integer value equal to the lower bound of the range.

> What's the difference between `33L` and `33`?

By default, `33` is of type `int`, `33L` is of type `long`.

> Are these two statements equivalent?

> `char grade = 65;

> `char grade = 'A';

Yes, they are equivalent.

> How to find the character with ASC II equals to 88? List at least 2 methods.

`char ch = 88;`

`char ch = (char) 88;`

> Assigning long to float would cause loss of precision, how about assigning long to double? assigning long long to double?

Assigning `long` and `long long` to `double` is fine.

> What's the value of these statements

> 8 * 9 + 2

74

> 6 * 3 / 4

4

> 3 / 4 * 6

0

> 6.0 * 3 / 4

4.5

> 15 % 4

3

> Assume that `x1` and `x2` are two `double` type variables, you need to convert them to integers and calculate the sum, assign the result to an integer variable. What if we want to calculate the sum and then convert.

 - convertion first

`int sum = int (x1) + int (x2);`

 - convertion later

`int sum = int (x1 + x2)`

> What are the types of these variables for the declaration statements below,

> `auto cars = 15;`

int

> `auto iou = 150.37;`

double

> `auto level = 'B';`

char

> `auto crat = U'/U00002155';`

w_chart

> `auto fract = 8.25f/2.5;`

double

## Coding Exercise

### 3.1

```cpp
#include <iostream>

using namespace std;

/**
 * Write a short program that asks for your height
 * in integer inches and then converts your height
 * to feet and inches. Have the program use the
 * underscore character to indicate where to type
 * the response. Also use a const symbolic constant
 * to represent the conversion factor.
 */
int main() {
    int height;
    const int INCHES_PER_FOOT = 12;
    cout << "Please input your height in inches: ";
    cin >> height;
    int feet = height / INCHES_PER_FOOT;
    int inches = height % INCHES_PER_FOOT;
    cout << "Your height is "
        << feet << " feet and "
        << inches << " inches." << endl;
    return 0;
}
```

### 3.2

```cpp
#include <iostream>

using namespace std;

/**
 * Write a short program that asks for your height in feet and inches and your
 * weight in pounds. (Use three variables to store the information.) Have the
 * program report your body mass index (BMI). To calculate the BMI, first
 * convert your height in feet and inches to your height in inches
 * (1 foot = 12 inches). Then convert your height in inches to your height in
 * meters by multiplying by 0.0254. Then convert your weight in pounds into
 * your mass in kilograms by dividing by 2.2. Finally, compute your BMI by
 * dividing your mass in kilograms by the square of your height in meters. Use
 * symbolic constants to represent the various conversion factors.
 */
int main() {
    int heightFeet, heightInches, weightPounds;
    const int INCHES_PER_FOOT = 12;
    const double METERS_PER_INCH = 0.0254;
    const double POUNDS_PER_KILOGRAMS = 2.2;

    cout << "Please input your height in feet and inches: ";
    cin >> heightFeet >> heightInches;
    cout << "Please input your weight in pounds: ";
    cin >> weightPounds;

    int heightInInches = heightFeet * INCHES_PER_FOOT + heightInches;
    double heightInMeters = heightInInches * METERS_PER_INCH;
    double weightInKilograms = weightPounds / POUNDS_PER_KILOGRAMS;
    double bmiIndex = weightInKilograms / (heightInMeters * heightInMeters);

    cout << "The BMI index is: " << bmiIndex << endl;
    return 0;
}
```

### 3.3

```cpp
#include <iostream>

using namespace std;

/**
 * Write a program that asks the user to enter a latitude in degrees, minutes,
 * and seconds and that then displays the latitude in decimal format. There are
 * 60 seconds of arc to a minute and 60 minutes of arc to a degree; represent
 * these values with symbolic constants. You should use a separate variable for
 * each input value. A sample run should look like this:
 *
 *   Enter a latitude in degrees, minutes, and seconds:
 *   First, enter the degrees: 37
 *   Next, enter the minutes of arc: 51
 *   Finally, enter the seconds of arc: 19
 *
 *   37 degrees, 51 minutes, 19 seconds = 37.8553 degrees
 */
int main() {
    const double SECONDS_PER_MINUTE = 60.0;
    const double MINUTES_PER_DEGREE = 60.0;
    int degree, minute, second;

    cout << "Enter a latitude in degrees, minutes, and seconds:" << endl;
    cout << "First, enter the degrees: ";
    cin >> degree;
    cout << "Next, enter the minutes of arc: ";
    cin >> minute;
    cout << "Finally, enter the seconds of arc: ";
    cin >> second;

    double degrees = degree + (minute + second / SECONDS_PER_MINUTE) / MINUTES_PER_DEGREE;
    cout << degree << " degrees, "
        << minute << " minutes, "
        << second << " seconds = "
        << degrees << " degrees" << endl;
    return 0;
}
```

### 3.4

```cpp
#include <iostream>

using namespace std;

/**
 * Write a program that asks the user to enter the number of seconds as an
 * integer value (use type long, or, if available, long long) and that then
 * displays the equivalent time in days, hours, minutes, and seconds. Use
 * symbolic constants to represent the number of hours in the day, the number
 * of minutes in an hour, and the number of seconds in a minute. The output
 * should look like this:
 *
 *  Enter the number of seconds: 31600000
 *  31600000 seconds = 365 days, 17 hours, 46 minutes, 40 seconds
 */
int main() {
    const int SECONDS_PER_MINUTE = 60;
    const int SECONDS_PER_HOURS = 60 * SECONDS_PER_MINUTE;
    const int SECONDS_PER_DAY = 24 * SECONDS_PER_HOURS;

    long long totalSeconds;
    int days, hours, minutes, seconds, secondsLeft;

    cout << "Enter the number of seconds: ";
    cin >> totalSeconds;

    // calculate days
    days = totalSeconds / SECONDS_PER_DAY;
    secondsLeft = totalSeconds % SECONDS_PER_DAY;
    // calculate hours
    hours = secondsLeft / SECONDS_PER_HOURS;
    secondsLeft %= SECONDS_PER_HOURS;
    // calculate minutes
    minutes = secondsLeft / SECONDS_PER_MINUTE;
    seconds = secondsLeft % SECONDS_PER_MINUTE;

    cout << totalSeconds << " seconds = "
        << days << " days, " << hours << " hours, "
        <<minutes << " minutes, " << seconds << " seconds"
        << endl;

    return 0;
}
```

### 3.5

```cpp
#include <iostream>

using namespace std;

/**
 * Write a program that requests the user to enter the current world population
 * and the current population of the U.S. (or of some other nation of your
 * choice). Store the information in variables of type long long. Have the
 * program display the percent that the U.S. (or other nation’s) population is
 * of the world’s population. The output should look something like this:
 *
 *  Enter the world's population: 6898758899
 *  Enter the population of the US: 310783781
 *  The population of the US is 4.50492% of the world population.
 *
 *  You can use the Internet to get more recent figures.
 */
int main() {
    long long usaPopulation, worldPopulation;
    cout << "Enter the world's population: ";
    cin >> worldPopulation;
    cout << "Enter the population of the US: ";
    cin >> usaPopulation;

    cout << "The population of the US is "
        << usaPopulation * 100.0 / worldPopulation
        << "% of the world population." << endl;
    return 0;
}
```

### 3.6

```cpp
#include <iostream>

using namespace std;

/**
 * Write a program that asks how many miles you have driven and how many
 * gallons of gasoline you have used and then reports the miles per gallon your
 * car has gotten. Or, if you prefer, the program can request distance in
 * kilometers and petrol in liters and then report the result European style,
 * in liters per 100 kilometers.
 */
int main() {
    double distanceTraveled, petrolUsed;
    cout << "Enter the distance traveled in kilometers: ";
    cin >> distanceTraveled;
    cout << "Enter the petrol has been used in liters: ";
    cin >> petrolUsed;

    cout << "On average, you need "
        << petrolUsed / distanceTraveled * 100
        << " liters petrol per 100 kilometers."
        << endl;
    return 0;
}
```

### 3.7

```cpp
#include <iostream>

using namespace std;

/**
 * Write a program that asks you to enter an automobile gasoline consumption
 * figure in the European style (liters per 100 kilometers) and converts to the
 * U.S. style of miles per gallon. Note that in addition to using different
 * units of measurement, the U.S. approach (distance / fuel) is the inverse of
 * the European approach (fuel / distance). Note that 100 kilometers is
 * 62.14 miles, and 1 gallon is 3.875 liters. Thus, 19 mpg is about
 * 12.4 l/100 km, and 27 mpg is about 8.7 l/100 km.
 */
int main() {
    double euroStyleConsumption;
    const double LITERS_PER_GALLON = 3.875;
    const double MILES_PER_HUNDRID_KMS = 62.14;
    cout << "Enter an automobile gasoline consumption in European style (L/100Km): ";
    cin >> euroStypeConsumption;

    double litersPerMile = euroStypeConsumption / MILES_PER_HUNDRID_KMS;
    double gallonsPerMile = litersPerMile / LITERS_PER_GALLON;
    cout << "The U.S. approach (miles/gallon): " << 1 / gallonsPerMile
        << endl;
    return 0;
}
```