# later

## dependencies

 * perl

### optional dependencies (see `-t` command-line option)

 * curl
 * HTML::Parser ([perl module](http://search.cpan.org/dist/HTML-Parser/))

## command-line options

    later [options] [URL] [memo ...]

      General options:
        -h, --help        print this message and exit
        -v, --version     print version and exit
        -q, --quiet       disable output
        -f FILE           file on which to operate (default is $HOME/.later)

      Add options:
        -a                append entry to FILE (default is prepend)
        -t                add URL title to entry (requires curl, HTML::Parser)

      Open options:
        -o NUMBERS*       open entries with given NUMBERS
        -O ENTRY          open given ENTRY
        -k                keep entries after opening (default is remove)

      Manipulate options:
        -l [d]            list contents of FILE with numbered lines,
                          descending if d is given (default is ascending)
        -r NUMBERS*       remove from FILE entries with given NUMBERS

      *accepts a range of numbers separated by a hyphen (e.g. 1-9)

#### examples

    later -t https://github.com/supplantr/later this is all part of the memo
    later -f /path/to/file -o 2 5 12-15

## example scripts

Copy URL from clipboard and use `dmenu` to prompt for memo:

    #!/bin/bash

    later -q -t "$(xsel -b)" "$(dmenu -p memo: <&-)"

Pipe file into `dmenu` and open selected entry:

    #!/bin/bash

    if [[ -f "$1" ]]; then
        FILE="$1"
    else
        FILE="$HOME/.later"
    fi

    later -q -O "$(dmenu -l 30 < $FILE)"

## known issues

 * HTML header parsing errors (such as
   [this](https://github.com/libwww-perl/http-message/issues/3)) are printed
   but otherwise ignored.
