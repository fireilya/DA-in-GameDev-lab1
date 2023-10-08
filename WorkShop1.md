# АНАЛИЗ ДАННЫХ И ИСКУССТВЕННЫЙ ИНТЕЛЛЕКТ [in GameDev]
Отчет по лабораторной работе #1 выполнил(а):
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
становить необходимое программное обеспечение, которое пригодится для создания интеллектуальных моделей на Python. Рассмотреть процесс установки игрового движка Unity для разработки игр.

Ход работы:

## Задание 1
### Написать программу Hello World на Python с запуском в Jupiter Notebook.

-Запустить JupiterNotebook
-Создать файл формата ipynb
-Использоать встроенную функцию консольного вывода "рrint" для вывода сообщения.

```py
print("Hello World!!!")
```

## Задание 2
### Написать программу Hello World на C# с запуском на Unity.


```cs
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class Hello_World : MonoBehaviour
{
    int count;
    void Start()
    {
        
    }

    // Update is called once per frame
    void Update()
    {
        if(Input.anyKeyDown)
        {
            count++;
            switch (count)
            {
                case 1:
                    Debug.Log("Hello World!!!");
                    break;
                case 2:
                    Debug.Log("Hello World!!!!!!!!!");
                    break;
                case 3:
                    Debug.Log("I already Said: \"Hello World\"");
                    break;
                case 4:
                    Debug.Log("Leave me alone");
                    break;
                case 5:
                    Debug.Log("Stop it!");
                    break;
                case 6:
                    Debug.Log("Don't touch the keyboard!");
                    break;
                case 7:
                    Debug.Log("I seek of you");
                    count = 3;
                    break;
            }
        }
    }
}
```

## Задание 3
### Оформить отчет в виде документации на github (markdown-разметка)
Результат этого задания вы только что прочитали

## Выводы

В ходе проделанной работы были изучены такие инструменты, как: Anakonda, JupiterLab, Unity, Python, C#
В ходе лабораторной:

1) Я научился работать с Anakonda
2) Я смог запустить Hello World в JupiterNotebook
3) Я создал скрипт, который заставляет любой объект в Unity, с учётом прикрепления к нему скрипт-файла, писать в консоль "Hello World" по нажатию клавиши
4) Я разобрался как клонировать репозитории на Git.

Цели лабораторной работы были достигнуты.
## Powered by

**BigDigital Team: Denisov | Fadeev | Panov**
