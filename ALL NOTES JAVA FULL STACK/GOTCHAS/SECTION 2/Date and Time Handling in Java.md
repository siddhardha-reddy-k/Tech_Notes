# Topic 1: Core Date/Time Classes (LocalDate, LocalTime, LocalDateTime, ZonedDateTime)

What it is: Java 8 introduced java.time package — much better than old java.util.Date/Calendar. Four classes, each handling a different combo:

|   |   |   |   |   |
|---|---|---|---|---|
|Class|Has Date?|Has Time?|Has Timezone?|Example use|
|LocalDate|✅|❌|❌|Birthday, deadline|
|LocalTime|❌|✅|❌|Alarm clock, race timing|
|LocalDateTime|✅|✅|❌|Local meeting schedule|
|ZonedDateTime|✅|✅|✅|Flight schedule, global meetings|

Key method: .now() — every class has it, gets current value from system clock.

java

```java
LocalDate today = LocalDate.now();

LocalTime time = LocalTime.now();

LocalDateTime dateTime = LocalDateTime.now();

ZonedDateTime zonedDateTime = ZonedDateTime.now();
```

Gotcha to remember: LocalDate/LocalTime/LocalDateTime are all timezone-unaware — they represent a value with no concept of "where." Only ZonedDateTime knows about timezone. This distinction gets tested directly in "which class would you use for X" MCQs.

## Also useful — creating specific (not "now") values:

java

```java
LocalDate specificDate = LocalDate.of(2026, 1, 26);  // year, month, day

LocalTime specificTime = LocalTime.of(14, 30);        // hour, minute
```

## Practice Q1:

## Write a program that:

1. Prints the current date, current time, and current date-time (all three, using .now())
2. Creates a specific LocalDate for your birthday (any year) using .of()
3. Prints how many days are left until that birthday this year (hint: look up Period.between() — new method, haven't covered it, but try figuring it out — it's a common one)

```java
import java.time.LocalDate;

import java.time.LocalTime;

import java.time.LocalDateTime;

import java.time.Period;

public class Test {

    public static void main(String[] args) {

        // Part 1: current values

        LocalDate today = LocalDate.now();

        LocalTime currentTime = LocalTime.now();

        LocalDateTime currentDateTime = LocalDateTime.now();

        System.out.println("Today's Date: " + today);

        System.out.println("Current Time: " + currentTime);

        System.out.println("Current Date and Time: " + currentDateTime);

        // Part 2: specific birthday

        LocalDate birthday = LocalDate.of(today.getYear(), 8, 15); // e.g. Aug 15

        // Part 3: days left until birthday

        Period period = Period.between(today, birthday);

        if (birthday.isBefore(today)) {

            // birthday already passed this year, calculate for next year

            birthday = birthday.plusYears(1);

            period = Period.between(today, birthday);

        }

        System.out.println("Your birthday this year: " + birthday);

        System.out.println("Days left until birthday: " + period.getDays()

            + " (Months: " + period.getMonths() + ", Years: " + period.getYears() + ")");

    }

}
```

## Walkthrough of the new part (Period):

