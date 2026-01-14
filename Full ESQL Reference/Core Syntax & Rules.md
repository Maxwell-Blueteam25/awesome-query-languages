### **I. Core Syntax & Rules**

_The strict grammar you must follow._

#### **1. Query Structure**

Every query **must** start with a Source Command (usually `FROM`) followed by pipes.

- **Syntax:** `source | process | process`.
    
- **Example:**
    
    SQL
    
    ```
    FROM index
    | WHERE status == 200
    | LIMIT 10
    ```
    

#### **2. Identifiers & Quoting**

- **Standard Fields:** No quotes needed if they start with a letter/underscore and contain only alphanumeric/underscore characters.
    
- **Special Fields:** Use **backticks ( )** if the field starts with a number or has special characters (e.g., `@timestamp` usually doesn't need it, but `1.field` does).
    
    - _Example:_ `` KEEP `1.field` ``.
        
- **String Literals:** Use **double quotes (`"`)**. Triple quotes (`"""`) are supported for multi-line strings or strings containing quotes.
    

#### **3. Comments**

- **Single Line:** `// This is a comment`
    
- **Block:** `/* This is a block comment */`.
    

#### **4. Timespan Literals**

Used for time buckets and intervals. Whitespace is optional.

- _Valid:_ `1day`, `1 day`, `2h`, `5m`.
    
