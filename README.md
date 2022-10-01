# ПК.С1. Вр_и_доп.реал.
Отчет по лабораторной работе #1 выполнил:
- Волков Илья Евгеньевич
- РИ-300004

Отметка о выполнении заданий (заполняется студентом):

| Задание | Выполнение | Баллы |
| ------ | ------ | ------ |
| Задание 1 | * |  |
| Задание 2 | * |  |
| Задание 3 | * |  |

знак "*" - задание выполнено; знак "#" - задание не выполнено;

Работу проверили:

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
Ознакомиться с основными функциями Unity и взаимодействием с объектами внутри редактора.

## Задание 1
### В разделе «ход работы» пошагово выполнить каждый пункт с описанием и примерами реализации задач по теме видео самостоятельной работы.
Ход работы:
1) Создать новый проект из шаблона 3D – Core;
2) Проверить, что настроена интеграция редактора Unity и Visual Studio Code
(пункты 8-10 введения);
3) Создать объект Plane;
4) Создать объект Cube;
5) Создать объект Sphere;
6) Установить компонент Sphere Collider для объекта Sphere;
7) Настроить Sphere Collider в роли триггера;
8) Объект куб перекрасить в красный цвет;
9) Добавить кубу симуляцию физики, при это куб не должен проваливаться
под Plane;
10) Написать скрипт, который будет выводить в консоль сообщение о том,
что объект Sphere столкнулся с объектом Cube;
11) При столкновении Cube должен менять свой цвет на зелёный, а при
завершении столкновения обратно на красный.

