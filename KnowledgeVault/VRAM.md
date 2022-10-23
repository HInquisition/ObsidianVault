# Video [[RAM]]

Raster-based display devices typically read a hard-wired range of physical
memory addresses in order to determine the brightness/color of each pixel on
the screen. Likewise, early charcter-based displays would determine which
character glyph to display at each location on the screen by reading ASCII
codes from a block of memory. A range of memory addresses assigned for
use by a video controller is known as video [[RAM]] (VRAM).

In early computers like the Apple II and early IBM PCs, video RAM used to
correspond to memory chips on the motherboard, and memory addresses in
VRAM could be read from and written to by the [[CPU]] in exactly the same way
as any other memory location. This is also the case on game consoles like the
PlayStation 4 and the Xbox One, where both the [[CPU]] and [[GPU]] share access to
a single, large block of unified memory.

In personal computers, the [[GPU]] often lives on a separate circuit board,
plugged into an expansion slot on the motherboard. Video [[RAM]] is typically
located on the video card so that the [[GPU]] can access it as quickly as possible.
A [[Bus]] protocol such as [[PCI]], AGP or [[PCI Express]] (PCIe) is used to transfer
data back and forth between “main [[RAM]]” and VRAM, via the expansion
slot’s bus. This physical separation between main RAM and VRAM can be
a significant performance bottleneck, and is one of the primary contributors
to the complexity of rendering engines and graphics APIs like [[OpenGL]] and
[[DirectX]] 11.