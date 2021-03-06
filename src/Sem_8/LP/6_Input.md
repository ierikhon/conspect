# Операторы ввода/вывода, `repeat`, `fail`
## Операторы ввода/вывода
* `read(X)` - считываение `X` из входного потока.
* `write(X)` - вывод `X` во входной поток.
* `nl` - вывод в поток оператора перевода каретки

### Работа с файлами
* `see(filename)` - перенаправляет входной поток в файл с именем `filename`.  
    `see(User)` - считывание из консоли.
* `seen` - закрывает чтение из файла
* `tell(filename)` - перенаправляет выходной поток в файл.  
    `tell(User)` - вывод в консоль.
* `told` - закрывает запись в файл.

Чтение файла производится последовательно. После чтения позиция в файле изменится на следующий непрочитанный символ; считанную один раз из файла информацию считать вторично невозможно.

Значения в файле должны быть закончены точкой. Если вводится не число, а текст, должны быть маленькие буквы; слова с большими буквами должны быть заключены в кавычки.

Если чтение производится в конце файла, возвращается атом `end_of_file`.

## `repeat` и `fail`
Оператор `repeat` в любом направлении заканчивается удачей, `fail` - неудачей.

Реализация оператора `repeat`:
```prolog
repeat.
repeat :- repeat.
```

С помощью `repeat` и `fail` можно создать бесконечный цикл, например, так:
```prolog
:- ..., repeat, ..., fail.
```

## Примеры использования
### Квадраты чисел
Считывать с клавиатуры квадраты чисел, пока не введен `stop`.

```prolog
do :- repeat, nl, read(X), (X = stop, ! ; X1 is X * X, write(X1), nl, fail).
```

```prolog
| ?- do.

256.
65536

stop.

(1 ms) yes

```

