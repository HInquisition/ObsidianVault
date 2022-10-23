# Процессор
Процессор — это мозг компьютера. Он состоит из следующих компонентов:

 - [[ALU|Aрифметико-логического устройства]] (АЛУ/ALU) для выполнения арифметических действий с целыми числами и побитового сдвига;
 
 - [[Floating-point unit, FPU|Модуля операций с плавающей точкой]] (floating-point unit, FPU) для реализации арифметики с [[Запись числа с плавающей точкой|числами с плавающей точкой]] (обычно с использованием стандартного представления IEEE 754); 

- [[Vector processing unit, VPU|Модуля векторной обработки]], имеющегося практически у всех современных процессоров, который способен выполнять операции с плавающей точкой и целочисленные операции над несколькими элементами данных параллельно;

- контроллера памяти ([[Memory controller]], MC) или блока управления памятью (memory management unit, MMU) для взаимодействия с устройствами памяти на чипе и вне его;

- набора [[Registers|регистров]], которые служат временным хранилищем во время расчетов (помимо прочего);

- блока управления ( [[CU, Control Unit]]) для декодирования и отправки инструкций на машинном языке другим компонентам на чипе и маршрутизации данных между ними.

Все эти компоненты приводятся в действие периодическим сигналом прямоугольной формы, известным как такт. Тактовая частота определяет частоту, с которой ЦП выполняет, например, инструкции или арифметические операции.

![[Pasted image 20221011174806.png]]