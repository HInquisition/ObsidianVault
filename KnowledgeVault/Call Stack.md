#ComputerScience/ComputerArchitecture 
#Memory 
# Program Stack

Когда исполняемая программа загружается в память и запускается, операционная система резервирует область памяти для стека программы. Всякий раз, когда вызывается функция, область стековой памяти помещается в стек — мы называем этот блок памяти кадром стека. Если функция a() вызывает другую функцию b(), новый кадр стека для b() помещается над кадром a(). Когда b() возвращает управление, ее кадр стека выталкивается и выполнение продолжается там, где была остановлена a().

Кадр стека хранит три вида данных.
1. Адрес возврата вызывающей функции, так что, когда вызываемая функция возвращает управление, выполнение программы продолжится в вызывающей функции.
2. Содержимое всех соответствующих [[Registers |регистров ЦП]]. Это позволяет новой функции использовать регистры любым удобным для нее способом, не опасаясь перезаписи данных, необходимых для вызывающей функции. После возврата в вызывающую функцию состояние регистров восстанавливается, так что выполнение вызывающей функции может возобновиться. Возвращаемое значение вызываемой функции, если таковое имеется, обычно оставляется в определенном регистре, чтобы вызывающая функция могла получить его, но остальные регистры восстанавливаются до первоначальных значений.
3. Все локальные переменные, объявленные функцией (известны также как автоматические переменные). Это позволяет каждому отдельному вызову функции сохранять собственную копию каждой локальной переменной, даже когда функция вызывает сама себя рекурсивно. (На практике некоторые локальные переменные фактически распределяются по регистрам ЦП, а не хранятся в кадре стека, но по большей части они работают так, как если бы размещались в кадре стека функции.)

Вталкивание и выталкивание кадров стека обычно осуществляется установкой значения одного регистра в ЦП, известного как указатель стека.

Когда функция, содержащая автоматические переменные, возвращается, ее стековый фрейм прекращает существование и все автоматические переменные в функции должны обрабатываться так, как будто их больше не существует. Технически память, занятая этими переменными, все еще находится в оставленном кадре стека, но она, скорее всего, будет перезаписана, как только будет вызвана другая функция.

Пример работы стека:
```C++
void c()
{
	U32 localC1;
	// ...
}

F32 b()
{
	F32 localB1;
	I32 localB2;
	// ...
	c();
	// ...
	return localB1;
}

void a()
{
	U32 aLocalsA1[5];
	// ...
	F32 localA2 = b();
	// ...
}
```

![[Pasted image 20220923163802.png]]