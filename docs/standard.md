# Proposed grammar/syntax

### Interpreter specific

#### Memory

Infinite tape-based memory system: One array, with the pointer starting at the center as index 0, all cells below are considered the "pull-up" and above are the "pull-down" (counter-intuitive, but works according to further syntax implementation discussed below) and this can move and point to different pairs in the array (pair being expanded below).

#### Data storage

The memory system will hold a pair in each cell of the array which stores an unsigned 32 bit integer (gate offset{8}, src offset{8}, drain offset{8}, type{1}) which represents the TRANSISTOR and an uint16 (state{2}, data_mode{1}, data{8}, charge_age{5}) which will represent the NODE. Note for the offset, to ensure the the tape can be use "infinitely", you can have it such that you can use a PMOS which has its, gate tied to GND which makes it act as a relay wire between cells that are greater than 128 cells apart (vice versa for the NMOS side) -> this routing is done by the interpreter though for both sides (positive and negative)

#### stdlib

This will be shared, with nanopulseOS and also here such that the language can be interpreted independently of the OS or with. This will also provide easier usage for certain tasks.

#### Internal Controller (for dev)

This more for devs, but my suggestion to ensure it is Turing complete (like bf) is to have a "controller" which dictates edits on the tape, like whether a new cmos needs to be created, removed, or edited (this would happen every net connection completion).

#### Generator

Maybe we will, need some sort of CMOS netlist generator of sorts to translate tasks from other code to CMOS, because manual typing of this code will be a struggle.

#### Timing

Timing is important in digital systems, and it will be here too. One tick in .bf is every single character that you input, one by one. Here a "tick" will be such: everytime we reach the output result for a gate pattern, the pin will be "sampled" in such where the output will be calculated using the logic of your previous gates, whatever that may be and continue from there to the next list, the value being saved on that output.

#### Nets

No hard limit on net/wire naming, other then avoiding name collision with already existing reserved NAMES that may be implemented.

#### Errors

Many parallels can be drawn from actual cmos circuitry where an error will occur if grammar is not followed, but mainly from when it runs where, if you were to drive both the pull-up and down at the same time (both are in parallel) the output would be SMOKE, as that is something you don't want happening. In fact, we may add extra features to punish it. Bad connections and what not, will also break.

### Esolang specific

#### Grammar

TODO: Use proper grammar format: <https://www.cs.cmu.edu/~pattis/misc/ebnf2.pdf>

#### Syntax

Series: `. (a.b)`

Parallel: `, (a,b)`

Separate pull-up to pull-down: `/ (a.b)/(a,b)`

Output: `> (a.b)/(a,b)>c`

<img width="310" height="505" alt="image" src="https://github.com/user-attachments/assets/4f2f8b9f-0948-4910-b957-8c10dc406981" />


TODO: (some type of method to make modules/funcs/templates) ...

More info on the language (once completed) will exist on esolangs.org/cmos
