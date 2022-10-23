[[C++]]

Assertation (Утверждения) - строка кода, проверяющее условие. Если результат выражения ложный - генерируется исключение, по возможности вызывается отладчик. Утверждения позволяют диагностировать ошибки сразу по мере их возникновения.

Пример:
`assert(PointerThatShouldBeAlwaysValid);`
`assert(CurrentArrayIndex < ArrayLength);`

По сути, Assertation - макросы. Из этого вытекает приятное свойство - они могут быть полностью удалены в Shipping сборках. Соответственно нулевые затраты по производительности. 

Помимо runtime assertations, существуют еще и static assertations, выполняющие проверки во время компиляции.

Пример:
`static_assert (bool_constexpr, message)`
`static_assert(2+2==1+1,"2+2 != 1+1");`

В С++ можно использовать `assert() ` и `static_assert() `из `#include <cassert>`

В [[Unreal Engine]] есть своя библиотека макросов для этих целей.
Существуют 3 семейства макросов, эквивалентных `assert()`

1. Check - наиболее близок к оригинальному assert, игнорируется в Shipping сборках
2. Verify - в большей части типов сборок ведет себя аналогично Check. Verify вычисляет выражение вне зависимости от того, выполняются проверки check или нет. 

	Например :
	`verify(CriticalFucntion)`
	
	// We use verify instead of check because our expression has a side effect (setting Mesh).
	`verify((Mesh = GetRenderMesh()) != nullptr);`

3. Ensure - особенность данных макросов в том, что они не вызывают исключения, а просто сообщают отладчику о том, что что-то пошло не так.

Существуют различные вариации каждого из макросов, о них больше тут:

https://docs.unrealengine.com/4.26/en-US/ProgrammingAndScripting/ProgrammingWithCPP/Assertions/
`Engine/Source/Runtime/Core/Public/Misc/AssertionMacros.h`
