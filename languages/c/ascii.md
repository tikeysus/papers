Noting down useful ascii-related things that I learn while coding in C. 

1. Checking if char input is a digit. 
- One option is to use a library. 
```
#include <ctype.h>

if (isdigit(*s)) {
    // it's a digit
}
```
- The better approach is to instead directly compare the ascii values and see if it falls in the right range. 
```
if (*s >= '0' && *s <= '9') {
    // it's a digit
}
```
