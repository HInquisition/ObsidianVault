# Data Dependencies

[[Pipeline Stalls]] are caused by dependencies between instructions in the instruction stream being executed. For example, consider the following sequence of instructions:
```
mov ebx,5                     ;; load the value 5 into register EBX
imul eax,10                   ;; multiply the contents of EAX by 10
;;                            ;; (result stored in EAX)
add eax,7                     ;; add 7 to EAX (result stored in EAX)
```

Ideally, we’d like to issue the `mov`, `imul` and add instructions on three consecutive clock cycles, to keep the pipeline as busy as possible. But in this case, the results of the `imul` instruction are used by the add instruction that follows
it, so the CPU must wait until the `imul` has made it all the way through the pipeline before issuing the add. If the pipeline contains five stages, that means four cycles are wasted (see [[Pipeline Stalls]]). These kinds of dependencies between instructions are called <mark style="background: #D2B3FFA6;">data dependencies</mark>.

![[Pasted image 20221122135345.png]]
Also, there are other types of dependencies: [[Branch Dependencies]] and [[Resource Dependencies]]