# DA-in-GameDev-lab5
# АНАЛИЗ ДАННЫХ И ИСКУССТВЕННЫЙ ИНТЕЛЛЕКТ [in GameDev]
Интеграция экономической системы в проект Unity и обучение ML-Agent.

Отчет по лабораторной работе #5 выполнил(а):
- Китушкин Данил Яковлевич
- РИ-210910
Отметка о выполнении заданий (заполняется студентом):

| Задание | Выполнение | Баллы |
| ------ | ------ | ------ |
| Задание 1 | * | 80 |
| Задание 2 | * | 20 |

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

Научиться внедрять экономическую систему в проект на Unity и обучать ML-Agent.

## Задание 1
### Измените параметры файла. yaml-агента и определить какие параметры и как влияют на обучение модели.

1) Открыл проект и подключил библиотеки мл агента.
![2](https://user-images.githubusercontent.com/95544542/205360591-fcf79de5-a0ca-49c3-ba4a-ffba255b1af4.PNG)

После запуска проекта, Anaconda выдала ссылку на графики, вот так они выглядят при открытии.

![1](https://user-images.githubusercontent.com/95544542/205364382-7b056ae0-e396-4a9e-89b9-f33de61531e3.PNG)



2) Добавил Economic.yaml в папку с проектом, а так же подключил и установил пакеты. Содержимое данного файло оставлю ниже + Скриншоты:

```yaml
behaviors:
  Economic:
    trainer_type: ppo
    hyperparameters:
      batch_size: 1024
      buffer_size: 10240
      learning_rate: 3.0e-4
      learning_rate_schedule: linear
      beta: 1.0e-2
      epsilon: 0.2
      lambd: 0.95
      num_epoch: 3      
    network_settings:
      normalize: false
      hidden_units: 128
      num_layers: 2
    reward_signals:
      extrinsic:
        gamma: 0.99
        strength: 1.0
    checkpoint_interval: 500000
    max_steps: 750000
    time_horizon: 64
    summary_freq: 5000
    self_play:
      save_steps: 20000
      team_change: 100000
      swap_steps: 10000
      play_against_latest_model_ratio: 0.5
      window: 10
```
![1](https://user-images.githubusercontent.com/95544542/205360721-aee6145a-d4a8-4deb-97b4-8502e918fe07.PNG)


Поменяем некоторые значения в файле Economic и посмотрим как будут меняться графики.

- Поменяем значение num_epoch и вместо 3 поставим 8

![4](https://user-images.githubusercontent.com/95544542/205363674-e9adc596-1a41-4aa3-ace9-ab4655fc1901.png)

 значение num_epoch показывает количество проходов через буфер опыта

- Поменяем значение batch_size с 1024 на 784

![3](https://user-images.githubusercontent.com/95544542/205363898-f0d18da5-499f-4ae0-ac50-6681b6e70400.png)

Значение batch_size отвечает за количество опытов в каждой итерации градиентного спуска.

- Поменяем значение epsilon с 0.2 на 0.3.

![2](https://user-images.githubusercontent.com/95544542/205364133-cca44614-e00d-444e-97cd-1ed4512d06c7.PNG)

Значение epsilon используется для расчёта скорости развития политики в процессе обучения.

## Задание 2
### Опишите результаты, выведенные в TensorBoard.

#### Environment
- Episode Length - Средняя продолжинтельность обучения агентов.
- Cumulative Reward - Общее среднее вознаграждение для всех агентов в сцене.

#### Losses

- Value Loss - Средняя потеря функции значения. 
- Policy Loss - Средняя потеря политики.

#### Policy

- Entropy - График случайности решений модели.
- Beta - Отвечает за настройку Entropy.
- Epsilon - оОтвечает за скорость развития политики.
- Extrinsic Reward - Среднее вознаграждение, полученное в среде.
- Value Estimate - Среднее значение, посещённое всеми состояниями агента.
- Learning Rate - Отвечает за величину шага при поиске оптимальной политики. 

#### Self play
- ELO - Отвечает за силу сети.

## Выводы
В этой лабораторной я научился интегрировать экономическую систему в проект Unity, обучать ML Agent. Так же научился выводить графики в Tensor Board.

| Plugin | README |
| ------ | ------ |
| Dropbox | [plugins/dropbox/README.md][PlDb] |
| GitHub | [plugins/github/README.md][PlGh] |
| Google Drive | [plugins/googledrive/README.md][PlGd] |
| OneDrive | [plugins/onedrive/README.md][PlOd] |
| Medium | [plugins/medium/README.md][PlMe] |
| Google Analytics | [plugins/googleanalytics/README.md][PlGa] |

## Powered by

**BigDigital Team: Denisov | Fadeev | Panov**
