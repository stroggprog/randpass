# randpass

A simple, yet flexible, random password generator.

  - Passwords are of an arbitrarily specified length
  - All output is to STDERR except the generated password

## How it works
The passwords are generated from a string of UTF-8 characters, known as the origin string. The string is used to generate a grid of randomly positioned characters. Each character appears exactly n<sup>n</sup> times, where `n` is the number of characters in the initial string.

Further, each character only appears once per line of the grid. The number of times it may appear in each column is somewhere in the range 0-n.

Once the grid has been created, the generator fetches two more random numbers to act as `x` and `y` coordinates into the grid. It will repeat this, copying the characters at each coordinate to the end of the password until the password is of the required length. The password may contain repeated characters, even if it did not repeat any coordinates.

The closer the length of the requested password is to the length of the origin string, the more likely coordinates will be repeated.

## Options
Form the help (`randpass -h`):

```
Options:
    <n> = number of characters in password returned
    -e  = echo password to STDERR (still also goes to STDOUT)
    -g  = print randomly generated grid result is generated from
    -h  = print this help and exit
    -l  = limit output (almost quiet, just version and password)
    -q  = quiet mode (only print password)

Options can be strung together, e.g. -gq
    -q overrides -l but not -e
    -h overrides everything

Note that only the password is output to STDOUT, everything else goes to STDERR,
so redirection to a file is safe as only the password is redirected.
```
