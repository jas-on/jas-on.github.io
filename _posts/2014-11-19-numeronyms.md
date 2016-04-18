---
layout: post
title: Numeronyms
summary: TIL
---
TIL about [numeronyms](https://en.wikipedia.org/wiki/Numeronym).

>the letters between the first and last are replaced with a number representing the number of letters omitted

Now I finally know why "A16Z" is Andreessen Horowitz and "i18n" is internationalization.

Counting takes too long...

```bash
#!/bin/bash

if [[ $# -eq 0 ]] ; then
    echo 'Pass in some strings.'
    exit -1
fi

LETTER_COUNT=-2 # account for first and last character
FIRST_CHAR="${1:0:1}" # get first character of first argument

# skip over the arguments and get last one
for last
do
    true
done

LAST_CHAR="${last: -1}" # get last character of last argument

# determine total character length of all of the arguments
# do not count whitespace between arguments
for word in "$@"
do
    LETTER_COUNT=$((LETTER_COUNT + ${#word}))
done

case $LETTER_COUNT in
    # if there is only one character
    1) echo "Get a longer string!"
        ;;

    # if there are two or more characters
    *) echo "Your numeronym is: $FIRST_CHAR$LETTER_COUNT$LAST_CHAR"
        ;;
esac

exit 0
```

```
» ./nmrnym johndoe
Your numeronym is: j5e
```
