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
Научиться интегрировать экономическую систему в проект Unity и обучать ML-Agent.

## Задание 1
### Измените параметры файла. yaml-агента и определить какие параметры и как влияют на обучение модели.

1) Открыл проект и подключил библиотеки мл агента.
![image](https://user-images.githubusercontent.com/100460661/204876835-50c9766b-9229-4b51-9b2e-9ab4f8e26e68.png)

2) Добавил Economic.yaml в папку с проектом. Содержимое файла Economic.yaml:

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
3) Активировал виртуальное пространство и запустил обучение.

![image](https://user-images.githubusercontent.com/100460661/204885863-0ae2ea78-fcf6-4d05-8a17-88203491c584.png)

4) По завершении обучения файлы сохранились.

![image](https://user-images.githubusercontent.com/100460661/204887208-84cc500f-c7b6-4031-855b-2f4fe065bed6.png)

5) Установил TensorBoard. Появились следующие графики:

![image](https://user-images.githubusercontent.com/100460661/204898423-7c906192-58d7-4afa-8c8a-bf4d005f6ced.png)

Далее буду изменять 5 раз какие-либо параметры файла Economic.yaml. Задача - добиться максимальной монотонности и линейности графика Cumulative Reward.

6) Изменил batch_size с 1024 на 2100. Прогнал все пункты заново.

![image](https://user-images.githubusercontent.com/100460661/204902981-ed6800f5-8e39-4c7d-8904-49d503508ea4.png)

График стал всегда равен 1.

7) Изменил batch_size с 1024 на 300. Прогнал все пункты заново.

![image](https://user-images.githubusercontent.com/100460661/204906752-666444b0-c8c9-4fe1-82b0-0fdc9dbef739.png)

График стал более кривым.

8) Вернул  batch_size 1024, изменил lambd с 0.95 на 0.9

![image](https://user-images.githubusercontent.com/100460661/204908823-3dc96edc-ef01-4e25-9510-2ad3272d8cf2.png)

график стал более линеен.

9) Оставил lambd 0.9 и изменил epsilon с 0.2 на 0.1

![image](https://user-images.githubusercontent.com/100460661/204910295-b7822e91-12c7-4527-b0d4-1f1cbd3fcb0c.png)

Практически нет изменений.

10) Изменил num_epoch с 3 на 1

![image](https://user-images.githubusercontent.com/100460661/204911579-0b373ba2-c0b5-46d4-99e7-7df73578100e.png)

Практически нет изменений.


## Задание 2
### Опишите результаты, выведенные в TensorBoard.

#### Environment
- Cumulative Reward - среднее общее вознаграждение за эпизод для всех агентов. Увеличивается, когда эпизод обучения успешен. График должен постоянно увеличиваться, но может вести себя скачкообразно.

- Episode Length - средняя продолжительность эпизода обучения в среде для агентов.

#### Losses
- Policy Loss - средняя величина функции потери политики, где политика - процесс принятия решений. График должен идти вниз во время успешного эпизода.

- Value Loss - средняя потеря функции значения. Она моделирует, насколько хорошо агент прогнозирует значение своего следующего состояния. Должна увеличиваться, пока агент обучается, а затем уменьшаться, когда вознаграждение стабилизируется.

#### Policy

- Entropy - график случайности решений модели. Должен уменьшаться во время успешного эпизода. 
- Beta - гиперпараметр для настройки Entropy.
- Epsilon - гиперпараметр, влияет на скорость развития политики.
- Extrinsic Reward - соответствует среднему совокупному вознаграждению, полученному от окружающей среды за эпизод.
- Value Estimate - это среднее значение, посещённое всеми состояниями агента. Чтобы отражать увеличение знаний агента, это значение должно расти, а затем стабилизироваться.
- Learning Rate - показывает величину шага при поиске оптимальной политики. Должен уменьшаться линейно.

#### Self play
- ELO - показывает силу сети.

## Выводы
В этой лабораторной я научился интегрировать экономическую систему в проект Unity, используя мл агента. Научился выводить графики в TensorBoard и анализировать их.

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
