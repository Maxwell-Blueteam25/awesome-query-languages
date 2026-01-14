### **III. Field Manipulation (The "Eval" Encyclopedia)**

_The "Transform" phase: Modifying data using `eval` and `rex`._

#### **1. General Field Commands**

|**Command**|**Description**|**Example**|
|---|---|---|
|**`eval`**|Calculates an expression and stores it in a field.|`|
|**`rename`**|Renames a field. Supports wildcards.|`|
|**`fields`**|Removes (`-`) or keeps (`+`) fields.|`|
|**`rex`**|Extracts fields using regex named groups.|`|

#### **2. Eval Functions: Logic & Comparison**

|**Function**|**Description**|**Example**|
|---|---|---|
|**`if(X,Y,Z)`**|If X is TRUE, return Y, else Z.|`if(error==200, "OK", "Error")` |
|**`case(...)`**|Takes pairs of Boolean/Result arguments.|`case(error==404, "Not Found", error==500, "Fail")` |
|**`validate(...)`**|Returns a string for the first False expression (Error Checking).|`validate(isint(port), "Error: Not Int", port < 65535, "Error: Range")` |
|**`coalesce(...)`**|Returns the first non-null value.|`coalesce(null(), "Returned Val", null())` |
|**`in(f, list)`**|Returns TRUE if field `f` is in the list (must be used inside `if`).|`if(in(status, "404", "500"), "True", "False")` |
|**`nullif(X,Y)`**|Returns NULL if X equals Y, else returns X.|`nullif(fieldA, fieldB)` |

#### **3. Eval Functions: String Manipulation**

|**Function**|**Description**|**Example**|
|---|---|---|
|**`len(X)`**|Returns character length of string X.|`len(username)`|
|**`lower(X)`**|Converts to lowercase.|`lower(username)` |
|**`substr(X,Y,Z)`**|Returns substring of X from start Y for length Z.|`substr("string", 1, 3)` |
|**`replace(X,Y,Z)`**|Substitutes regex Y with string Z in string X.|`replace(date, "/", "-")` |
|**`trim(X)`** / **`ltrim`** / **`rtrim`**|Removes whitespace or specific chars.|`rtrim(" ZZZabcZZ", "Z")` |
|**`match(X,Y)`**|Returns TRUE if X matches regex pattern Y.|`match(field, "^\d")` |
|**`like(X,Y)`**|Returns TRUE if X is like the SQLite pattern Y.|`like(field, "addr%")` |
|**`split(X,Y)`**|Splits string X by delimiter Y into a multivalued field.|`split(address, ";")` |

#### **4. Eval Functions: Math & Numbers**

|**Function**|**Description**|**Example**|
|---|---|---|
|**`round(X,Y)`**|Rounds X to Y decimal places.|`round(3.5)` (defaults to integer) |
|**`abs(X)`**|Absolute value.|`abs(-10)`|
|**`ceil(X)`**|Ceiling (round up).|`ceil(1.9)` -> 2 |
|**`exact(X)`**|Evaluates using double precision floating point.|`exact(3.14 * num)` |
|**`random()`**|Pseudo-random number 0 to 2,147,483,64760.|`random()` |

#### **5. Eval Functions: Type Checking & Conversion**

|**Function**|**Description**|**Example**|
|---|---|---|
|**`cidrmatch(X,Y)`**|Identifies if IP Y belongs to subnet X.|`cidrmatch("10.0.0.0/24", ip)` |
|**`isint(X)`**|Returns TRUE if X is an integer.|`isint(port)`|
|**`isnull(X)`**|Returns TRUE if X is NULL.|`isnull(result)`|
|**`tonumber(X,Y)`**|Converts string X to number (Base Y, default 10).|`tonumber("0A4", 16)` |
|**`tostring(X,Y)`**|Converts number X to string format Y ("hex", "commas", "duration").|`tostring(seconds, "duration")` -> `HH:MM:SS` |
