# Uxn notes

```
( comment )
```

Requires spaces, ignored by assembler

```
LIT - LITeral - push the next byte in memory onto the stack
LIT 68
```

```
DEO - DEvice Output - push byte A onto device address B
LIT 68 LIT 18 DEO
```

## Runes

```
| Absolute pad - the address to write the next items in memory
|0100 - 2 bytes - main memory
|01 - 1 byte - I/O memory or zero page (???)
```

```
$ Relative pad (I think) - nudge the addressed memory location along
```

```
@ Label,
& Sub-label
|10 @Console &vector $2 &read
```

Defines `.Console\vector` as address 10, `.Console\read` as address 12
See <https://wiki.xxiivv.com/site/varvara.html#console>

```
# Literal rune - just sugar for LIT
#53 #18 DEO ( output S )
```

```
" Raw character rune - convert an ascii character to raw numeric value
LIT "S #18 DEO
```

The quote `"` rune doesn't push to the stack, so you still need the LIT command.

## Macro

Define a macro with the `%` rune

```
%MACRO_NAME { ( instructions go here ) }
```

## Screen

x,y is left,top based

To draw a pixel, push to x, and y, and then pixel (to set the colour/layer)

Watch out that your labels and sub-labels are right for the screen device, or no pixel will appear. Check the official varvara page.






