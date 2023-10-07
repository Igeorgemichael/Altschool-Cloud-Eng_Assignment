## [Assignment]() 2
### Task: 
* Research online for 15 more Bash Scripting operators and its usage
### Instruction:
- [ ] Submit your work in a folder for this exercise in your altschool-cloud-exercises project.
---

## [Research]() 

In Bash scripting, operators are used to perform various operations on data, variables, and files. Here are 15 common Bash operators along with descriptions:


1. Assignment Operator (=):
   - Description: Used to assign a value to a variable.

   - Example: `my_variable=10`

2. Arithmetic Operators (+, -, *, /, %):
   - Description: Used for basic arithmetic operations.
   - Examples:
     `a=5
     b=3
     sum=$((a + b))  # Addition
     diff=$((a - b)) # Subtraction
     prod=$((a * b)) # Multiplication
     quot=$((a / b)) # Division
     remainder=$((a % b)) # Modulus`


3. String Concatenation Operator (+=):
   - Description: Used to concatenate strings.
   - Example: 
     `str1="Hello,"
     str2="World!"
     combined_str="$str1$str2"`


4. Comparison Operators (==, !=, >, <, >=, <=):
   - Description: Used to compare values.
   - Examples:
     `c=5
     x=3
     if [ "$c" -eq "$x" ]; then
       echo "c is equal to x"
     fi`


5. Logical Operators (&&, ||, !):
   - Description: Used for logical operations.
   - Examples:
     `if [ "$a" -gt 0 ] && [ "$b" -lt 10 ]; then
       echo "a is greater than 0 and b is less than 10"
     fi`


6. Increment/Decrement Operators (++, --):
   - Description: Used to increment or decrement variable values.
   - Examples:
     `count=0
     count=$((count + 1)) # Increment
     count=$((count - 1)) # Decrement`


7. String Comparison (=~, !=~):
   - Description: Used for pattern matching in strings.
   - Example:
     `string="Hello, World!"
     if [[ "$string" =~ "Hello" ]]; then
       echo "String contains 'Hello'"
     fi`


8. Ternary Operator (? :):
   - Description: Used for conditional expressions.
   - Example:
     `age=18
     status=$((age >= 18 ? "Adult" : "Minor"))`


9. Null Coalescing Operator (??):
   - Description: Used to provide a default value if a variable is null.
   - Example:
     `input_value=""
     value=${input_value:-"Default Value"}`


10. Command Substitution (`` or $()):
    - Description: Used to execute a command and capture its output.
    - Example:
      `current_date=$(date)`


11. File Existence Operators (-e, -f, -d):
    - Description: Used to check if files or directories exist.
    - Examples:
      `file="myfile.txt"
      if [ -e "$file" ]; then
        echo "$file exists."
      fi`


12. String Length Operator (#):
    - Description: Used to get the length of a string.
    - Example:
      `text="Hello, World!"
      length=${#text}`


13. Array Operators (${array[@]}):
    - Description: Used to work with arrays.
    - Examples:
      `my_array=("pawpaw" "coconut" "mango")
      element=${my_array[1]} # Accessing an element
      length=${#my_array[@]} # Array length`


14. Bitwise Operators (&, |, ^, ~):
    - Description: Used for bitwise operations on integers.
    - Example:
      `num1=5
      num2=3
      result=$((num1 & num2)) # Bitwise AND`


15. File Redirection Operators (>, >>, <):
    - Description: Used to redirect input and output of commands.
    - Examples:
      `echo "Hello" > output.txt   # Redirect output to a file
      cat < input.txt             # Redirect input from a file
      echo "Append" >> output.txt # Append output to a file`
