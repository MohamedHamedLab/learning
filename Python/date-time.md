# Date Time

```python
from datetime import date
from datetime import time
from datetime import datetime
```
- DATE OBJECTS: Get today's date from the simple today() method from the date class
def main():

```python
  today = date.today()
  print("Today's date is", today)

  # print out the date's individual components
  print("date components: ", today.day, today.month, today.year)

  # retrieve today's weekday (0=Monday, 6=Sunday)
  print("Today's weekday # is: ", today.weekday())
  days = ["mon", "tue", "wed", "thu", "fri", "sat", "sun"]
  print("which is a: ", days[today.weekday()])

  ## DATETIME OBJECTS
  # Get today's date from the datetime class
  today = datetime.now()
  print("The current date and time is ", today)
  # Get the current time
  currentTime = datetime.time(datetime.now())
  print("The time now is: ", currentTime)
  if __name__ == "__main__":
    main()
```

### Formatting time
#### Example file for formatting time and date output
```python
from datetime import datetime
def main():
```

 #### can be formatted using a set of predefined string
```python
now = datetime.now()
```

- ` %y/%Y` - Year, `%a/%A `- weekday, `%b/%B` - month, `%d` - day of month

```python
print(now.strftime("The current year is: %Y"))
print(now.strftime("%a, %d %B, %y"))
```

- `%c` - locale's date and time, `%x` - locale's date,` %X `- locale's time
  
 ```python
print(now.strftime("Locale date and time: %c"))
print(now.strftime("Locale date: %x"))
print(now.strftime("Locale time: %X"))
```

- `%I/%H` - 12/24 Hour, `%M` - minute, `%S` - second, `%p` - locale's AM/PM

 ```python
print(now.strftime("Current time: %I:%M:%S %p"))
print(now.strftime("24-hour time: %H:%M"))
if name == "main":
  main()
```

## Timedelta
- Example file for working with timedelta objects
1. construct a basic timedelta and print it  
2. print today's date
3. print today's date one year from now
4. create a timedelta that uses more than one argument

```python
from datetime import date
from datetime import time
from datetime import datetime
from datetime import timedelta


print(timedelta(days=365, minutes=20, hours=10, weeks=0))

now = datetime.now()
print("today is: " + str(now))

print("one year from now it will be: " + str(now + timedelta(days=365)))

print("one year and 3 weeks from now it will be: " + str(now + timedelta(days=365, weeks= 3)))
```

1. calculate the date 1 week ago, formatted as a string

```python
t = datetime.now() - timedelta(weeks=1)
s= t.strftime("%A %B %d, %Y")
print("1 week ago: " + str(s))
```

2. How many days until April Fools' Day?

```python
today = date.today()
afd = date(today.year, 4, 1)
```


3. use date comparison to see if April Fool's has already gone for this year if it has, use the replace() function to get the date for next year.
4. if so, ge the date for the next year
5.  Now calculate the amount of time until April Fool's Day

```python
if afd < today:
  print("April fool's day already went by %d days ago " % ((today - afd).days))
  afd = afd.replace(year=today.year + 1)
  time_to_afd = afd - today
  print("it's just", time_to_afd.days, "days until next April Fools' Day")
```


## Calendars

-  import the calendar module
-  create a plain text calendar
```python
import calendar
c = calendar.TextCalendar(calendar.MONDAY)
st = c.formatmonth(2017, 1, 0, 0)
print(st)
```

- create an HTML formatted calendar
```python
hc = calendar.HTMLCalendar(calendar.SUNDAY)
st1 = hc.formatmonth(2017, 1)
print(st1)
```

- The Calendar module provides useful utilities for the given locale, such as the names of days and months in both full and abbreviated forms

```python
for name in calendar.month_name:
  print(name)
for day in calendar.day_name:
  print(day)
```
-  Calculate days based on a rule: For example, consider a team meeting on the first Friday of every month To figure out what days that would be for each month we can use this script

```python
  print("Team meeting will be on: ")
  for m in range(1, 13):
    cal = calendar.monthcalendar(2018, m)
    weekone = cal[0]
    weektwo = cal[1]
    if weekone[calendar.FRIDAY] != 0:
      meetday = weekone[calendar.FRIDAY]
    else:
      meeday = weektwo=cal[calendar.FRIDAY] 
    print ("%10s %2d" % (calendar.month_name[m], meetday))
```