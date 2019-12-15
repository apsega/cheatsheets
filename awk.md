# Awk

## Basics

    awk program file

Program is ;-separated pattern-action statements.

    /pattern/ { action }
    # e.g. (apostrophes to not interpolate shell vars
    awk '/tt/ { print $1 }' awk.md

`$0` is whole line, `$1`, `$2`, ... are fields separated by `FS` (by default,
whitespace).

