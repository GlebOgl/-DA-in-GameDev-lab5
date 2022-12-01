# АНАЛИЗ ДАННЫХ И ИСКУССТВЕННЫЙ ИНТЕЛЛЕКТ [in GameDev]
Отчет по лабораторной работе #4 выполнил(а):
- Оглоблин Глеб Александрович
- РИ210941
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
познакомиться и реализовать прецептрон

## Задание 1
### в проекте Unity реализовать прецептрон, который умеет производить вычисления: OR, AND, NAND, XOR
- создал проект юнити и подключил пустому объекту скрипт preceptron.cs
- ![image](https://user-images.githubusercontent.com/79518116/204323357-d8361acb-cf49-4c22-b4f7-adcfa9328d04.png)


```C#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

[System.Serializable]
public class TrainingSet
{
    public double[] input;
    public double output;
}

public class Preceptron : MonoBehaviour
{
    public TrainingSet[] ts;
    double[] weights = {0,0};
    double bias = 0;
    double totalError = 0;

    double DotProductBias(double[] v1, double[] v2)
    {
        if (v1 == null || v2 == null)
            return -1;

        if (v1.Length != v2.Length)
            return -1;

        double d = 0;
        for (int x = 0; x < v1.Length; x++)
        {
            d += v1[x] * v2[x];
        }

        d += bias;

        return d;
    }

    double CalcOutput(int i)
    {
        double dp = DotProductBias(weights, ts[i].input);
        if (dp > 0) return (1);
        return (0);
    }

    void InitialiseWeights()
    {
        for (int i = 0; i < weights.Length; i++)
        {
            weights[i] = Random.Range(-1.0f, 1.0f);
        }
        bias = Random.Range(-1.0f, 1.0f);
    }

    void UpdateWeights(int j)
    {
        double error = ts[j].output - CalcOutput(j);
        totalError += Mathf.Abs((float)error);
        for (int i = 0; i < weights.Length; i++)
        {
            weights[i] = weights[i] + error * ts[j].input[i];
        }
        bias += error;
    }

    public double CalcOutput(double i1, double i2)
    {
        double[] inp = new double[] { i1, i2 };
        double dp = DotProductBias(weights, inp);
        if (dp > 0) return (1);
        return (0);
    }

    public void Train(int epochs)
    {
        InitialiseWeights();

        for (int e = 0; e < epochs; e++)
        {
            totalError = 0;
            for (int t = 0; t < ts.Length; t++)
            {
                UpdateWeights(t);
                Debug.Log("W1: " + (weights[0]) + " W2: " + (weights[1]) + " B: " + bias);
            }
            Debug.Log("TOTAL ERROR: " + totalError);
        }
    }

    // Start is called before the first frame update
    void Start()
    {
        Train(4);

        Debug.Log("Test 0 0: " + CalcOutput(0,0));
        Debug.Log("Test 0 1: " + CalcOutput(0,1));
        Debug.Log("Test 1 0: " + CalcOutput(1,0));
        Debug.Log("Test 1 1: " + CalcOutput(1,1));
    }

    // Update is called once per frame
    void Update()
    {
        
    }
}
```
-задал количество тренировок равное 4
-работа операции OR
-![image](https://user-images.githubusercontent.com/79518116/204323943-fed21f31-4792-42ea-96ea-87003e8cbb09.png)
-на 4 итерации прецептрон обучился и выдал верные результаты
-работа AND
-![image](https://user-images.githubusercontent.com/79518116/204324823-aa7def2b-4272-4cd9-b0a3-4cbb7975bd7f.png)
-обучился только на 5 итерации(изменил количество тренировок до 8), верные результаты
-работа NAND
-![image](https://user-images.githubusercontent.com/79518116/204325424-27db2e46-8efd-4a95-89d8-39cd0fef1d3d.png)
-обучился на 7, результаты правильные
-работа XOR
-![image](https://user-images.githubusercontent.com/79518116/204325675-2a4ee9c7-981c-479b-873b-a10f16989852.png)
-не обучился, у операции не верные результаты, из-за того что линейная модель перцептрона не может правильно разделить одной линией плоскость XOR на нули и единицы
## Задание 2 
### построить графики зависимости количества эпох от ошибок обучения. Указать от чего зависит необходимое количество эпох
-метод для вычесления средней ошибки за количество эпох(5) среди range(100) повторений
```C#
public double GetStatistics(int epochs, TrainingSet[] ts, int range)
    {
        var statArray = new double[range];
        for (int i = 0; i < range; i++)
        {
            Train(epochs);
            statArray[i] = totalError;
        }
        var res = 0.0;
        foreach (var item in statArray)
        {
            res += item;
        }
        return res / range;
    }
```
-результатаы для OR
-![image](https://user-images.githubusercontent.com/79518116/204494427-42d25781-4d82-4326-bf86-9de068901357.png)
-результатаы для AND
-![image](https://user-images.githubusercontent.com/79518116/204495549-46be8c96-afa1-4002-94ce-eabd43438098.png)
-результатаы для NAND
-![image](https://user-images.githubusercontent.com/79518116/204496923-942ad66d-cf30-4b88-a7bf-ad594249414f.png)
-результатаы для XOR
-![image](https://user-images.githubusercontent.com/79518116/204497468-1affa487-ef5a-4424-be08-2ef72d73298d.png)

## Задание 3
### построить визуальную модель работы прецептрона на сцене Unity
-сделал новый скрип Preceptron.cs в уотором добавил метод OnCollisionEnter, при соприкосновении кубы должны менять цвет в соответствии с операцией OR (белый куб = 1, черный = 0)
```C#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;


public class Perceptron : MonoBehaviour
{

    public TrainingSet[] Ts;

    public int Value;

    public Material True;
    public Material False;

    public GameObject Cube;

    private class PerceptronClass
    {
        public TrainingSet[] ts;
        double[] weights = { 0, 0 };
        double bias = 0;
        double totalError = 0;

        double DotProductBias(double[] v1, double[] v2)
        {
            if (v1 == null || v2 == null)
                return -1;

            if (v1.Length != v2.Length)
                return -1;

            double d = 0;
            for (int x = 0; x < v1.Length; x++)
            {
                d += v1[x] * v2[x];
            }

            d += bias;

            return d;
        }

        double CalcOutput(int i)
        {
            double dp = DotProductBias(weights, ts[i].input);
            if (dp > 0) return (1);
            return (0);
        }

        void InitialiseWeights()
        {
            for (int i = 0; i < weights.Length; i++)
            {
                weights[i] = Random.Range(-1.0f, 1.0f);
            }
            bias = Random.Range(-1.0f, 1.0f);
        }

        void UpdateWeights(int j)
        {
            double error = ts[j].output - CalcOutput(j);
            totalError += Mathf.Abs((float)error);
            for (int i = 0; i < weights.Length; i++)
            {
                weights[i] = weights[i] + error * ts[j].input[i];
            }
            bias += error;
        }

        public double CalcOutput(double i1, double i2)
        {
            double[] inp = new double[] { i1, i2 };
            double dp = DotProductBias(weights, inp);
            if (dp > 0) return (1);
            return (0);
        }

        public void Train(int epochs, TrainingSet[] ts)
        {
            this.ts = ts;
            InitialiseWeights();

            for (int e = 0; e < epochs; e++)
            {
                totalError = 0;
                for (int t = 0; t < ts.Length; t++)
                {
                    UpdateWeights(t);
                    //Debug.Log("W1: " + (weights[0]) + " W2: " + (weights[1]) + " B: " + bias);
                }
                //Debug.Log("TOTAL ERROR: " + totalError);
            }
        }

        public double GetStatistics(int epochs, TrainingSet[] ts, int range)
        {
            var statArray = new double[range];
            for (int i = 0; i < range; i++)
            {
                Train(epochs, ts);
                statArray[i] = totalError;
            }
            var res = 0.0;
            foreach (var item in statArray)
            {
                res += item;
            }
            return res / range;
            
        }
    }

    IEnumerator UpdateCoroutine()
    {
        yield return new WaitForSeconds(2);
        this.transform.position = pos;
        this.gameObject.GetComponent<Renderer>().material = material;
        
    }

    private void OnCollisionEnter(Collision collision)
    {
        Debug.Log(collision);
        var Cube = collision.gameObject.GetComponent<Perceptron>();
        if (Cube)
        {
            if (perceptron.CalcOutput(this.Value, Cube.Value) == 1)
            {
                this.gameObject.GetComponent<Renderer>().material = True;
            }
            else
            {
                this.gameObject.GetComponent<Renderer>().material = False;
            }
            StartCoroutine(UpdateCoroutine());
        }
    }

    private PerceptronClass perceptron;
    private Vector3 pos;
    private Material material;

    void Start()
    {
        perceptron = new PerceptronClass();
        perceptron.Train(8, Ts);

        pos = this.transform.position;
        material = this.gameObject.GetComponent<Renderer>().material;
    }

    void Update()
    {

    }
}
```
-демонстрация работы
-![2022-11-29-21-07-23](https://user-images.githubusercontent.com/79518116/204582144-4e41fabd-6eb0-4792-9839-be4795884159.gif)

## Выводы
-В ходе лабораторной работы я изучил работу перцептрона, проблему XOR, а также создал собственный перцептрон, который может безошибочно выполнять операции AND, OR, NAND, а также визуализировал его работу
## Powered by

**BigDigital Team: Denisov | Fadeev | Panov**
