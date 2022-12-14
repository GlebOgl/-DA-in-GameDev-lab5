# АНАЛИЗ ДАННЫХ И ИСКУССТВЕННЫЙ ИНТЕЛЛЕКТ [in GameDev]
Отчет по лабораторной работе #5 выполнил(а):
- Оглоблин Глеб Александрович
- РИ210941
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

## Цель работы
-Интеграция экономической системы в проект Unity и обучение ML-Agen

## Задание 1
### Измените параметры файла. yaml-агента и определить какие параметры и как влияют на обучение модели.
- Открыл проект Unity и добавил в него ML-Agent, запустил, шар двигвется от одного куба к другому
- ![image](https://user-images.githubusercontent.com/79518116/205056534-3e8f02c1-9e22-4976-99bf-0ef5cda3d67d.png)
- Подготавливаю к работе ML Agent
- ![image](https://user-images.githubusercontent.com/79518116/205057347-50fddd35-ba21-4d5c-b880-3adfdbe4f4f9.png)
- ![image](https://user-images.githubusercontent.com/79518116/205057912-18250b13-b386-4188-b1c9-a3b669a01d38.png)
- ![image](https://user-images.githubusercontent.com/79518116/205059757-90bf559d-b88f-4cd2-b78a-3e085125d551.png)
- Запускаю проект
- ![image](https://user-images.githubusercontent.com/79518116/205059983-2d5c500b-0f96-4322-b59a-b06c199afac4.png)
- 12 префабов TargetAreaEconomic
- ![image](https://user-images.githubusercontent.com/79518116/205060332-e48eb80d-e784-4720-a2b9-7df78c8bc75d.png)
- процесс обучения модели
- ![image](https://user-images.githubusercontent.com/79518116/205060455-336ea969-4c3e-4e6f-a897-7472e5822660.png)
- Результаты 
- ![image](https://user-images.githubusercontent.com/79518116/205061165-b57c575f-ed29-4676-8bd9-f36807818cf9.png)
- TensorBoard графики
- ![image](https://user-images.githubusercontent.com/79518116/205084576-15578abc-d563-47cb-a815-cb79bf3d69bd.png)
- Изменение параметров economic.yaml, изменил batch_size до 512(количество опытов на каждой итерации)
- ![image](https://user-images.githubusercontent.com/79518116/205090448-c394aed4-7f37-47ab-a580-27fa5fbc13fa.png)
- изменил beta до 2.0e-2 (регулирует энтропию)
- ![image](https://user-images.githubusercontent.com/79518116/205117077-9a638923-f7ab-45b1-9d6d-54da6f0b500c.png)
- рост общей награды и снижение потери значения
- изменил num_epoch до 6
- ![image](https://user-images.githubusercontent.com/79518116/205119981-23759058-060a-4816-a98c-04709bcf22b7.png)
- скачкообразное снижение общей награды и потери значения
- изменил epsilon до 0.5(влияет на быстроту развития поведения)
- ![image](https://user-images.githubusercontent.com/79518116/205123820-4ed9bfc9-1393-43a1-b44f-eb7436d7753d.png)
- немного ломаное повышение общей награды и снижение потери значения
- изменил learning_rate до 1.0e-4 (начальная скорость обучения)
- ![image](https://user-images.githubusercontent.com/79518116/205125618-9e4bb2bb-6058-4b40-a06a-65829c7e7cb8.png)
- общая награда равна 1, плавный спад потери значения

## Задание 2 
### Опишите результаты, выведенные в TensorBoard. 
- Cumulative Reward - общая награда, должна постепенно увеличиваться до 1
- Episode Length - средняя продолжительность эпизода обучения
- Policy Loss - величина потери политики(процесс принятия решений), уменьшается во время успешного эпизода
- Value Loss - потеря значения, влияет на точность прогноза следующего состояния агентом, должна уменьшаться
- Entropy - насколько случайны решения модели, должен уменьшаться во время успешного эпизода
- Epsilon - влияет на быстроту развития поведения
- Learning Rate - начальная скорость обучения, должен уменьшаться линейно
- Beta - cила регуляризации энтропии, делает поведение более случайным, должен уменьшаться

## Выводы
-В ходе лабораторной работы я научился с помощью ML Agent внедрять и изменять экономические системы в проекте Unity, а также выводить графики с помощью TensorBoard и анализировать их.
## Powered by

**BigDigital Team: Denisov | Fadeev | Panov**
