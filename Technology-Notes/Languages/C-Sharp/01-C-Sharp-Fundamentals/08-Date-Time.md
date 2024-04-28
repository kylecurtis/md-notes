---
tags: [csharp]
---

In C#, handling date and time is robustly supported by several classes, including `System.DateTime`, `System.TimeSpan`, `System.DateTimeOffset`, as well as the newer `DateOnly` and `TimeOnly` structures.

<br>

---

<br>

## System.DateTime

<br>

The `DateTime` class is crucial for representing both date and time in a single object. It's suitable for most scenarios requiring a timestamp.

<br>

- **Declaration and Initialization**

  ```csharp
  DateTime now = DateTime.Now; // Current date and time
  DateTime today = DateTime.Today; // Today's date with time set to 00:00:00
  DateTime specificDate = new DateTime(1969, 7, 20); // Specific date: July 20, 1969
  ```

<br>

- **Properties and Methods**

  Properties like `Year`, `Month`, `Day`, and methods such as `AddDays`, `AddHours` help manipulate DateTime objects conveniently.

<br>

- **Parsing and Formatting**

  ```csharp
  DateTime parsedDate = DateTime.Parse("April 14, 2024");
  string formattedDate = now.ToString("yyyy-MM-dd");  // Outputs: 2024-04-14
  ```

<br>

---

<br>

## System.TimeSpan

<br>

`TimeSpan` represents time intervals and is perfect for measuring elapsed time or durations.

<br>

- **Declaration and Initialization**

  ```csharp
  TimeSpan thirtyMinutes = TimeSpan.FromMinutes(30);
  TimeSpan oneHour = new TimeSpan(1, 0, 0);  // 1 hour
  ```

<br>

- **Operations**

  TimeSpan objects can be added to or subtracted from DateTime values to calculate future or past times.

<br>

---

<br>

## System.DateTimeOffset

<br>

`DateTimeOffset` is essential for applications that handle multiple time zones, as it includes a time offset from UTC.

<br>

- **Declaration and Initialization**

  ```csharp
  DateTimeOffset nowWithOffset = DateTimeOffset.Now;
  DateTimeOffset specificTimeWithOffset = new DateTimeOffset(2024, 4, 14, 12, 0, 0, TimeSpan.FromHours(-4));
  ```

<br>

---

<br>

## DateOnly and TimeOnly

<br>

.NET 6 introduced `DateOnly` and `TimeOnly` to handle dates and times separately when you don't need to work with both together.

<br>

- **DateOnly**

  ```csharp
  DateOnly dateOfBirth = new DateOnly(1990, 4, 14);
  DateOnly today = DateOnly.FromDateTime(DateTime.Now);  // Convert DateTime to DateOnly
  string formattedDate = dateOfBirth.ToString("yyyy-MM-dd");  // Outputs: 1990-04-14
  ```

<br>

- **TimeOnly**

  ```csharp
  TimeOnly openingTime = new TimeOnly(9, 30);  // 9:30 AM
  TimeOnly currentTime = TimeOnly.FromDateTime(DateTime.Now);  // Convert DateTime to TimeOnly
  bool isOpenNow = TimeOnly.FromDateTime(DateTime.Now) < new TimeOnly(17, 0);  // Compare times
  ```

<br>

---

<br>

### Best Practices and Use Cases

- **DateTime vs. DateTimeOffset**: Use `DateTime` for local time or when time zone is not a factor. Use `DateTimeOffset` for handling multiple time zones.
- **UTC Times**: Work with UTC times to avoid issues with daylight saving time and time zone conversions.
- **DateOnly and TimeOnly**: Use these for clarity and simplicity when only the date or time component is needed.