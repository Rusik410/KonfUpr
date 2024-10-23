## Задача 1
Реализовать на Jsonnet приведенный ниже пример в формате JSON. Использовать в реализации свойство программируемости и принцип DRY.<br>
```
local groups = [
  "ИКБО-1-24",
  "ИКБО-2-24",
  "ИКБО-3-24",
  "ИКБО-4-24",
  "ИКБО-5-24",
  "ИКБО-6-24",
  "ИКБО-7-24",
  "ИКБО-8-24",
  "ИКБО-9-24",
  "ИКБО-10-24",
  "ИКБО-11-24",
  "ИКБО-12-24",
  "ИКБО-13-24",
  "ИКБО-14-24",
  "ИКБО-15-24",
  "ИКБО-16-24",
  "ИКБО-17-24",
  "ИКБО-18-24",
  "ИКБО-19-24",
  "ИКБО-20-24",
  "ИКБО-21-24",
  "ИКБО-22-24",
  "ИКБО-23-24",
  "ИКБО-24-24"
];

local student(name, age, group, subject) = {
  name: name,
  age: age,
  group: group,
  subject: subject,
};

local students = [
  student("Иванов И.И.", 19, "ИКБО-4-24", "Конфигурационное управление"),
  student("Петров П.П.", 18, "ИКБО-5-24", "Конфигурационное управление"),
  student("Сидоров С.С.", 18, "ИКБО-5-24", "Конфигурационное управление"),
  student("Решетов К.С.", 19, "ИКБО-52-23", "Конфигурационное управление")
];

{
  groups: groups,
  students: students,
}
```
Установим Jsonnet на свой компьютер с помощью терминала:<br>
```
brew install jsonnet
```
Далее создадим файл prkt3.jsonnet, в который добавим приведенный в дано код, и скомпилируем файл в JSON, выполнив:<br>
```
jsonnet prktr3.jsonnet -o prktr3_1zd.json
```
Просмотреть содержимое файла JSON можно с помощью команды cat:<br>
```
cat prktr3_1zd.json
```
Результат:<br>

![Без имени-1](https://github.com/user-attachments/assets/59b9177f-ee9b-4a4d-9c4f-57c7caf8f58b)




# Задача 2
Реализовать на Dhall приведенный выше пример в формате JSON. Использовать в реализации свойство программируемости и принцип Dry<br>

Установим Dhall нас свой компьютер с помощью терминала:<br>
```
brew install dhall-json
```
Далее создадим файл prktr3.dhall, в который добавим код пример, и скомпилируем файл в JSON, выполнив:<br>
```
dhall-to-json --file prktr3.dhall > Pr3_2zd.json
```
Просмотреть содержимое файла JSON можно с помощью команды cat:<br>
```
cat prktr3_2zd.json
```
Результат:<br>

![Без имени-1](https://github.com/user-attachments/assets/2eba4df9-4f4a-4a23-b612-d4a51a765664)



# _____________________________________________________________
Для решения дальнейших задач потребуется программа на Питоне, представленная ниже. Разбираться в самом языке Питон при этом необязательно.

```Python
import random


def parse_bnf(text):
    '''
    Преобразовать текстовую запись БНФ в словарь.
    '''
    grammar = {}
    rules = [line.split('=') for line in text.strip().split('\n')]
    for name, body in rules:
        grammar[name.strip()] = [alt.split() for alt in body.split('|')]
    return grammar


def generate_phrase(grammar, start):
    '''
    Сгенерировать случайную фразу.
    '''
    if start in grammar:
        seq = random.choice(grammar[start])
        return ''.join([generate_phrase(grammar, name) for name in seq])
    return str(start)


BNF = '''
E = a
'''

for i in range(10):
    print(generate_phrase(parse_bnf(BNF), 'E'))

```

Реализовать грамматики, описывающие следующие языки (для каждого решения привести БНФ). Код решения должен содержаться в переменной BNF:
# _____________________________________________________________


## Задача 3
Язык нулей и единиц

### Решение
```python
BNF = '''
E = 0 | 1 E | 1
'''
```

![image](https://github.com/user-attachments/assets/09740216-00f4-40b4-81c2-d3f7a95ec5ab)



## Задача 4
Язык правильно расставленных скобок двух видов

### Решение
```python
BNF = '''
E = () | {} | ( E ) | { E } | E E
'''
```
![image](https://github.com/user-attachments/assets/cee638a5-e120-4bd5-8ffc-4cf9f8071c5a)



## Задача 5
Язык выражений алгебры логики

### Решение
```python
BNF = '''
E = ( E B F ) | U ( E ) | F
F = P B P | U P | P
P = x | y | (x) | (y)
U = ~
B = & | V
'''
```
![Без имени-1](https://github.com/user-attachments/assets/ee3242d3-47c1-45e7-b0f5-960a59a9396f)
