# Python Date Time String Format

## Introduction

Date and time are two of the most useful yet confusing things in programming life. Date time storage and retrieval required a common well-decided protocol. Timezone conversion is also one of the most challenging tasks. That's why while working with Date and Time, developers should be extra curious. When it comes to working with date and time, Python's `datetime` library is the most reliable one. The **Datetime** library tries to solve all the problems to a large extent. So that's why developers love to use it.

While creating a user-oriented application, one of the most common tasks is to create a well-formatted Date-time string. Example: `Friday, 7 October 2022`. 

Another useful task is to convert the Date-time string into a [`datetime object`](https://docs.python.org/3/library/datetime.html) so that we can use that object with the rest of the program.

## Datetime object

Python's Datetime Object is an object which stores information on a particular date and time. It stores `day`, `month`, `year`, `hour`, `minute`, `second`, and `timezone` information as parameters. The object has various methods to do almost everything possible.

The scope of this blog is the formatting of the date-time object, but not the description of the object itself. So if you want to know more, I am adding some references.

- https://docs.python.org/3/library/datetime.html
- https://www.geeksforgeeks.org/python-datetime-module/


## Conversion of user-given String to Python's Datetime Object

Often time, when users give a date or time input, they often use the specified format by the app. Some common formats are  `DD/MM/YYYY`, `MM/DD/YYYY`, and `HH:MM:SS`, like so. Now, it's the responsibility of the developer to convert the given string to a more useful object.

To convert user given string to a datetime object we use **`strptime`**.

### strptime

```python
from datetime import datetime

datetime.strptime(date_string, format_string) -> Datetime
```

Here, `date_string` is the input from the user, and `format_string` is the expected format, in which the user has given the `date_string`. The `format_string` has the format specifiers, which will be used to extract the values from the `date_string`.

Example:
```python
from datetime import datetime

datetime.strptime("07/10/2022", "%d/%m/%Y")
# datetime.datetime(2022, 10, 7, 0, 0)
```

### Explaination

The date_string (`07/10/2022`) is mapped with the format string (`%d/%m/%Y`).

| Date string value | Format string value | Explanation |
|------------------|----------------------|-------------|
| **07**                 |`%d`                            | `%d` is the format specifier for Day, so 07 is considered as the day |
| **/**                    | `/`                               | Ignored, as not a format specifier |
| **10**                 | `%m`                          | `%m` is the format specifier for Month, so 10 is considered as the Month |
| **/**                    | `/`                               | Ignored, as not a format specifier |
| **2022**             | `%Y`                          | `%Y` is the format specifier for Long Year, so 2022 is considered as the Year |

See the Format list [below](#format-list).

## Conversion Datetime Object to user-readable string

Now that, you have a new `datetime object` and you have done some operations with that, you need to properly format it to string so that users can understand it very well. So now our task is to convert the object to a string.

To convert a datetime object to a string, we use **`strftime`**.

### strftime

```python
# Method 1
datetime_object.strftime(format_string) -> formatted_string

# Method 2
from datetime import datetime
datetime.strftime(Datetime, format_string) -> formatted_string
```

- In `Method 1`, we use `strftime` as a method call to the datetime object and pass the  format_string as a parameter.

- In `Method 2`, we are directly calling the `strftime` as a function and passing the datetime object as the first param, and format_string as the second param.

For both cases, it'll return a `formatted date and time string`.

Example:
```python
from datetime import datetime

datetime.now().strftime("%d/%m/%Y")
# '07/10/2022' (current date in the above format)
```

## Format Specifiers List

Below there are all format specifiers used while formatting. The format specifies are grouped by their types.

### Weekday

| Directive | Meaning                                                                                                                                          | Example                  |
|-----------|--------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------|
| `%a`      | Abbreviated weekday name.                                                                                                                        | Sun, Mon, ...            |
| `%A`      | Full weekday name.                                                                                                                               | Sunday, Monday, ...      |
| `%w`      | Weekday as a decimal number.                                                                                                                     | 0, 1, ..., 6             |
| `%W`      | Week number of the year (Monday as the first day of the week). All days in a new year preceding the first Monday are considered to be in week 0. | 00, 01, ..., 53          |
| `%U`      | Week number of the year (Sunday as the first day of the week). All days in a new year preceding the first Sunday are considered to be in week 0. | 00, 01, ..., 53          |

### Day

| Directive | Meaning                                                                                                                                          | Example                  |
|-----------|--------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------|
| `%d`      | Day of the month as a zero-padded decimal.                                                                                                       | 01, 02, ..., 31          |
| `%-d`     | Day of the month as a decimal number.                                                                                                            | 1, 2, ..., 31            |
| `%j`      | Day of the year as a zero-padded decimal number.                                                                                                 | 001, 002, ..., 366       |
| `%-j`     | Day of the year as a decimal number.                                                                                                             | 1, 2, ..., 366           |


### Month

| Directive | Meaning                                                                                                                                          | Example                  |
|-----------|--------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------|
| `%b`      | Abbreviated month name.                                                                                                                          | Jan, Feb, ..., Dec       |
| `%B`      | Full month name.                                                                                                                                 | January, February, ...   |
| `%m`      | Month as a zero-padded decimal number.                                                                                                           | 01, 02, ..., 12          |
| `%-m`     | Month as a decimal number.                                                                                                                       | 1, 2, ..., 12            |

### Year

| Directive | Meaning                                                                                                                                          | Example                  |
|-----------|--------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------|
| `%y`      | Year without century as a zero-padded decimal number.                                                                                            | 00, 01, ..., 99          |
| `%-y`     | Year without century as a decimal number.                                                                                                        | 0, 1, ..., 99            |
| `%Y`      | Year with century as a decimal number.                                                                                                           | 2013, 2019 etc.          |

### Hour

| Directive | Meaning                                                                                                                                          | Example                  |
|-----------|--------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------|
| `%H`      | Hour (24-hour clock) as a zero-padded decimal number.                                                                                            | 00, 01, ..., 23          |
| `%-H`     | Hour (24-hour clock) as a decimal number.                                                                                                        | 0, 1, ..., 23            |
| `%I`      | Hour (12-hour clock) as a zero-padded decimal number.                                                                                            | 01, 02, ..., 12          |
| `%-I`     | Hour (12-hour clock) as a decimal number.                                                                                                        | 1, 2, ... 12             |
| `%p`      | Locale’s AM or PM.                                                                                                                               | AM, PM                   |

### Minutes

| Directive | Meaning                                                                                                                                          | Example                  |
|-----------|--------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------|
| `%M`      | Minute as a zero-padded decimal number.                                                                                                          | 00, 01, ..., 59          |
| `%-M`     | Minute as a decimal number.                                                                                                                      | 0, 1, ..., 59            |

### Seconds

| Directive | Meaning                                                                                                                                          | Example                  |
|-----------|--------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------|
| `%S`      | Second as a zero-padded decimal number.                                                                                                          | 00, 01, ..., 59          |
| `%-S`     | Second as a decimal number.                                                                                                                      | 0, 1, ..., 59            |
| `%f`      | Microsecond as a decimal number, zero-padded on the left.                                                                                        | 000000 - 999999          |

### Time Zone

| Directive | Meaning                                                                                                                                          | Example                  |
|-----------|--------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------|
| `%z`      | UTC offset in the form +HHMM or -HHMM.                                                                                                           |                          |
| `%Z`      | Time zone name.                                                                                                                                  |                          |

### Overall Representation

| Directive | Meaning                                                                                                                                          | Example                  |
|-----------|--------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------|
| `%c`      | Locale’s appropriate date and time representation.                                                                                               | Mon Sep 30 07:06:05 2013 |
| `%x`      | Locale’s appropriate date representation.                                                                                                        | 09/30/13                 |
| `%X`      | Locale’s appropriate time representation.                                                                                                        | 07:06:05                 |
| `%%`      | A literal '%' character.                                                                                                                         | %                        |