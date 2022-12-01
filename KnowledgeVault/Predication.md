# Predication

Another way to mitigate the effects of [[Branch Dependencies]] is to simply avoid
branching altogether. 
```c++
float SafeFloatDivide(float a, float b, float d)
{
return (b != 0.0f) ? a / b : d;
}
```
This simple function calculates one of two answers, depending on the results of the conditional test `b != 0`. Instead of using a conditional branch statement to return one of these two answers, we can instead arrange for our conditional test to generate a bit mask consisting of all zeros (`0x0U`) if the condition is false, and all ones (`0xFFFFFFFFU`) if it is true. We can then execute both branches, generating two alterate answers. Finally, we use the mask to produce the final answer that we’ll return from the function.
```c++
int SafeFloatDivide_pred(float a, float b, float d)
{
// convert Boolean (b != 0.0f) into either 1U or 0U
const unsigned condition = (unsigned)(b != 0.0f);
// convert 1U -> 0xFFFFFFFFU
// convert 0U -> 0x00000000U
const unsigned mask = 0U - condition;
// calculate quotient (will be QNaN if b == 0.0f)
const float q = a / b;
// select quotient when mask is all ones, or default
// value d when mask is all zeros (NOTE: this won't
// work as written -- you'd need to use a union to
// interpret the floats as unsigned for masking)
const float result = (q & mask) | (d & ~mask);
return result;
}
```

The use of a mask to select one of two possible values like this is called predication because we run both code paths (the one that returns a / b and the one that returns d) but each code path is predicated on the results of the test (`b != 0`), via the mask. Because we are selecting one of two possible values, this is also often called a <mark style="background: #D2B3FFA6;">select operation</mark>.

Going to all this trouble to avoid a branch may seem like overkill. And it can be—its usefulness depends on the relative cost of a branch versus the predicated alternative on your target hardware. Predication really shines when a CPU’s [[ISA, Instruction Set Architecture|ISAs]] provide special [[Machine Language]] instructions for performing a select operation. For example, the PowerPC ISA offers an integer select instruction `isel`, a floating point select instruction `fsel`, and even a SIMD vector select instruction `vecsel`, and their use can definitely result in performance improvements on PowerPC based platforms (like the PS3).

It’s important to realize that predication only works when both branches can be executed safely. Performing a divide by zero operation in floating-point generates a quiet not-a-number (QNaN), but an integer divide by zero throws an exception that will crash your game (unless it is caught). 