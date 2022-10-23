# Word in computer terms
The term “word” is often used to describe a multi-byte value. However, the
number of bytes comprising a word is not universally defined. It depends to
some degree on context.

Sometimes the term “word” refers to the smallest multi-byte value, namely
16 bits or two bytes. In that context, a double word would be 32 bits (four
bytes) and a quad word would be 64 bits (eight bytes). This is the way the
term “word” is used in the Windows API.

On the other hand, the term “word” is also used to refer to the “natural”
size of data items on a particular machine. For example, a machine with 32-bit
registers and a 32-bit data bus operates most naturally with 32-bit (four byte)
values, and programmers and hardware folks will sometimes say that such a
machine as a word size of 32 bits. The takeaway here is to be aware of context
whenever you hear the term “word” being used to refer to the size of a data
item.
#ComputerScience/ComputerArchitecture 