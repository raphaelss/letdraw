# Letdraw

Command-line drawing tool.
Letdraw reads one character at a time from input and interprets the supported
characters as instructions for a drawing machine.

## Supported characters

- =d= :: Move forward drawing line
- =u= :: Move forward without drawing
- =<= :: Turn 15 degrees counterclockwise
- =>= :: Turn 15 degrees clockwise
- =[= :: Push state (position and direction) into stack
- =]= :: Pop state (position and direction) from stack
  - Stack usage must be balanced (can't pop an empty stack).
- =o= :: Move to origin without drawing
- =r= :: Move to origin without drawing and reset angle to 0 degrees
- =#= :: Execute next instruction =#= times
  - =#= = any single digit number.
  - =#= instruction is cummulative. Ex.: =2d= = =dd=, =3d= = =ddd=, =23d= = =6d=

## Numeric repeat instructions

Numbers are interpreted as an instruction to execute the next operation /n/
times.
Ex.: the sequence =4d= draws a line four units long (same as =dddd=).
Numbers are read as individual digits and the repeating effect is
cumulative.
Ex.: The sequence =22d= does not mean the =d= instructions executed
twenty-two times. The first =2= is an instruction to execute the next
instruction 2 times.
In this case, the next instruction is also =2=. This causes =d= to be
executed 4 (2*2) times (same as =dddd=). =235d= as another example,
would execute =d= 30 (2*3*5) times.

# Usage

#+BEGIN_EXAMPLE
Usage: letdraw --out=FILE [OPTION]
  -h --help                Display this message
  -o --out=*.(pdf|png)     Output file (required)
  -i --in=FILE             Input file containing sequence of characters
                           If no file is specified, letdraw reads from
                           STDIN
  -w --width=NATURAL       Width of image canvas (default: 800)
  -H --height=NATURAL      Height of image canvas (default: 600)
  -x --origin_x=REAL       X of starting point (default: width/2)
  -y --origin_y=REAL       Y of starting point (default: height/2)
  -s --scale=REAL>0        Scale drawing lines (default: 1.0)
  -l --line_width=REAL>0   Width of line stroke (default: 2.0)
  -c --line_cap=(normal|round|square) Line end shape (default: normal)
Letdraw reads characters and treats some of them as instructions for a
drawing machine while ignoring the others.
Supported characters:
  d : Move forward drawing line
  u : Move forward without drawing
  < : Turn 15 degrees counterclockwise
  > : Turn 15 degrees clockwise
  [ : Push state (position and direction) into stack
  ] : Pop state (position and direction) from stack
  o : Move to origin without drawing
  r : Move to origin without drawing and reset angle to 0 degrees
  # : Repeat next instruction # times
\# == any single digit number.
\# instruction is cumulative. Ex.: 2d = dd, 3d = ddd, 23d = 6d.
Stack usage must be balanced (can't pop an empty stack).
#+END_EXAMPLE

# License

(See COPYING.txt for the GNU GENERAL PUBLIC LICENSE)

Copyright (C) 2014  Raphael Sousa Santos, http://www.raphaelss.com/

This program is free software: you can redistribute it and/or modify
it under the terms of the GNU General Public License as published by
the Free Software Foundation, either version 3 of the License, or
(at your option) any later version.

This program is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
GNU General Public License for more details.

You should have received a copy of the GNU General Public License
along with this program.  If not, see <http://www.gnu.org/licenses/>.