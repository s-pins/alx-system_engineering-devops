# Guide: 0x03 Shell, Init Files, Variables and Expansions

This guide provides a summary of the tasks completed, the concepts applied, and how to test each script.

## Core Concepts

This project revolves around fundamental shell features that are crucial for system administration and development.

*   **Shebang (`#!/bin/bash`)**: This is the very first line of every script. It tells the system to execute the script using the Bash interpreter.
*   **Executable Permissions**: For a script to run directly (e.g., `./my_script`), it must have the execute permission set. This is done with the command `chmod +x <filename>`.
*   **Variables**:
    *   **Local Variables**: Exist only within the current shell. They are created by simple assignment (e.g., `MYVAR="hello"`).
    *   **Environment (Global) Variables**: Are passed down to child processes. They are created using the `export` keyword (e.g., `export MYVAR="hello"`). The `printenv` command lists them.
    *   **Special Variables**: The shell provides many built-in variables, such as `$USER` (current user), `$PATH` (list of directories to search for commands), and `$?` (exit status of the last command).
*   **Expansions**:
    *   **Parameter Expansion**: Getting the value of a variable (e.g., `$USER`).
    *   **Arithmetic Expansion (`$((...))`)**: Performing integer math (e.g., `$((10 / 2))`). This also supports base conversion (e.g., `$((2#1011))` for binary).
    *   **Brace Expansion (`{..}`)**: Generating arbitrary strings (e.g., `echo {a..d}` prints `a b c d`).
    *   **Command Substitution (`$(...)`)**: Running a command and substituting its output (e.g., `echo "Today is $(date)"`).
*   **Piping (`|`) and Redirection (`<`, `>`)**:
    *   A pipe (`|`) sends the output of one command to the input of another.
    *   Redirection (`<`) reads input from a file.
*   **Sourcing (`source` or `.`)**: The `source` command (or its alias `.`) executes a script within the *current* shell, not a subshell. This is necessary when a script needs to modify the current shell's environment (e.g., setting an alias or exporting a variable).

## How to Test Each Script

Here is a breakdown of each script and how to verify its functionality. All tests should be run from the root of the project directory (`alx-system_engineering-devops`).

---

**0-alias**
*   **Purpose**: Creates an alias that makes the `ls` command behave like `rm *`.
*   **How to Test**:
    1.  `cd 0x03-shell_variables_expansions`
    2.  `touch file1 file2 file3` (Create some test files)
    3.  `ls` (Should list the new files)
    4.  `source ./0-alias` (Load the alias into the current shell)
    5.  `ls` (This will now execute `rm *` and delete the files. Be careful!)
    6.  `\ls` (Using a backslash bypasses the alias and shows the directory is now empty)
    7.  `cd ..` (Go back to the project root)

---

**1-hello_you**
*   **Purpose**: Prints "hello" followed by the current user's name.
*   **How to Test**: `./0x03-shell_variables_expansions/1-hello_you`
*   **Expected Output**: `hello <your_username>`

---

**2-path**
*   **Purpose**: Adds the `/action` directory to the end of the `PATH` variable for the current session.
*   **How to Test**:
    1.  `echo $PATH` (Note the current `PATH`)
    2.  `source ./0x03-shell_variables_expansions/2-path`
    3.  `echo $PATH` (You will see `:/action` appended to the end)

---

**3-paths**
*   **Purpose**: Counts the number of directories listed in the `PATH` variable.
*   **How to Test**: `./0x03-shell_variables_expansions/3-paths`
*   **Expected Output**: A single number representing the count of directories.

---

**4-global_variables**
*   **Purpose**: Lists all environment (global) variables.
*   **How to Test**: `./0x03-shell_variables_expansions/4-global_variables`
*   **Expected Output**: A long list of key-value pairs (e.g., `HOME=/home/user`, `PATH=...`).

---

**5-local_variables**
*   **Purpose**: Lists all local variables, global variables, and any defined functions.
*   **How to Test**: `./0x03-shell_variables_expansions/5-local_variables`
*   **Expected Output**: A very long list of variables and function definitions.

---

