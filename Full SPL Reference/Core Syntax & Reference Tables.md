### **I. Core Syntax & Reference Tables**

_The atomic building blocks of every search._

#### **1. Common Date & Time Formatting**

Used in `strftime()`, `strptime()`, and timestamping2.

|**Format**|**Description**|**Example Output**|
|---|---|---|
|`%Y-%m-%d`|Year-Month-Day|`2022-12-31` 3|
|`%H:%M:%S`|Hour:Minute:Second (24hr)|`14:05:59`|
|`%I:%M %p`|Hour:Minute (12hr) AM/PM|`02:05 PM` 4|
|`%Q` or `%3N`|Subseconds (millis/micros)|`%3N` = milliseconds 5|
|`%z`|Time zone offset|`-0500` (EST) 6|
|`%s`|Unix Epoch Timestamp|`1308677092` 7|

#### **2. Regex Cheat Sheet**

Used in `rex`, `regex`, `match()`, and field extraction8.

|**Symbol**|**Meaning**|**Example**|
|---|---|---|
|`\d` / `\D`|Digit / Not Digit|`\d\d\d` matches `123` 9|
|`\s` / `\S`|Whitespace / Not Whitespace|`\d\s\d` matches `1 2` 10|
|`\w` / `\W`|Word Char / Not Word Char|`\w` matches letter, number, or `_` 11|
|`[...]`|Character Set|`[a-z0-9#]` matches lower alphanumeric or hash 12|
|`*`|Zero or more|`\w*` 13|
|`+`|One or more|`\d+` matches an integer 14|
|`(?<name>...)`|Named Capture Group|`(?<ssn>\d{3}-\d{2}-\d{4})` extracts field `ssn` 15|
