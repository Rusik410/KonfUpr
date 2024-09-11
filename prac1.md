## Задача 1
Вывести отсортированный в алфавитном порядке список имен пользователей в файле passwd (вам понадобится grep).
```
grep '.*' /etc/passwd | cut -d: -f1 | sort
```
![image](https://github.com/user-attachments/assets/be000ae3-2c1b-4709-8943-bf0c972d717b)


## Задача 2
Вывести данные /etc/protocols в отформатированном и отсортированном порядке для 5 наибольших портов, как показано в примере ниже:
```
awk '{print $2, $1}' /etc/protocols | sort -nr | head -n 5
```
![image](https://github.com/user-attachments/assets/6806edfa-2e7a-41f9-b29a-1804f11c4410)


## Задача 3
Написать программу banner средствами bash для вывода текстов, как в следующем примере (размер баннера должен меняться!):
```
#!/bin/bash

text=$*
length=${#text}

for i in $(seq 1 $((length + 2))); do
    line+="-"
done

echo "+${line}+"
echo "| ${text} |"
echo "+${line}+"
```



