**6-create_local_variable**
*   **Purpose**: Defines a new local variable `BEST` with the value `School`.
*   **How to Test**:
    1.  `source ./0x03-shell_variables_expansions/6-create_local_variable`
    2.  `echo $BEST`
    3.  **Expected Output**: `School`

---

**7-create_global_variable**
*   **Purpose**: Creates a new global (environment) variable `BEST`.
*   **How to Test**:
    1.  `source ./0x03-shell_variables_expansions/7-create_global_variable`
    2.  `env | grep BEST`
    3.  **Expected Output**: `BEST=School`

---

**8-true_knowledge**
*   **Purpose**: Adds 128 to the value of the `TRUEKNOWLEDGE` environment variable.
*   **How to Test**:
    1.  `export TRUEKNOWLEDGE=1209`
    2.  `./0x03-shell_variables_expansions/8-true_knowledge`
    3.  **Expected Output**: `1337`

---

**9-divide_and_rule**
*   **Purpose**: Divides the `POWER` variable by the `DIVIDE` variable.
*   **How to Test**:
    1.  `export POWER=42784`
    2.  `export DIVIDE=32`
    3.  `./0x03-shell_variables_expansions/9-divide_and_rule`
    4.  **Expected Output**: `1337`

---

**10-love_exponent_breath**
*   **Purpose**: Calculates `BREATH` to the power of `LOVE`.
*   **How to Test**:
    1.  `export BREATH=4`
    2.  `export LOVE=3`
    3.  `./0x03-shell_variables_expansions/10-love_exponent_breath`
    4.  **Expected Output**: `64`

---

**11-binary_to_decimal**
*   **Purpose**: Converts a binary number (from `BINARY` variable) to decimal.
*   **How to Test**:
    1.  `export BINARY=10100111001`
    2.  `./0x03-shell_variables_expansions/11-binary_to_decimal`
    3.  **Expected Output**: `1337`

---

**12-combinations**
*   **Purpose**: Prints all two-letter combinations from `aa` to `zz`, except `oo`.
*   **How to Test**: `./0x03-shell_variables_expansions/12-combinations | wc -l`
*   **Expected Output**: `675` (which is 26*26 - 1)

---

**13-print_float**
*   **Purpose**: Prints the number in the `NUM` variable, formatted to two decimal places.
*   **How to Test**:
    1.  `export NUM=3.14159`
    2.  `./0x03-shell_variables_expansions/13-print_float`
    3.  **Expected Output**: `3.14`

---

**100-decimal_to_hexadecimal**
*   **Purpose**: Converts a decimal number (from `DECIMAL` variable) to hexadecimal.
*   **How to Test**:
    1.  `export DECIMAL=1337`
    2.  `./0x03-shell_variables_expansions/100-decimal_to_hexadecimal`
    3.  **Expected Output**: `539`

---

**101-rot13**
*   **Purpose**: Encrypts text from standard input using the ROT13 cipher.
*   **How to Test**:
    1.  `echo "Hello World" | ./0x03-shell_variables_expansions/101-rot13`
    2.  **Expected Output**: `Uryyb Jbeyq`
    3.  To decrypt, pipe the output back: `echo "Hello World" | ./101-rot13 | ./101-rot13` will return `Hello World`.

---

**102-odd**
*   **Purpose**: Prints only the odd-numbered lines from its input (1st, 3rd, 5th, etc.).
*   **How to Test**: `\ls -1 /etc | ./0x03-shell_variables_expansions/102-odd`
*   **Expected Output**: Every other file/directory name from the `/etc` directory.

---

**103-water_and_stir**
*   **Purpose**: Performs a complex multi-base addition problem.
*   **How to Test**:
    1.  `export WATER="ewwatratewa"`
    2.  `export STIR="ti.itirtrtr"`
    3.  `./0x03-shell_variables_expansions/103-water_and_stir`
    4.  The script uses `tr` to convert the letters in `WATER` and `STIR` to digits, `dc` (desk calculator) to perform the base-5 addition and convert the result to base-8, and `tr` again to convert the base-8 digits to the letters of `bestchol`.
