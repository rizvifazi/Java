
![[integer-printf-table.jpg]]


![[printf-table-example.gif]]



| Pattern  | Data | _Printf_ Output   |
| -------- | ---- | ----------------- |
| '%s'     | Java | 'Java'            |
| '%15s'   | Java | '           Java' |
| '%-15s ' | Java | 'Java           ' |
| '%-15S ' | Java | 'JAVA           ' |



**Java _printf_ format flags**

| printf flag | Purpose                                                                                |
| ----------- | -------------------------------------------------------------------------------------- |
| –           | Aligns the formatted _printf_ output to the left                                       |
| +           | The output includes a negative or positive sign                                        |
| (           | Places negative numbers in parenthesis                                                 |
| 0           | The formatted _printf_ output is zero padded                                           |
| ,           | The formatted output includes grouping separators                                      |
| <space>     | A blank space adds a minus sign for negative numbers and a leading space when positive |


**Hex, oct and dec integer _printf_ examples**

|Pattern|Data|_Printf_ output|
|---|---|---|
|‘%d’|123,457,890|'123457890'|
|‘%,15d’|123,457,890|'    123,457,890'|
|‘%+,15d’|123457890|'   +123,457,890'|
|‘%-+,15d’|123457890|'+123,457,890   '|
|‘%0,15d’|123457890|'0000123,457,890'|
|‘%15o’|123457890|'      726750542'|
|‘%15x’|123457890|'        75bd162'|


**Java _printf_ format specifiers**

|_Printf_ specifier|Data type|
|---|---|
|%s|String of text|
|%f|floating point value (float or double)|
|%e|Exponential, scientific notation of a float or double|
|%b|boolean true or false value|
|%c|Single character char|
|%d|Base 10 integer, such as a Java int, long, short or byte|
|%o|Octal number|
|%x|Hexadecimal number|
|%%|Percentage sign|
|%n|New line, aka carriage-return|
|%tY|Year to four digits|
|%tT|Time in format of HH:MM:SS ( ie 21:46:30)|

**Java _printf_ cheatsheet**

|Pattern|Data|_Printf_ output|
|---|---|---|
|‘%s’|Java|'Java'|
|‘%15s’|Java|'           Java'|
|‘%-15s ‘|Java|'Java           '|
|‘%d’|123,457,890|'123457890'|
|‘%,15d’|123,457,890|'    123,457,890'|
|‘%+,15d’|123457890|'   +123,457,890'|
|‘%-+,15d’|123457890|'+123,457,890   '|
|‘%0,15d’|123457890|'0000123,457,890'|
|‘%15o’|123457890|'      726750542'|
|‘%15x’|123457890|'        75bd162'|
|‘%15f’|12345.123450|'   12345.123450'|
|‘%-15.3f’|12345.123450|'12345.123      '|
|‘%015.3f’|12345.123450|'00000012345.123'|
|‘%e’|12345.123450|'1.234579e+08'|
|‘%.2e’|12345.123450|'1.23e+08'|
|‘%7tH %<-7tM’|new Date()|'     22 35     '|
|‘%15tT’|LocalDateTime.now()|'       22:35:53'|
