# АНАЛИЗ ДАННЫХ И ИСКУССТВЕННЫЙ ИНТЕЛЛЕКТ [in GameDev]
Отчет по лабораторной работе #3 выполнил(а):
- Перминов Илья Андреевич
- РИ220913
Отметка о выполнении заданий (заполняется студентом):

| Задание | Выполнение | Баллы |
| ------ | ------ | ------ |
| Задание 1 | * | 60 |
| Задание 2 | * | 20 |
| Задание 3 | * | 20 |

знак "*" - задание выполнено; знак "#" - задание не выполнено;

Работу проверили:
- к.т.н., доцент Денисов Д.В.
- к.э.н., доцент Панов М.А.
- ст. преп., Фадеев В.О.

[![N|Solid](https://cldup.com/dTxpPi9lDf.thumb.png)](https://nodesource.com/products/nsolid)

[![Build Status](https://travis-ci.org/joemccann/dillinger.svg?branch=master)](https://travis-ci.org/joemccann/dillinger)

Структура отчета

- Данные о работе: название работы, фио, группа, выполненные задания.
- Цель работы.
- Задание 1.
- Код реализации выполнения задания. Визуализация результатов выполнения (если применимо).
- Задание 2.
- Код реализации выполнения задания. Визуализация результатов выполнения (если применимо).
- Задание 3.
- Код реализации выполнения задания. Визуализация результатов выполнения (если применимо).
- Выводы.
- ✨Magic ✨

## Цель работы
разработать оптимальный баланс для десяти уровней игры Dragon Picker

Ход работы:

## Задание 1
### Предложите вариант изменения найденных переменных для 10 уровней в игре. Визуализируйте изменение уровня сложности в таблице.


В качестве переменных, влияющих на баланс были обнаружены следующие:

speed - скорость дракона
timeBetweenEggDrops - время между сбросом яиц
leftRightDistance - ширина рамок поля, внутри которых может перемещаться дракон
chanceDirection - шанс изменения направления дракона

Так как по моему мнению успех в игре зависит от реакции и координации игрока, то я решил увеличивать сложность с каждым уровнем по экспоненциальному закону. Были определены оптимальные начальные значения, которые используются в первом уровне, а также их коэффициента приращения. Если переменная с каждым уровнем должна увеличиваться, то коэффициент больше единицы, иначе меньше. Чтобы построить график увеличения сложности я ввёл такое пониятие, как коэффициент сложности уровня. Его график должен расти экспоненциально.
Коэффициент сложности = speed * leftRightDistance * chanceDirection / timeBetweenEggDrops
Данная формула была выведена из следующих соображений:

1. Чем быстрее движется дракон-тем сложнее за ним уследить
2. Чем больше рамка, тем больше у дракона пространства для манёвра, что усложняет процесс
3. Чем выше шанс смены направления движения, тем сложнее предугадать направление движения дракона, вследствие чего полагаться игрок может лишь на свою реакцию
4. Чем меньше времени между сбросом яиц, тем более активно ими бомбордируется игрок и тем больше шанс ошибиться и уронить яйцо

Визуализация коэффициента сложности, а также данные для всех 10 уровней представлены в следующей таблице: https://docs.google.com/spreadsheets/d/1RdGfE57yo6dJecfAcnjuPod165MIXz8KwoCt0WY3yBk/edit#gid=0


## Задание 2
### Создайте 10 сцен на Unity с изменяющимся уровнем сложности.

Подробнее с результатом выполнения этого задания вы можете ознакомиться здесь: https://github.com/fireilya/Dragon-Picker-Prototype-With-Difficulties

## Задание 3
### Решение в 80+ баллов должно заполнять google-таблицу данными из Python. В Python данные также должны быть визуализированы.

модель заполнения мы возьмём из WorkShop2, в качестве визуализации мы будем использовать график, который будем строить и выводить с помощью модуля "matplotlib"
Скрипт получается следующий:
```py
    import enum
import time

import gspread
import matplotlib.pyplot as plt
import numpy as np


class DifficultIndex(enum.Enum):
    speed = 0
    egg_drop_time = 1
    right_left_distance = 2
    change_direction_chance = 3


class DifficultData:
    values = [2, 2, 1, 0.01]
    increase_coef = [1.3, 0.79, 1.78, 1.19]
    column_names = ("B", "C", "D", "E")
    fields_count = 4
    difficulty_coef = []

    def __init__(self):
        self.append_difficult_coef()

    def append_difficult_coef(self):
        self.difficulty_coef.append(
            self.values[DifficultIndex.speed.value] * self.values[DifficultIndex.right_left_distance.value] /
            self.values[
                DifficultIndex.egg_drop_time.value] * self.values[DifficultIndex.change_direction_chance.value])

    def icrease_difficulty(self):
        for i in range(self.fields_count):
            self.values[i] *= self.increase_coef[i]
        if self.values[DifficultIndex.right_left_distance.value] > 10:
            self.values[DifficultIndex.right_left_distance.value] = 10
        self.append_difficult_coef()


gc = gspread.service_account(filename='godsaveme-bc35de239287.json')
sh = gc.open("Difficult Changing")

sh.sheet1.update(('A1'), "Level number")
sh.sheet1.update(('B1'), "Dragon speed")
sh.sheet1.update(('C1'), "Egg drop time")
sh.sheet1.update(('D1'), "Right-left distance")
sh.sheet1.update(('E1'), "change_direction_chance")

difficulty_data = DifficultData()


def update_sheet(row):
    for i in range(difficulty_data.fields_count):
        sh.sheet1.update(("A" + str(row)), row - 1)
        sh.sheet1.update((difficulty_data.column_names[i] + str(row)), difficulty_data.values[i])


for i in range(1, 11):
    time.sleep(5)
    if i != 1: difficulty_data.icrease_difficulty()
    update_sheet(i + 1)
fig, ax = plt.subplots()
x = np.arange(1, 11)
y = np.array(difficulty_data.difficulty_coef)
ax.plot(x, y)
ax.grid()
plt.xticks(range(1, 11, 1), range(1, 11, 1))
plt.yticks(range(1, 50, 2), range(1, 50, 2))
plt.xlabel("Level number")
plt.ylabel("Difficulty")
plt.show()

```

## Выводы

В ходе лабораторной работы был разобран и доработан прототип игры Dragon Picker, а именно был создан дизайн-документ с помощью Python, была проведена визуализация динамики изменения данных средствами Python и Google Sheets, а также, в соответствии с дизайн-документом была добавлена система сожностей, которая представляет собой набор из 10 сцен, чем больше номер сцены, тем выше уровень сложности.

Цели лабораторной работы были достигнуты.
## Powered by

**BigDigital Team: Denisov | Fadeev | Panov**
