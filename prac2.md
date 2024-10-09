## Задача 1

Вывести служебную информацию о пакете matplotlib (Python). Разобрать основные элементы содержимого файла со служебной информацией из пакета. Как получить пакет без менеджера пакетов, прямо из репозитория?
```
pip show matplotlib
```
![image](https://github.com/user-attachments/assets/7348bb9e-3be8-4e86-b3d9-0993bd6a7fbf)
Основные элементы содержимого файла со служебной информацией из пакета:

Name: Название пакета.

Version: Текущая версия пакета.

Summary: Краткое описание пакета.

Home-page: Ссылка на домашнюю страницу пакета.

Author: Авторы пакета.

Author-email: Электронная почта авторов.

License: Лицензия пакета.

Location: Расположение установленного пакета.

Requires: Список зависимых пакетов, необходимых для работы.

Required-by: Список пакетов, которые зависят от matplotlib.

Чтобы получить пакет без менеджера пакетов, прямо из репозитория нужно перейти по ссылке: https://matplotlib.org



## Задача 2

Вывести служебную информацию о пакете express (JavaScript). Разобрать основные элементы содержимого файла со служебной информацией из пакета. Как получить пакет без менеджера пакетов, прямо из репозитория?

__Решение:__  
`npm show express` - выводит служебную информацию о пакете express  
Вывод:  
![image](https://github.com/user-attachments/assets/37608517-da4f-451d-9256-b308705ad5e4)

Основные элементы служебной информации пакета express:

- Name (Имя): Название пакета
- Version (Версия): Текущая версия пакета 
- Fast, unopinionated, minimalist web framework (Быстрый, минималистичный веб-фреймворк без строгих правил)
- Homepage (Домашняя страница)
- Dependencies (Зависимости): Пакеты, от которых зависит express
- Maintainers (Сопроваждающие)
- Dist-tags (Теги дистрибутива)
- Published: Кем и когда опубликован


Чтобы получить пакет express без использования менеджера пакетов, можно скачать его исходный код непосредственно из официального репозитория GitHub.

## Задача 3

Сформировать graphviz-код и получить изображения зависимостей matplotlib и express.

matplotlib:

![image](https://github.com/user-attachments/assets/ca4543a6-f51e-4d80-b4d0-50b678989f44)


express:

![image](https://github.com/user-attachments/assets/148e2c58-7234-4b73-8d4a-357fc9298659)


## Задача 4

**Следующие задачи можно решать с помощью инструментов на выбор:**

* Решатель задачи удовлетворения ограничениям (MiniZinc).
* SAT-решатель (MiniSAT).
* SMT-решатель (Z3).

Изучить основы программирования в ограничениях. Установить MiniZinc, разобраться с основами его синтаксиса и работы в IDE.

Решить на MiniZinc задачу о счастливых билетах. Добавить ограничение на то, что все цифры билета должны быть различными (подсказка: используйте all_different). Найти минимальное решение для суммы 3 цифр.

```
include "globals.mzn";

array[1..6] of var 0..9: digits;
constraint all_different(digits);

var int: sum_first = sum(digits[1..3]);
var int: sum_last = sum(digits[4..6]);

constraint sum_first = sum_last;
solve minimize sum_first;
```
Вывод:
![image](https://github.com/user-attachments/assets/17ea6208-b2ce-4adb-b88f-81ffcf4d536d)

## Задача 5

Решить на MiniZinc задачу о зависимостях пакетов для рисунка, приведенного ниже.

![image](https://github.com/user-attachments/assets/e6fc79e2-76e0-4dae-b1a5-056360eb272c)

Решение:
```MiniZinc
set of int: MenuVersion = {100, 110, 120, 130, 150};
set of int: DropdownVersion = {230, 220, 210, 200, 180};
set of int: IconsVersion = {100, 200};

var MenuVersion: menu;
var DropdownVersion: dropdown;
var IconsVersion: icons;

constraint if menu >= 110 then dropdown >= 200 else dropdown = 180 endif;

constraint if dropdown <= 200 /\ dropdown > 180 then icons = 200 else icons = 100 endif;

solve satisfy;
```
Результат:

![image](https://github.com/user-attachments/assets/f02d4149-0c95-49bc-a471-f53ab820e63d)


## Задача 6
Решить на MiniZinc задачу о зависимостях пакетов для следующих данных:

```
root 1.0.0 зависит от foo ^1.0.0 и target ^2.0.0.
foo 1.1.0 зависит от left ^1.0.0 и right ^1.0.0.
foo 1.0.0 не имеет зависимостей.
left 1.0.0 зависит от shared >=1.0.0.
right 1.0.0 зависит от shared <2.0.0.
shared 2.0.0 не имеет зависимостей.
shared 1.0.0 зависит от target ^1.0.0.
target 2.0.0 и 1.0.0 не имеют зависимостей.
```

Решение: 
```
% Определение пакетов и их версий
enum Version = {v1_0_0, v1_1_0, v2_0_0};

% Пакеты
enum Package = {root, foo, left, right, shared, target};

% Массив для хранения версий каждого пакета
array[Package] of var Version: versions;

% Зависимости
% Зависимость вида: пакет A зависит от пакета B версии C
% Функция valid_dependency(p, v) проверяет, что версия v пакета p находится в указанном диапазоне

% root 1.0.0 зависит от foo ^1.0.0 и target ^2.0.0
constraint versions[root] = v1_0_0;
constraint (versions[foo] = v1_0_0 \/ versions[foo] = v1_1_0);
constraint versions[target] = v2_0_0;

% foo 1.1.0 зависит от left ^1.0.0 и right ^1.0.0
constraint versions[foo] = v1_1_0 -> (versions[left] = v1_0_0 /\ versions[right] = v1_0_0);

% foo 1.0.0 не имеет зависимостей
% Это автоматически выполняется, так как нет дополнительных ограничений для foo 1.0.0

% left 1.0.0 зависит от shared >=1.0.0
constraint versions[left] = v1_0_0 -> (versions[shared] = v1_0_0 \/ versions[shared] = v2_0_0);

% right 1.0.0 зависит от shared <2.0.0
constraint versions[right] = v1_0_0 -> (versions[shared] = v1_0_0);

% shared 2.0.0 не имеет зависимостей
% shared 1.0.0 зависит от target ^1.0.0
constraint versions[shared] = v1_0_0 -> (versions[target] = v1_0_0);

% target 2.0.0 и 1.0.0 не имеют зависимостей
% Эти ограничения включены в выбор версий

solve satisfy;

% Вывод результата
output ["Versions:\n"] ++
  [ show(versions[p]) ++ " " ++ show(p) ++ "\n" | p in Package];
```
Вывод:
![image](https://github.com/user-attachments/assets/cbce3ca2-777f-4b0b-b2c9-6b79e5d911b3)

## Задача 7

Представить задачу о зависимостях пакетов в общей форме. Здесь необходимо действовать аналогично реальному менеджеру пакетов. То есть получить описание пакета, а также его зависимости в виде структуры данных. Например, в виде словаря. В предыдущих задачах зависимости были явно заданы в системе ограничений. Теперь же систему ограничений надо построить автоматически, по метаданным.

Решение:

```
# Описание пакетов и их зависимостей
packages = {
    "root": {
        "version": "1.0.0",
        "dependencies": {
            "foo": "^1.0.0",
            "target": "^2.0.0"
        }
    },
    "foo": {
        "version": "1.1.0",
        "dependencies": {
            "left": "^1.0.0",
            "right": "^1.0.0"
        }
    },
    "left": {
        "version": "1.0.0",
        "dependencies": {
            "shared": ">=1.0.0"
        }
    },
    "right": {
        "version": "1.0.0",
        "dependencies": {
            "shared": "<2.0.0"
        }
    },
    "shared": {
        "version": "2.0.0",
        "dependencies": {}
    },
    "target": {
        "version": "2.0.0",
        "dependencies": {}
    }
}

# Функция для получения зависимостей пакета
def get_dependencies(package_name):
    if package_name in packages:
        return packages[package_name]["dependencies"]
    else:
        return None

# Пример использования
package_name = "foo"
dependencies = get_dependencies(package_name)
if dependencies:
    print(f"Зависимости пакета {package_name}:")
    for dep, version in dependencies.items():
        print(f"  - {dep}: {version}")
else:
    print(f"Пакет {package_name} не найден.")
constraints = []

def add_constraints(package_name):
    if package_name not in packages:
        return

    dependencies = packages[package_name]["dependencies"]
    for dep, version in dependencies.items():
        # Создаем ограничения на основе зависимостей
        constraints.append(f"{package_name} -> {dep} {version}")
        add_constraints(dep)  # Рекурсивно добавляем зависимости

# Добавление ограничений для корневого пакета
add_constraints("root")

# Печать сгенерированных ограничений
print("Сгенерированные ограничения:")
for constraint in constraints:
    print(constraint)
```

Вывод:
![image](https://github.com/user-attachments/assets/fe69d553-915c-4bda-a3d5-3b6123493ca5)
