# Interrupts

An interrupt is a signal sent to the [[CPU]] in order to notify it of an important low-level event, such as a keypress on the keyboard, a signal from a peripheral device, or the expiration of a timer. When such an event occurs, an <mark style="background: #D2B3FFA6;">interrupt request</mark> (IRQ) is raised. If the operating system wishes to respond to the event, it pauses (interrupts) whatever processing had been going on, and calls a special kind of function called an <mark style="background: #D2B3FFA6;">interrupt service routine</mark> (ISR). The ISR function performs some operation in response to the event (ideally doing so as quickly as possible) and then control is returned back to whatever program had been running prior to the interrupt having been raised.

There are two kinds of interrupt: hardware interrupts and software interrupts.

![[Hardware Interrupts#Hardware interrupts]]

![[Software Interrupts#Software Interrupts]]

