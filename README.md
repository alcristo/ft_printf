*This project has been created as part of the 42 curriculum by [alcristo](https://github.com/alcristo)*

# ft_printf

## Description

This project attempts to imitate C's `printf` function in order to print characters efficiently. However, it only supports characters, strings, pointers and memory addresses and signed, unsigned and hexadecimal integers. Floats were added for `push_swap`; longs were not.

This is a variadic function: the function accepts as arguments a string (the `format` string) an undefined number of arguments in many formats. The format type is determined by the `%` character followed y one of the set `cspdiuxX%`.

The function prints `format` along with the arguments in the established order and returns the number of printed characters, or `-1` if an issue arised.

Format variation is possible with flags.

## Instructions

### Compilación

This project has a Makefile with the following rules:

| Rule | Description |
| - | - |
| all | Compile the library `libftprintf.a` |
| clean | Remove temporary objects |
| fclean | Remove temporary objects and the library |
| re | Remove temporary objects and the library, then compile again |

To compile the library, execute in terminal:

```bash
make
```

To compile .c files with `ft_printf` include the `ft_printf,h` header and execute in terminal:

```bash
cc [files.c] libftprintf.a
```

### Funcionamiento

To use `ft_printf` in a C file, follow the format:

```c
ft_printf(char *format, ...)
```

To write an argument, write one of the following format identifiers:

| Format identifier | Description |
| - | - |
| `%c` | Write a character |
| `%s` | Write a string |
| `%p` | Write a pointer's memory address in hexadecimal notation |
| `%d` | Write an integer |
| `%i` | Write an integer |
| `%u` | Write an unsigned integer |
| `%x` | Write an hexadecimal integer with lowercase letters |
| `%X` | Write an hexadecimal integer with lowercase letters |
| `%%` | Write a percentage sign |
| `%f` | Write a floating point number. Not required by the subject. Default precision is 6 decimals |

Alternatively, flags can be used, and the minimum width and precision may be defined. If `a` is any format identifier, 

Alternativamente se pueden usar flags y definir la anchura mínima y la precisión. Para ello se debe indicar entre el '%' y cualquier identificador 'a'. Siempre deben tener el siguiente orden:

```c
ft_printf("%[flags][width].[precision]/[file_descriptor]a", ...)
```

The minimum width is the minimum number of characters that must be printed. Adds spaces to the left if no flags say the opposite. It's always `1` for `%%`.

Precision marks the number of digits that must be written. Must be defined after a `.` character. If greater than the number of digits, printing will add zeros to the left.

The file descrptor was implemented for `push_swap`; it wasn't required by the subject and is not in the original `printf` function.

There are 5 possible flags:

| Flag | Description |
| - | - |
| `-` | Adds space padding to the left. Has priority over `0` |
| `0` | Replaces space padding with zeros |
| `#` | Prints alternative version for hexadecimal numbers, adding `0x` or `oX` to the left |
| `+` | For pointers and signed and unsigned integers, justify positive numbers with a `+` sign. Has priority over ` `  |

## Algorithm

First, the function iterates over the format string (protected against `NULL`), writing it. If a `%` character is detected, it will search for flags. If no flags, the function will execute a simple printing algorithm depending on the format. If the number of printed characters is in any moment `-1`, printing will stop and returns `-1`. Else it adds the number of printed characters as they get printed.

If a flag is detected, the function allocates memory for a structure with 7 integers: 5 for the flags and other 2 for the width and precision. First, a zero is set for every flag and assigns 1 for each one if found. Then, the width and precision are set to `0` and `-1` respectively. If precision and flag `0` is active, spaces will be printed instead of zeros. After parsing flags, a more complex algorithm is applied. Finally, the structure memory is freed.

This complex algorithm will first count the number of characters that the simple algorithm would print. Then spaces will be added as padding if `-` is not active, a process that has its own function depending on the flags. Next the argument is printed. Finally adds a right padding if `-` is active.

Left padding requires comparing width ($w$) and precision ($p$). If $w>p$ the sign and zeros are printed. Else, the function will check for the `-` flag. If marked, the sign and zeros are printed, else spaces are printed until the padding is satisfied. If `0` flag is active the sign is printed first (`+`, `-`, ` ` or `0x`) and then checks for the previously described condition to print zeros depending on the width and the precision.

## Resources

[This web page](https://es.cppreference.com/c/variadic) Heped me understand what a variadic function was.

[W3Schools page for `printf`](https://www.w3schools.com/c/ref_stdio_printf.php) was used to understand how the `printf` flags worked.

[Francinette](https://github.com/WaRtr0/francinette-image) was used for testing.

### AI Usage

AI wasn't used for this project.
