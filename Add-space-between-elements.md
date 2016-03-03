## Problem

Rendered Jade leaves no space between elements, but sometimes you want to space them, especially when interpolating strings.

## Solution

Use CSS classes `.spl` and `.spr` (short for space-left, space-right) to add a single space to the left or right of the element.

## Example
```jade
p
  span.spr Click this
  a(href='#') link
  | !
```

In this case you would always add the .spr to the span, not a .spl to the link, so that the link is only the word 'link'.

