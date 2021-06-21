CPP code review checklist
==========================

After getting many code reviews and performing code reviews I thought I would compile a decent list of gotchas.





- const correctness
- when doing an equality check of doubles and floats use approximates with an episilon
- If you're using an algorithm and not mutating use cbegin/cend versions
- if a member is default constructed you can skip listing it in the initializer list
- look for <algorithm> opportunities
- If passing in a variable into a function and it doesn't take ownership, prefer to pass by reference
- in a class, if you are disabling one of copy/move/assignment the others should be considered for disabling
- if working with packet of data and are using offsets, consider creating a struct, this simplifies offsets and creates self documenting code
- Look for opportunites to construct variables with the return value of the function
- For very long lambda functions consider a static or private method instead
- When using a type that is private to the class look to forward declare and move the include out of the header
- look for unsused private variables

#### Cmake ####

- Prefer to manually list out each file in an `add_library` versus using GLOB

