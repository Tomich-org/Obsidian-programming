Вещественные числа поддерживают те же операции, что и целые. Однако (из-за представления чисел в компьютере) вещественные числа неточны, и это может привести к ошибкам:
```py
>>> 0.1 + 0.1 + 0.1 + 0.1 + 0.1 + 0.1 + 0.1 + 0.1 + 0.1 + 0.1
0.9999999999999999
```

Для высокой точности используются объекты, например, [[Decimal]] и [[Fraction]]
### Дополнительные методы
1. `float.as_integer_ratio()` - пара целых чисел, чьё отношение равно этому числу.
2. `float.is_integer()` - является ли значение целым числом.
3. ``float.hex()`` - переводит float в hex (шестнадцатеричную систему счисления).
4. ``float.fromhex(s)`` - float из шестнадцатеричной строки.

#python #основы #числа #тип_данных 