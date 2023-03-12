- #ARM #Assembly Stack
	- The stack pointer (`sp`) is always 4 byte aligned. This is absolutely mandatory. However, due to the Procedure Call Standard for the ARM architecture (AAPCS), the stack pointer will have to be 8 byte aligned, otherwise funny things may happen when we call what the AAPCS calls as *public interfaces* (this is, code written by other people).
	- The value of `sp` when leaving the function should be the same value it had upon entering the function.
	  ```asm
	  sub sp, sp, #8  /* sp ← sp - 8. This enlarges the stack by 8 bytes */
	  str lr, [sp]    /* *sp ← lr */
	  ... // Code of the function
	  ldr lr, [sp]    /* lr ← *sp */
	  add sp, sp, #8  /* sp ← sp + 8. /* This reduces the stack by 8 bytes
	                                  effectively restoring the stack 
	                                  pointer to its original value */
	  bx lr
	  ```
	  ```asm
	  str lr, [sp, #-8]!  /* preindex: sp ← sp - 8; *sp ← lr */
	  ... // Code of the function
	  ldr lr, [sp], #+8   /* postindex; lr ← *sp; sp ← sp + 8 */
	  bx lr
	  ```
-