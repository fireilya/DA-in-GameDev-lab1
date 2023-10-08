# АНАЛИЗ ДАННЫХ И ИСКУССТВЕННЫЙ ИНТЕЛЛЕКТ [in GameDev]
Отчет по лабораторной работе #2 выполнил(а):
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
научиться передавать в Unity данные из Google Sheets с помощью Python.

Ход работы:

## Задание 1
### Выберите одну из компьютерных игр, приведите скриншот её геймплея и краткое описание концепта игры. Выберите одну из игровых переменных в игре (ресурсы, внутри игровая валюта, здоровье персонажей и т.д.), опишите её роль в игре, условия изменения / появления и диапазон допустимых значений. Постройте схему экономической модели в игре и укажите место выбранного ресурса в ней.


Мой выбор пал на компьютерную игру "Cringe", скриншоты которой приведены ниже:

![Alt text](https://sun9-42.userapi.com/impg/rOYkIMtj-MBFUiSm2hUqR4Gkfe1mlwPllshRXg/Numx84JqrsE.jpg?size=1920x1080&quality=96&sign=c14d3592c304ad736c126bbd61e91205&type=album "Optional title")
![Alt text](https://sun9-38.userapi.com/impg/wIX9zGfU1ZuZqNYPK0Ns_xCDbsNdHzlDqmgaaw/ZaVpCHQWOqo.jpg?size=1920x1080&quality=96&sign=aac95546b135fa46a74da7f53b93a2ca&type=album "Optional title")

Описание концепта: Злой моргенштерн со своей бандой украл у BananaCat-а его любимый скейт-борд. Лучший друг BananaCat-а - HappyCat не собирается это так оставлять! Он берёт свой ховерборд бросает вызов банде моргенштерна!

В качестве рассматриваемого ресурса выбраны ракеты HappyCat-а. Максимум их может быть 10, минимум 0. Они необходимы для нанесения сокрушительного урона Моргенштерну и его соратникам в размере 50 единиц. В одном запуске участвует лишь одна ракета, время отката-1 секунда. Добывать ракеты можно убивая злых негров, которых время от времени выпускает Моргенштерн, или вызывая Титора в режиме "Поддержка припасами". В этом случае на игровом поле будет появляться силовая ячейка с изображением ракеты, которую надо будет поймать. Одной силовой ячейки достаточно, чтобы полностью восполнить запас ракет. 

Экономическая модель у всего этого следующая:
![Alt text](https://sun9-78.userapi.com/impg/jILG7yPNWXsOli6pH3Ix3zmBefj41i8KiHk4xg/8qGbU_ME3iQ.jpg?size=1920x1080&quality=96&sign=993624afb4a025c3fd08e4d4d95d8a19&type=album "Optional title")
## Задание 2
### С помощью скрипта на языке Python заполните google-таблицу данными, описывающими выбранную игровую переменную в выбранной игре (в качестве таких переменных может выступать игровая валюта, ресурсы, здоровье и т.д.). Средствами google-sheets визуализируйте данные в google-таблице (постройте график, диаграмму и пр.) для наглядного представления выбранной игровой величины.

Скрипт:

```py
import gspread
import numpy as np

gc = gspread.service_account(filename='godsaveme-bc35de239287.json')
sh = gc.open("HappyCat Rockets change sheet")
rockets_count = 7


def update_sheet(middle_string):
    sh.sheet1.update(('A' + str(i)), str(i))
    sh.sheet1.update(('B' + str(i)), middle_string)
    sh.sheet1.update(('C' + str(i)), str(rockets_count))


for i in range(1, 21):
    luck = np.random.sample()
    if luck > 0.9:
        rockets_count = 10
        update_sheet("Восполнение запаса")
    elif rockets_count == 0:
        update_sheet("Пропуск хода")
    else:
        rockets_count -= 1
        update_sheet("Запуск ракеты")

```

Визуализация всех данных представлена в гугл-таблице: https://docs.google.com/spreadsheets/d/11nPsYmSJy1SwUGCkDI_8D7iLP0Iy9EqNxR5Y_XbmW58/edit#gid=0

## Задание 3
### Настройте на сцене Unity воспроизведение звуковых файлов, описывающих динамику изменения выбранной переменной. Например, если выбрано здоровье главного персонажа вы можете выводить сообщения, связанные с его состоянием.

Введём условие, что если ракет 7 или больше, то всё хорошо, если меньше 3-ёх, то всё плохо, иначе средне, тогда мы метод Update изменим следущим образом:
```cs
    void Update()
    {
        if (dataSet["Mon_" + i.ToString()] >= 7 & statusStart == false & i != dataSet.Count)
        {
            StartCoroutine(PlaySelectAudioGood());
            Debug.Log(dataSet["Mon_" + i.ToString()]);
        }

        if (dataSet["Mon_" + i.ToString()] < 7 & dataSet["Mon_" + i.ToString()] > 2 & statusStart == false & i != dataSet.Count)
        {
            StartCoroutine(PlaySelectAudioNormal());
            Debug.Log(dataSet["Mon_" + i.ToString()]);
        }

        if (dataSet["Mon_" + i.ToString()] <= 2 & statusStart == false & i != dataSet.Count)
        {
            StartCoroutine(PlaySelectAudioBad());
            Debug.Log(dataSet["Mon_" + i.ToString()]);
        }
    }
```

## Выводы

В ходе лабораторной работы я смог получить API ключ гугл-таблиц, заполнил их с помощью Python, после чего создал интерактивное взаимодействие с таблицей в Unity

Цели лабораторной работы были достигнуты.
## Powered by

**BigDigital Team: Denisov | Fadeev | Panov**
