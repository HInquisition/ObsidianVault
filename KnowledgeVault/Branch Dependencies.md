# Branch Dependencies

What happens when a [[Pipelined CPU]] encounters a conditional branch instruction (e.g., an if statement, or the conditional expression at the end of a for or while loop)? To answer this question, let’s consider the following C/C++ code:
```cpp
int SafeIntegerDivide(int a, int b, int defaultVal)
{
return (b != 0) ? a / b : defaultVal;
}
```
If we looked at the disassembly for this function, it might look something like
this on an Intel x86 CPU:
```
; function preamble omitted for clarity...
; first, put the default into the return register
mov eax,dword ptr [defaultVal]
mov esi,dword ptr [b]                   ; check (b != 0)
cmp esi,0
jz SkipDivision
mov eax, dword ptr[a]                   ; divisor (a) must be in EDX:EAX
cdq                                     ; ... so sign-extend into EDX
idiv esi                                ; quotient lands in EAX
SkipDivision:
; function postamble omitted for clarity...
ret                                     ; EAX is the return value
```

The dependency here is between the `cmp` (compare) instruction and the `jz`
(jump if equal to zero) instruction. The CPU cannot issue the conditional jump
until it knows the results of the comparison. This is called a <mark style="background: #D2B3FFA6;">branch dependency</mark>
(also known as a <mark style="background: #D2B3FFA6;">control dependency</mark>).

![[Pasted image 20221122141536.png]]