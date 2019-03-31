# Скрипты в командном интерпретаторе Linux bash

### Оглавление

- [Запуск скрипта](#запуск-скрипта)
- [Объявление и использование переменных](#объявление-и-использование-переменных)
- [Передача параметров](#Передача-параметров)
- [Чтение данных из файла](#Чтение-данных-из-файла)
- [Запись данных в файл](#Запись-данных-в-файл)
- [Условный оператор if](#Условный-оператор-if)
- [Циклы](#Циклы)
- [Полезные ссылки](#Полезные-ссылки)


## Запуск скрипта

Для запуска файла скрипта используется команда `sh`

```sh
sh [file-name]
```

### Скрипт Hello World

Создаем текстовый файл содержащий

hello-world
```sh
echo Hello World 🖖
```

В директории с файлом в которытой консоле запускаем скрипт из файла

```sh
sh hello-world
```

Получаем

`Hello World 🖖`

## Объявление и использование переменных

В `bash` переменне объявляются просто

```sh
var1 = 1
var2 = "variable 2"
```

Для использования переменных необходимо поставить `$` перед их именем

```sh
var1 = 1
var2 = "variable 2"

echo $var1
echo var2
```

Result

```
1
var2
```

## Передача параметров

Зачастую необходимо передать параметры внутрь выполняемого скрипта. 
Можно провести аналогию с функциями в "обычных" языках программирования:

```js
function (art1, arg2, arg3, ...) => arg1 + arg2 + arg3 + ...
```

Передают аргументы в скрипт через пробел при вызове скрипта

```sh
sh file-name arg1 arg2 arg3 ...
```

Для использования аргументов внутри скрипта используется следующией синтаксис `$` и число `[0-9]`

```sh
echo $0 # Имя файла (путь к нему)
echo $1 # Первый аргумент arg1
echo $2 # Второй аргумент arg2
```

## Чтение данных из файла

Для чтения необходимо

- открыть файл
- прочитать символы
- сделать с символами что-нибудь
- закрыть файл

Используются следующие команды

Для открытия/закрытия

```sh
exec 3< thisfile          # open "thisfile" for reading on file descriptor 3
exec 4> thatfile          # open "thatfile" for writing on file descriptor 4
exec 8<> tother           # open "tother" for reading and writing on fd 8
exec 6>> other            # open "other" for appending on file descriptor 6
exec 5<&0                 # copy read file descriptor 0 onto file descriptor 5
exec 7>&4                 # copy write file descriptor 4 onto 7
exec 3<&-                 # close the read file descriptor 3
exec 6>&-                 # close the write file descriptor 6
```

**Важно: чтобы значение дескриптора всегда было одинаковое**

Пример чтения файла

*_file-read*
```sh
file_name="_data" # file name for reading

exec 10<$file_name # open file for reading on file desriptor 10

while read t <&10 # read lint
do
  echo "[$t]"
done
exec 10<&- # close file for reading on file desriptor 10
```

## Запись данных в файл

Запись в файл осуществляется командой `echo` и символами `>>` перед именем файла

```sh
echo "new line" >> _data
```

## Условный оператор if

```sh
if [conditon]
 then [commands]
 else [commands]
fi
```


*_condition*
```sh
var_1 = 10
var_2 = 20

if (($var_1<$var_1))
  then echo "<$2"
  else echo ">=$2"
fi
```

## Циклы

### for (fereach)

```sh
for [variable-name] in [list of variables]
  do
    [commands]
  done
```

*_for*
```sh
for i in 1 2 3
  do echo $i
done
```

### while

```sh
while [condition]
  do
   [commands]
  done
```

*_while*

```sh
n=0
while (($n<5))
  do
    echo $n;
    n=`expr $n + 1`;
  done
```

## Полезные ссылки

- [Топ 10 команд Bash для постоянной работы](https://medium.com/the-code-review/top-10-bash-file-system-commands-you-cant-live-without-4cd937bd7df1)
