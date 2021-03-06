﻿Решение для конкурса по программированию на JS: Классификатор слов / 2016 / Алексей Борисов

Суммарный размер файлов: 65531 байт
Средний результат: 82.09% на выборке из 1000000 элементов
Затраченное время на задачу: суммарно 40 часов
Лицензия: Creative Commons

Основные тезисы:
* от слов отрезаются самые частые окончания 's, s, ing; слова с апострофом считаются ложными
* основной алгоритм похож на фильтр Блума:
  для каждого слова считается хеш-функция, по получившемуся индексу в чанке устанавливается единичный бит;
  размер чанка подобран так, что после прохода по словарю остаётся приблизительно 15 нулевых битов;
  позиции этих нулевых битов сохраняются в файл;
  дальше происходит заполнение нового чанка с новой хеш-функцией, всего таких хеш-фунций около 3000;
  при тестировании слова происходит проверка, не попала ли хеш-функция слова на один из этих нулевых битов
  
* дополнительно используются эвристики для отсечения ложноположительных срабатываний (+4% правильных ответов)
* стоит уделить внимание изменяемой хеш-функции, небольшие изменение в мутаторе хеш-функции дали прирост +3%
* для улучшения сжатия файла (~+7% к степени сжатия), сохраняются только расстояния между нулевыми битами, старшие байты, которые имеют схожие значения рядом с нулём, перенесены в отдельную часть файла (сделано с расчётом на gzip, для других архиваторов такая предварительная обработка может навредить)
* на небольших выборках (~1000 элементов) очень большая погрешность при оценке эффективности, использовалась выборка 1000000 элементов
* предварительная версия писалась на C, это позволило быстро проверять гипотезы на больших объёмах данных
