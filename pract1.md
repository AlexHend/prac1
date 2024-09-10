
## Задача 1

Вывести отсортированный в алфавитном порядке список имен пользователей в файле passwd (вам понадобится grep).

Решение:
```bash
grep -o '^[^:]*' /etc/passwd | sort
```
![Image alt](https://github.com/AlexHend/prac1/blob/main/zadan1.png)


## Задача 2

Вывести данные /etc/protocols в отформатированном и отсортированном порядке для 5 наибольших портов, как показано в примере ниже:

```
[root@localhost etc]# cat /etc/protocols ...
142 rohc
141 wesp
140 shim6
139 hip
138 manet
```

Решение:
```bash
cat /etc/protocols | awk '{print $2, $1}' | sort -nr | head -n 5
```
![image](https://github.com/AlexHend/prac1/blob/main/zadan2.png)

## Задача 3

Написать программу banner средствами bash для вывода текстов, как в следующем примере (размер баннера должен меняться!):

```
[root@localhost ~]# ./banner "Hello from RTU MIREA!"
+-----------------------+
| Hello from RTU MIREA! |
+-----------------------+
```

Перед отправкой решения проверьте его в ShellCheck на предупреждения.

Решение:
```bash
#!/bin/bash
text=$1
size=${#text}
echo -n "+"
for ((i = -2; i < size; i++))
do
echo -n "-"
done
echo "+"
echo "| $text |"
echo -n "+"
for ((i = -2; i < size; i++))
do
echo -n "-"
done
echo "+"
```
![image](https://github.com/AlexHend/prac1/blob/main/zadan3.png)


## Задача 4

Написать программу для вывода всех идентификаторов (по правилам C/C++ или Java) в файле (без повторений).

Пример для hello.c:

```
h hello include int main n printf return stdio void world
```

Решение:
```bash
grep -o '\b[_A-Za-z][_A-Za-z0-9]*\b' hello.cpp | sort | uniq
```
![image](https://github.com/AlexHend/prac1/blob/main/zadan4.png)


## Задача 6

Написать программу для проверки наличия комментария в первой строке файлов с расширением c, js и py.

Решение:
```bash
for file in "$@"; do
  if [[ "$file" =~ \.(c|js|py)$ ]]; then
    first_line=$(head -n 1 "$file")
    if [[ "$first_line" =~ ^\/[*\/]{1}|#|\'{3} ]]; then
  echo "$file has a comment in the first line."
    else
      echo "$file doesn't have a comment in the first line."
    fi
  fi
done
```
![image](https://github.com/AlexHend/prac1/blob/main/zadan6.png)
