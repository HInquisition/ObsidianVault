# Critical Races

Sometimes [[Race Condition|race conditions]] are innocuous—the behavior of the program may change somewhat depending on timing, but the race causes no ill effects. On the other hand, a critical race is a race condition that has the potential to cause incorrect program behavior.

The kinds of bugs caused by critical races often seem “strange” or even “impossible” to programmers who aren’t experienced with them. Examples include:
- intermittent or seemingly random bugs or crashes,
- incorrect results,
- data structures that get into corrupted states,
- bugs that magically disappear when you switch to a debug build,
- bugs that are around for a while, and then go away for a few days, only to return again (usually the night before E3!),
- bugs that go away when logging (a.k.a., “`printf()` debugging”) is added to the program in an attempt to discover the source of the problem.

Programmers often call these kinds of issues Heisenbugs.