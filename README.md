# Brainfuck Interpreter in Brainfuck
## Program structure
### Execution
1) Read and save the code
2) Set Pointer and Carret
3) Start Main loop
	1) Handle brackets \[ \]
	2) Handle other commands + - < > . ,
	3) Move carret
### Memory
Every odd cell is holding a value (code or tape) every other cell is a "backpack"-cell and set to zero.
Between Code and tape is one empty cell.
The backpack-cell in front of the active command (carret) and in front of the active cell (pointer) are set to 1. 
The backpack-cells are used as space for the different operations and have to be reset when leaving (0 for normal cells and 1 for carret and pointer).
Every time a value is needed somewhere else (e.g. +-<>., are interpretet on the tape so the command has to be copied to a backpack cell in the tape area) it is "put in the backpack". 
That means, that the value is copied into the next backpack cell and copied along while you are "wandering" to your destination. 
```
Code: +++[->+<]>

Before execution
|1|+|0|+|0|+|0|[|0|-|0|>|0|+|0|<|0|]|0|>|0|0|1|0|0|0|0|0|...
 ^carret                                     ^Pointer

After first command (+)
|0|+|1|+|0|+|0|[|0|-|0|>|0|+|0|<|0|]|0|>|0|0|1|1|0|0|0|0|...

After full execution
|0|+|0|+|0|+|0|[|0|-|0|>|0|+|0|<|0|]|0|>|1|0|0|0|1|3|0|0|...
```
