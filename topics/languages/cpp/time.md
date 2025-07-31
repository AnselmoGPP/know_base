# Time

## Table of Contents
+ [std::chrono](#std::chrono)
+ [Sleeps](#sleeps)
+ [Timers](#timers)
+ [Data](#data)
+ [References](#references)


## std::chrono

The chrono library is a flexible collection of types that track time with varying degrees of precision. It defines 3 main types as well as utility functions and common typedefs.

- **Clocks**

A clock consists of a starting point (or epoch) and a tick rate. Example: a clock may have an epoch of 1/1/1970 and tick every second. C++ defines several clock types.

- **Time points**

A time point is a duration of time that has passed since the epoch of a specific clock.

**`time_point`** is a class template that represents a point in time. It’s implemented as if it stores a value of type Duration indicating the time interval from the start of the clock’s epoch.

- **Durations**

A duration consists of a span of time, defined as some number of ticks of some time unit. Example: 42 seconds could be represented by a duration consisting of 42 ticks of a 1-second time unit.

**`duration`** is a class template that represents a time interval. It consists of a count of ticks of type Rep and a tick period, where the tick period is a compile-time rational constant representing the number of seconds from one tick to the next. The only data stored in a duration is a tick count of type Rep. If Rep is a floating point, then the duration can represent fractions of ticks. Period is included as part of the duration’s type, and is only used when converting between different durations.

**`time_of_day`** splits a duration representing time elapsed since midnight into hours, minutes, seconds and fractional seconds, as applicable. It’s primarily a formatting tool.


## Sleeps

- **C++ sleep**

```
std::this_thread::sleep_for(std::chrono::milliseconds(x));
```

- **Boost sleep**

```
boost::this_thread::sleep(boost::posix_time::milliseconds(500));
```

```
boost::this_thread::sleep_for(boost::chrono::milliseconds(4));
```

- **Windows sleep**

```
Sleep(500);          // <windows.h>
```


## Timers

- **C++ timer**

```
#include <chrono>
std::chrono::high_resolution_clock::time_point t1 = std::chrono::high_resolution_clock::now();
// do something...
std::chrono::high_resolution_clock::time_point t2 = std::chrono::high_resolution_clock::now();

long duration = std::chrono::duration_cast<std::chrono::milliseconds>(t2 - t1).count();
std::cout << duration << std::endl;
```

```
std::chrono::high_resolution_clock::time_point timeZero = std::chrono::system_clock::duration::zero();
```

- **Boost timer**

  - Control the number of milliseconds that have happened between 2 lines:

```
double chronometer;
boost::chrono::high_resolution_clock timer;
boost::chrono::high_resolution_clock::time_point start, end;
start = timer.now();

// do something ...

end = timer.now();
chronometer = boost::chrono::duration_cast<boost::chrono::duration<float, boost::milli>>(end - start).count();
```

- Control the number of milliseconds that you want to wait:

```
boost::chrono::high_resolution_clock timer;
boost::chrono::high_resolution_clock::time_point start, end;
m_start = timer.now();  m_end = timer.now();
float clock = 0;
while (timer < 48)
timer = boost::chrono::duration_cast<boost::chrono::duration<float, boost::milli>>(end - start).count();
```


## Data

- Time since the clock’s epoch (UNIX/POSIX time: 1/1/1970 00:00:00 UTC) (<chrono>)

```
auto current_time = std::chrono::system_clock::now();
auto duration_in_seconds = std::chrono::duration<double>(current_time.time_since_epoch());
double num_seconds = duration_in_seconds.count();
std::cout << (long long)num_seconds;
```

```
std::cout << (long long) std::chrono::duration<double>(current_time.time_since_epoch()).count();
```

```
1551966821
```

- Get a string with the date and time (`<chrono>`):

```
auto timePoint= std::chrono::system_clock::now();
std::time_t date = std::chrono::system_clock::to_time_t(timePoint);
std::cout << std::ctime(&date);
```

```
Thu Mar  7 13:43:25 2019
```

- Get a string with date and time (only numbers) (`<chrono>`)

```
std::string date_time() {
    // Get a string containing date and time
    auto timePoint = std::chrono::system_clock::now();
    std::time_t date = std::chrono::system_clock::to_time_t(timePoint);
    std::string date_time = std::ctime(&date);			// std::ctime() format: Thu Mar  7 13:43:25 2019

    // Convert month from name format to number format
    char month[4] = { date_time[4], date_time[5], date_time[6], '\0' };
    std::string month_string = month;
    if (month_string == "Jan") { month[0] = '0'; month[1] = '1'; }
    else if (month_string == "Feb") { month[0] = '0'; month[1] = '2'; }
    else if (month_string == "Mar") { month[0] = '0'; month[1] = '3'; }
    else if (month_string == "Apr") { month[0] = '0'; month[1] = '4'; }
    else if (month_string == "May") { month[0] = '0'; month[1] = '5'; }
    else if (month_string == "Jun") { month[0] = '0'; month[1] = '6'; }
    else if (month_string == "Jul") { month[0] = '0'; month[1] = '7'; }
    else if (month_string == "Aug") { month[0] = '0'; month[1] = '8'; }
    else if (month_string == "Sep") { month[0] = '0'; month[1] = '9'; }
    else if (month_string == "Oct") { month[0] = '1'; month[1] = '0'; }
    else if (month_string == "Nov") { month[0] = '1'; month[1] = '1'; }
    else if (month_string == "Dic") { month[0] = '1'; month[1] = '2'; }

    // Build the date and time format
    char arr[15] = { date_time[8], date_time[9], month[0], month[1], date_time[20], date_time[21], date_time[22], date_time[23], date_time[11], date_time[12], date_time[14], date_time[15], date_time[17], date_time[18], '\0' };
    for (int i = 0; i < 16; i++) if (arr[i] == ' ') arr[i] = '0';
    std::string date_string = arr;
    return date_string;
```

```
08032019113542            // i.e.: 8/3/2019 11:35:42
```


## References

- [Data and time utilities](https://en.cppreference.com/w/cpp/chrono)
- [std::tm](https://en.cppreference.com/w/cpp/chrono/c/tm)
- [<ctime>](https://en.cppreference.com/w/cpp/header/ctime)
- [std::localtime](https://en.cppreference.com/w/cpp/chrono/c/localtime)