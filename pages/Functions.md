- #ARM #Assembly Functions
  title:: Functions
	- A function must be a a *well-behaved* citizen.
		- A function must adhere, at least, to the following rules if we want it to be AAPCS compliant.
		- A function should not make any assumption on the contents of the `cpsr`. So, at the entry of a function condition codes N, Z, C and V are unknown.
		- A function can freely modify registers `r0`, `r1`, `r2` and `r3`.
		- A function cannot assume anything on the contents of `r0`, `r1`, `r2` and `r3` unless they are playing the role of a parameter.
		- A function can freely modify `lr` but the value upon entering the function will be needed when leaving the function (so such value must be kept somewhere).
		- A function can modify all the remaining registers as long as their values are restored upon leaving the function. This includes `sp` and registers `r4` to `r11`.
		  *This means that, after calling a function, we have to assume that (only) registers `r0`, `r1`, `r2`, `r3` and `lr` have been overwritten*
	- Special Registers
		- r15 -> pc
		- r14 -> lr
	- Parameter Passing
	  Functions can receive parameters. The first 4 parameters must be stored, sequentially, in the registers `r0`, `r1`, `r2` and `r3`.
	- Leaving from Function
	  We have to put lr somewhere before we leave
	  And after we come back we have to put lr back in its place
	- Returning data from functions
	  Return the value by modifying r0
	-