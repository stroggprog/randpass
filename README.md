# randpass

A simple, yet flexible, command-line random password generator.

  - Passwords are of an arbitrarily specified length (default=64)
  - All output is to STDERR except the generated password

Requirements: PHP >5.4

_built and tested with php 8.2_

## How it works
The passwords are generated from a string of UTF-8 characters, known as the origin string. The string is used to generate a grid of randomly positioned characters. Each character appears exactly n<sup>n</sup> times, where `n` is the number of characters in the initial string.

Further, each character only appears once per line of the grid. The number of times it may appear in each column is somewhere in the range 0-n.

Once the grid has been created, the generator fetches two more random numbers to act as `x` and `y` coordinates into the grid. It will repeat this, copying the characters at each coordinate to the end of the password until the password is of the required length. The password may contain repeated characters, even if it did not repeat any coordinates.

The closer the length of the requested password is to the length of the origin string, the more likely coordinates will be repeated.

## Options
From the help (`randpass -h`):

```
Options:
    <n> = number of characters in password returned
    -e  = echo password to STDERR (still also goes to STDOUT)
    -g  = print randomly generated grid result is generated from
    -h  = print this help and exit
    -l  = limit output (almost quiet, just version and password)
    -p  = print origin and exit
    -q  = quiet mode (only print password)

Options can be strung together, e.g. -gq
    -h overrides everything
    -p overrides everything except -h
    -q overrides -l but not -e

Note that only the password is output to STDOUT, everything else goes to STDERR,
so redirection to a file is safe as only the password is redirected.
```

If '?' character-on-a-background starts appearing in your passwords, then you need to remove any characters from the origin string that were created using the `AltGr` key, as these are almost certainly multi-byte characters, and this generator only works with single-byte UTF-8 characters. By default, there are no multi-byte characters in the origin.

You can include non-keyboard characters, such as `╚`, `╩` & `╝` etc., but these are best avoided for the obvious reason that they are hard to remember how to type since you need to know their ASCII codes. It can also be confusing too, as `}` (AltGr+0) and `}` (Shift+]) may look the same, but since they were created by different key combinations there is no guarantee they have the same UTF-8 code.