Скриншоты:
![image](https://user-images.githubusercontent.com/74401943/192089619-e847868c-5b75-4aae-87ff-bc41c5319bee.png)
![image](https://user-images.githubusercontent.com/74401943/192089553-ac73869f-cf5d-4f66-afe0-a3f536fb3077.png)
![image](https://user-images.githubusercontent.com/74401943/192089567-135dcd73-1191-4ec6-973f-a0be5f4ef29c.png)

Код:
```c#

using UnityEngine;

public class IntersectionListener : MonoBehaviour
{
    private void OnTriggerEnter(Collider other)
    {
        Debug.LogWarning($"{gameObject.name} соприкоснулся с {other.gameObject.name}");
        other.GetComponent<MeshRenderer>().material.color = Color.green;
    }

    private void OnTriggerExit(Collider other)
    {
        other.GetComponent<MeshRenderer>().material.color = Color.red;
    }
}

```



## Задание 2
### Продемонстрируйте на сцене в Unity следующее:
- Что произойдёт с координатами объекта, если он перестанет быть
дочерним?
- Создайте три различных примера работы компонента RigidBody.

#### Часть 1:
Результаты выполнения:

Скриншоты: 
1. ![image](https://user-images.githubusercontent.com/74401943/192089857-15970a1c-a462-445d-9501-dc1ac3473a5e.png)
2. ![image](https://user-images.githubusercontent.com/74401943/192089858-3871b948-5873-42be-b3e3-e4dd6a59f08d.png)
3. ![image](https://user-images.githubusercontent.com/74401943/192089865-419a3d5a-74f7-46e6-bd0f-7d978299a1ef.png)

На первом скриншоте изначальные (локальные) координаты объекта Cube. На втором скриншоте координаты родительского объекта InteractiveObjects. Если Cube перестанет быть дочерним объектом InteractiveObjects, то координаты куб увеличаться на координаты InteractiveObjects по след. формулам:
```
Cube.x += InteractiveObjects.x;
Cube.y += InteractiveObjects.y;
Cube.z += InteractiveObjects.z;
```
К слову, Rotation InteractiveObjects тоже прибывиться к Rotation Cube.

#### Часть 2:

Скриншоты:
1. ![image](https://user-images.githubusercontent.com/74401943/192090170-8772e49a-af6a-4e15-a122-212dc79efd6b.png)
2. ![image](https://user-images.githubusercontent.com/74401943/192090187-f14ef46e-6742-4d10-882d-2c7069f6fec0.png)
3. ![image](https://user-images.githubusercontent.com/74401943/192090237-c0310bda-3586-4d4b-b6f6-3206d94c565e.png)

На первом скриншоте мы увеличили значение поля Drag, тем самым увеличив "сопротивление" объекта Cube. Это значит, что взаимодействовать с окружающей средой он будет медленней.

На втором скриншоте мы задали полю IsKinematic значение True. Теперь на объект Cube не действуют физ. силы. Это полезно для создания ragdoll'ов персонажей в играх. Когда мы хотим, чтобы персонаж стал "тряпичной куклой" просто ключаем IsKinematic. По сути это enable у rigidbody.

На третьем скриншоте мы заморозили движение объекта Cube по Y, что не позволяет ему более самостоятельно и с помощью других объектов двигаться по Y, однако гравитация на него все еще действует.

## Задание 3
### Реализуйте на сцене генерацию n кубиков. Число n вводится пользователем после старта сцены.

Скриншоты:
1. ![image](https://user-images.githubusercontent.com/74401943/192092059-34e3b311-e5dc-49fa-af38-511fad131546.png)
2. ![image](https://user-images.githubusercontent.com/74401943/192092107-e4626a62-58d2-429e-8c4a-409b99afcfaf.png)

Код:
```c#

using System.Collections;
using TMPro;
using UnityEngine;
using UnityEngine.UI;
using Exception = System.Exception;

public class CubeGenerator : MonoBehaviour
{
    [Header("Real Data")]
    [SerializeField] private GameObject cubeTemplate;
    [SerializeField] private Transform spawnPosition;
    
    [Header("UI Data")]
    [SerializeField] private TMP_InputField inputField;
    [SerializeField] private Button button;

    private void Start()
    {
        button.onClick.AddListener(OnButtonClick);
    }

    private void OnButtonClick()
    {
        var countCubes = 0;
        
        try
        {
            countCubes = int.Parse(inputField.text);
        }
        catch (Exception exception)
        {
            Debug.LogException(exception);
        }

        if (countCubes > 0)
            StartCoroutine(GenerateCubes(countCubes));
    }

    private IEnumerator GenerateCubes(int countCubes)
    {
        for (int i = 0; i < countCubes; i++)
        {
            Instantiate(cubeTemplate, spawnPosition);
            yield return new WaitForSeconds(0.25f);
        }
    }
}


```

## Выводы

В ходе выполнения лабораторной работы мы познакомились с основными функциями Unity и взаимодействием с объектами внутри редактора.

В целом, все, что требовалось сделать, у меня не вызвало трудностей, ибо я уже работал со всем этим.


# ПК.С1. Вр_и_доп.реал.
Отчет по лабораторной работе #2 выполнил:
- Волков Илья Евгеньевич
- РИ-300004

Отметка о выполнении заданий (заполняется студентом):

| Задание | Выполнение | Баллы |
| ------ | ------ | ------ |
| Задание 1 | * |  |
| Задание 2 | * |  |
| Задание 3 | * |  |

знак "*" - задание выполнено; знак "#" - задание не выполнено;

Работу проверили:

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
Познакомится с XR возможностями Unity.
## Задание 1
### Пошагово выполнить каждый пункт по примеру предоставленных видеоматериалов:
1. Создайте новый Unity проект из шаблона 3D-Core:
![image](https://user-images.githubusercontent.com/74401943/193418822-d137d11b-0ce7-4cf9-a444-56fca12cc7a0.png)

2. Откройте вкладку Edit -> Project settings;
3. Установите XR Plugin Management;
4. Настройте XR Plugin Management на работу через SDK OpenXR:
![image](https://user-images.githubusercontent.com/74401943/193418891-c7fcc54f-4696-4c4a-a174-aa7fb426becb.png)

5. Настройте режим рендера VR на каждый глаз;
6. Добавить поддержку контроллеров вашего оборудования:
![image](https://user-images.githubusercontent.com/74401943/193418940-42422415-9645-418e-a0da-5203fd2c13e4.png)

7. Через вкладку Windows -> Pacage Manager добавьте и установите пакет
com.unity.xr.interaction.toolkit;
8. Импортируйте Starter Assets из установленного пакета;
9. Настройте Input system на основе импортированного Starter Assets:
![image](https://user-images.githubusercontent.com/74401943/193418998-cfebe0d2-00ac-4401-a41e-95502c26c321.png)

10. Скачайте и установите Steam и Steam VR;
11. Настройте и подключите к PC ваше VR оборудование;
12. Вернитесь в Unity и настройте запуск проекта через SteamVR:
(с контроллерами все ок, просто на момент написания отчета они уже отлючились)
![image](https://user-images.githubusercontent.com/74401943/193419168-36bc78fe-ddc5-482e-955c-4cdbf0b8192c.png)

13. Добавьте объект Plane;
14. Добавьте на сцену объект XR-Orig (Action Base);
15. На объект XR Interaction Manager создайте компонент Input Action
Manager;
16. Добавьте в Input Action Manager настроенный Input System;
17. Запустите проект и убедитесь, что он воспроизводится на VR
оборудовании:
![image](https://user-images.githubusercontent.com/74401943/193419289-5b423d98-922f-454b-ba21-954fc8bc5b34.png)

## Задание 2
### Привести ответ на вопросы:
1. Что значит X в аббревиатуре XR?
Это такая универсальная аббревеатура AR, MR, VR.
2. Какие SDK поддерживает XR Plugin Management по Default?
![image](https://user-images.githubusercontent.com/74401943/193419378-b04dc3bb-d6f5-4ca1-a2c9-1ede988b5310.png)
![image](https://user-images.githubusercontent.com/74401943/193419394-b5eea160-28c9-4bd5-9591-5cd4efd00293.png)

## Задание 3
### На сцену в Unity добавьте три различных элемента из XRInterraction Toolkit.
![image](https://user-images.githubusercontent.com/74401943/193419441-42aa4fd1-2e32-46c7-9383-3dbf25ada61f.png)

## Выводы
В ходе выполнения лабораторной работы познакомится с XR возможностями Unity. С инстрментами был знаком и раньше.