- Period.between(startDate, endDate) calculates the difference between two LocalDates as years + months + days (not total days — that's a common confusion).
- Gotcha: if birthday already happened this year (e.g., today is July 26 and birthday was in March), Period.between() would give you a negative or misleading result. That's why there's a check: if (birthday.isBefore(today)) → push it to next year with plusYears(1) before calculating.
- period.getDays() alone gives you just the day component — not "total days remaining." If you want a single total day count instead, you'd use a different class: ChronoUnit.DAYS.between(today, birthday) — worth knowing both exist:

- Period → breaks difference into years/months/days (human-readable)
- ChronoUnit.DAYS.between() → gives one raw number of days

Topic 2: Formatting Dates (DateTimeFormatter)

What it is: Formatting = converting a date/time object into a string following a specific pattern. Without formatting, LocalDate.now() prints as 2026-07-26 (ISO default) — fine for logs, ugly for user-facing display.

Key class: DateTimeFormatter — you define a pattern, then call .format() on your date object.

```java
LocalDate today = LocalDate.now();

DateTimeFormatter formatter = DateTimeFormatter.ofPattern("dd/MM/yyyy");

String formatted = today.format(formatter);

System.out.println(formatted); // e.g. 26/07/2026
```

## Common pattern symbols (memorize these, they're asked directly):

|   |   |   |
|---|---|---|
|Symbol|Meaning|Example|
|yyyy|4-digit year|2026|
|MM|2-digit month|07|
|MMM|short month name|Jul|
|MMMM|full month name|July|
|dd|2-digit day|26|
|EEEE|full weekday name|Sunday|
|HH|hour (24-hr)|14|
|mm|minutes|30|
|ss|seconds|45|

Gotcha: the formatter is reusable — you can call .format() on multiple different dates with the same formatter object. Also, DateTimeFormatter is applicable to LocalDate, LocalTime, LocalDateTime — same class works across all of them, as long as the pattern matches what the object actually holds (e.g., don't put HH:mm in a pattern and apply it to a LocalDate — it has no time component, will throw an exception).

## Practice Q:

## Write a program that:

1. Gets today's date
2. Formats and prints it in three different styles: dd-MM-yyyy, MMMM dd, yyyy, and EEEE, MMM dd yyyy

```java
import java.time.LocalDate;

import java.time.format.DateTimeFormatter;

public class Test {

    public static void main(String[] args) {

        LocalDate today = LocalDate.now();

        DateTimeFormatter formatter1 = DateTimeFormatter.ofPattern("dd-MM-yyyy");

        DateTimeFormatter formatter2 = DateTimeFormatter.ofPattern("MMMM dd, yyyy");

        DateTimeFormatter formatter3 = DateTimeFormatter.ofPattern("EEEE, MMM dd yyyy");

        System.out.println("Style 1: " + today.format(formatter1));

        System.out.println("Style 2: " + today.format(formatter2));

        System.out.println("Style 3: " + today.format(formatter3));

    }

}
```

Topic 3: Time Zones (ZoneId, ZonedDateTime, ZoneOffset, OffsetDateTime)

What it is: So far everything was timezone-blind. Real apps (flight booking, global meetings, IBM enterprise systems) need to know which timezone a moment belongs to.

|   |   |
|---|---|
|Class|What it represents|
|ZoneId|An identifier for a timezone region, e.g. "Asia/Kolkata", "America/New_York"|
|ZonedDateTime|Date + time + full timezone (handles daylight saving rules automatically)|
|ZoneOffset|A fixed offset from UTC, e.g. +05:30 — no region rules, just a raw number|
|OffsetDateTime|Date + time + offset only (no full timezone identity) — common in databases|

## Key methods:

java

```java
ZoneId zone = ZoneId.of("Asia/Kolkata");

ZonedDateTime zdt = ZonedDateTime.now(zone);
```

## The critical method for real use — converting between zones:

java

```java
ZonedDateTime newYorkTime = zdt.withZoneSameInstant(ZoneId.of("America/New_York"));
```

withZoneSameInstant() — this is the one to remember. It keeps the actual moment in time unchanged, just recalculates what that moment looks like in a different zone's local clock. (Contrast: there's also withZoneSameLocal() which does the opposite — keeps the clock numbers the same but shifts the actual instant. Rarely used, but good to know it exists so you don't confuse the two.)

Gotcha: ZoneId.of("IST") does NOT work — Java doesn't recognize abbreviations like IST/EST/PST because they're ambiguous (IST could mean India Standard Time or Israel Standard Time). You must use full region names like "Asia/Kolkata".

## Practice Q:

## Write a program that:

1. Gets the current ZonedDateTime in "Asia/Kolkata"
2. Converts and prints the same instant in "America/New_York" and "Europe/London"
3. Format the output nicely using a DateTimeFormatter pattern that includes date, time, and zone abbreviation (hint: zone abbreviation pattern symbol is zzz)

```java
import java.time.ZonedDateTime;

import java.time.ZoneId;

import java.time.format.DateTimeFormatter;

public class Test {

    public static void main(String[] args) {

        DateTimeFormatter formatter = DateTimeFormatter.ofPattern("dd-MM-yyyy HH:mm:ss zzz");

        ZonedDateTime kolkataTime = ZonedDateTime.now(ZoneId.of("Asia/Kolkata"));

        System.out.println("Kolkata: " + kolkataTime.format(formatter));

        ZonedDateTime newYorkTime = kolkataTime.withZoneSameInstant(ZoneId.of("America/New_York"));

        System.out.println("New York: " + newYorkTime.format(formatter));

        ZonedDateTime londonTime = kolkataTime.withZoneSameInstant(ZoneId.of("Europe/London"));

        System.out.println("London: " + londonTime.format(formatter));

    }

}
```

## Walkthrough:

- kolkataTime is the anchor — the actual real-world instant.
- withZoneSameInstant() called twice, once per target zone — each call keeps the same underlying instant (same point on the universal timeline) but re-renders it in that zone's local wall-clock time.
- Notice New York is ~10.5 hrs behind Kolkata and London ~5.5 hrs behind — that's IST offset (+5:30) doing its job.
- zzz in the pattern gives the abbreviated zone name (IST, EDT, GMT) — note EDT vs EST depends on daylight saving, which ZonedDateTime handles automatically based on the date. That's actually the whole point of using ZonedDateTime over ZoneOffset — DST rules are baked in.

Topic 4: Parsing Dates from Strings

What it is: Parsing = converting a String into a structured date object (opposite of formatting, which goes date → string). This matters because user input, form fields, CSV files, API responses — they all give you dates as plain text, and you need to convert that text into a LocalDate/LocalDateTime to actually work with it (compare, calculate, store).

## Key method:

java

```java
LocalDate date = LocalDate.parse("2026-07-26"); // works directly — ISO format is default
```

But if the string isn't in ISO format (yyyy-MM-dd), you must supply a matching DateTimeFormatter:

java

```java
DateTimeFormatter formatter = DateTimeFormatter.ofPattern("dd/MM/yyyy");

LocalDate date = LocalDate.parse("26/07/2026", formatter);
```

Critical rule: the pattern in your formatter must exactly match the shape of the string, or it throws DateTimeParseException (a checked-ish runtime exception — actually it's unchecked, but you should still catch it since bad user input is common).

Gotcha to remember: DateTimeParseException is a RuntimeException (unchecked) — Java doesn't force you to catch it with try-catch, but you absolutely should whenever parsing user input, because malformed date strings are extremely common in real apps (typos, wrong format, empty fields).

## Practice Q:

## Write a program that:

1. Takes a date string from the user via Scanner in dd-MM-yyyy format (e.g. 26-07-2026)
2. Parses it into a LocalDate using a matching DateTimeFormatter
3. If parsing fails (user types garbage), catch DateTimeParseException and print a friendly error message instead of crashing
4. If successful, print the parsed date back in a different format: EEEE, MMMM dd, yyyy

```java
import java.time.LocalDate;

import java.time.format.DateTimeFormatter;

import java.time.format.DateTimeParseException;

import java.util.Scanner;

public class Test {

    public static void main(String[] args) {

        try (Scanner sc = new Scanner(System.in)) {

            System.out.println("Enter a date (dd-MM-yyyy): ");

            String input = sc.nextLine();

            DateTimeFormatter inputFormatter = DateTimeFormatter.ofPattern("dd-MM-yyyy");

            try {

                LocalDate parsedDate = LocalDate.parse(input, inputFormatter);

                DateTimeFormatter outputFormatter = DateTimeFormatter.ofPattern("EEEE, MMMM dd, yyyy");

                System.out.println("Parsed Date: " + parsedDate.format(outputFormatter));

            } catch (DateTimeParseException e) {

                System.err.println("Invalid date format! Please use dd-MM-yyyy. Error: " + e.getMessage());

            }

        }

    }

}
```

## Walkthrough:

- Two separate formatters — inputFormatter (matches what the user typed) and outputFormatter (how you want to display it). This is the standard pattern: parse with one format, display with another.
- LocalDate.parse(input, inputFormatter) — the two-argument version, needed because your string isn't in default ISO format.
- Notice the try-catch is nested inside the try-with-resources block, not combined — that's intentional. The Scanner's try-with-resources handles closing the resource; the inner try-catch handles the parsing failure specifically. If you typed them as one combined catch, you couldn't distinguish "Scanner problem" from "bad date format."
- Test it with garbage input like "hello" or wrong format like "2026-07-26" (ISO instead of dd-MM-yyyy) — should print the friendly error instead of an ugly stack trace crash.
