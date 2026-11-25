# Bash Cheatsheet

> A concise reference for Bash scripting syntax, shell expansion, and practical command-line patterns.

## Table of Contents
- [Variables](#variables)
- [Conditionals](#conditionals)
- [Loops](#loops)
- [Functions](#functions)
- [String Manipulation](#string-manipulation)
- [Arrays](#arrays)
- [I/O Redirection](#io-redirection)
- [Command Substitution](#command-substitution)
- [Special Variables](#special-variables)
- [Test Operators](#test-operators)
- [Useful One-liners](#useful-one-liners)

## Variables

| Snippet | Description |
| --- | --- |
| `name="value"` | Assign a value without spaces around the equals sign. |
| `echo "$name"` | Expand a variable safely inside double quotes. |
| `readonly NAME=value` | Declare a variable that cannot be reassigned. |
| `local name=value` | Define a function-local variable. |
| `export NAME=value` | Export a variable to child processes. |
| `unset name` | Remove a variable from the shell environment. |
| `${name:-default}` | Use a default when a variable is unset or empty. |
| `${name:=default}` | Assign and use a default when a variable is unset or empty. |
| `${name:?message}` | Abort expansion with a message when a variable is unset or empty. |
| `declare -p name` | Display a variable's attributes and value. |

## Conditionals

| Snippet | Description |
| --- | --- |
| `if command; then ... fi` | Run a block when a command succeeds. |
| `if ...; then ... else ... fi` | Choose between two conditional branches. |
| `if ...; then ... elif ...; then ... fi` | Evaluate multiple conditional branches. |
| `case "$value" in pattern) ... ;; esac` | Match a value against several patterns. |
| `[[ "$name" == admin ]]` | Perform a Bash conditional string comparison. |
| `[[ "$file" == *.log ]]` | Match a string against a glob pattern. |
| `[[ "$a" -lt "$b" ]]` | Compare two integer values. |
| `command && success` | Run the second command only after success. |
| `command || fallback` | Run the fallback only after failure. |

## Loops

| Snippet | Description |
| --- | --- |
| `for item in "${items[@]}"; do ... done` | Iterate over array elements safely. |
| `for file in *.log; do ... done` | Iterate over files matching a glob. |
| `for ((i=0; i<10; i++)); do ... done` | Run a C-style arithmetic loop. |
| `while read -r line; do ... done < file` | Read a file line by line without altering backslashes. |
| `while condition; do ... done` | Repeat while a command succeeds. |
| `until condition; do ... done` | Repeat until a command succeeds. |
| `break` | Exit the current loop immediately. |
| `continue` | Skip to the next loop iteration. |

## Functions

| Snippet | Description |
| --- | --- |
| `name() { commands; }` | Define a Bash function. |
| `function name { commands; }` | Define a function using Bash's alternate syntax. |
| `name arg1 arg2` | Invoke a function with positional arguments. |
| `local result="$1"` | Store a function argument in a local variable. |
| `return 0` | Return a successful status from a function. |
| `return 1` | Return a failure status from a function. |
| `source ./lib.sh` | Load function definitions from another file. |
| `name "${args[@]}"` | Pass all array elements as separate function arguments. |

## String Manipulation

| Snippet | Description |
| --- | --- |
| `${#value}` | Return the length of a string. |
| `${value:0:5}` | Extract five characters starting at index zero. |
| `${value#prefix}` | Remove the shortest matching prefix. |
| `${value##*/}` | Remove the longest prefix through the final slash. |
| `${value%suffix}` | Remove the shortest matching suffix. |
| `${value%%.*}` | Remove the longest suffix beginning with a dot. |
| `${value/foo/bar}` | Replace the first matching substring. |
| `${value//foo/bar}` | Replace every matching substring. |
| `${value,,}` | Convert a string to lowercase. |
| `${value^^}` | Convert a string to uppercase. |

## Arrays

| Snippet | Description |
| --- | --- |
| `items=(one two three)` | Create an indexed array. |
| `items+=(four)` | Append an element to an indexed array. |
| `${items[0]}` | Read the first array element. |
| `${items[@]}` | Expand all array elements as separate words when quoted. |
| `${#items[@]}` | Return the number of array elements. |
| `unset 'items[1]'` | Remove one indexed array element. |
| `declare -A config` | Declare an associative array. |
| `config[port]=8080` | Assign a value to an associative-array key. |
| `${!config[@]}` | Expand all associative-array keys. |

## I/O Redirection

| Snippet | Description |
| --- | --- |
| `command > file` | Redirect standard output and overwrite a file. |
| `command >> file` | Append standard output to a file. |
| `command < file` | Read standard input from a file. |
| `command 2> errors.log` | Redirect standard error to a file. |
| `command &> output.log` | Redirect both output streams to a file. |
| `command 2>&1` | Redirect standard error to standard output. |
| `command1 | command2` | Pipe output from one command into another. |
| `command <<EOF ... EOF` | Pass a here-document as standard input. |
| `command <<< "$value"` | Pass a string as standard input with a here-string. |
| `command &` | Run a command asynchronously in the background. |

## Command Substitution

| Snippet | Description |
| --- | --- |
| `result=$(command)` | Capture command output in a variable. |
| `printf '%s\n' "$(date +%F)"` | Embed command output in another command. |
| `mapfile -t lines < <(command)` | Read process output into an array by line. |
| `diff <(sort a) <(sort b)` | Compare outputs from two commands. |
| `$(<file)` | Read a file efficiently in Bash. |
| `for user in $(cat users); do ...; done` | Iterate over whitespace-separated command output. |

## Special Variables

| Snippet | Description |
| --- | --- |
| `$?` | Expand to the previous command's exit status. |
| `$#` | Expand to the number of positional arguments. |
| `$@` | Expand to all positional arguments as separate words when quoted. |
| `$*` | Expand to positional arguments joined by the first `IFS` character when quoted. |
| `$0` | Expand to the script or shell name. |
| `$1` | Expand to the first positional argument. |
| `$$` | Expand to the current shell's process ID. |
| `$!` | Expand to the process ID of the most recent background job. |
| `$-` | Expand to the shell's current option flags. |
| `$_` | Expand to the last argument of the previous command in Bash. |

## Test Operators

| Snippet | Description |
| --- | --- |
| `[[ -e "$path" ]]` | Test whether a path exists. |
| `[[ -f "$path" ]]` | Test whether a path is a regular file. |
| `[[ -d "$path" ]]` | Test whether a path is a directory. |
| `[[ -r "$path" ]]` | Test whether a path is readable. |
| `[[ -x "$path" ]]` | Test whether a path is executable. |
| `[[ -z "$value" ]]` | Test whether a string is empty. |
| `[[ -n "$value" ]]` | Test whether a string is non-empty. |
| `[[ "$a" == "$b" ]]` | Test exact string equality. |
| `(( count > 0 ))` | Test an arithmetic expression. |
| `[[ "$a" =~ regex ]]` | Test a string against an extended regular expression. |

## Useful One-liners

| Snippet | Description |
| --- | --- |
| `set -euo pipefail` | Enable exit-on-error, unset-variable, and pipeline safety options. |
| `trap 'rm -f "$tmp"' EXIT` | Clean up a temporary file when the script exits. |
| `printf '%s\n' "$value"` | Print a value without interpreting escape sequences. |
| `read -r -p 'Name: ' name` | Prompt for input while preserving backslashes. |
| `command -v git >/dev/null || exit 1` | Require an executable before continuing. |
| `printf '%s\n' *.log` | Print matching filenames one per line. |
| `xargs -n1 command < list.txt` | Run a command once for each input item. |
| `find . -type f -print0 | xargs -0 chmod 644` | Safely process filenames containing spaces. |
| `printf '%s\n' "$PATH" | tr ':' '\n'` | Display each PATH entry on its own line. |
| `exec > >(tee -a script.log) 2>&1` | Send script output to both the terminal and a log. |
