# АНАЛИЗ ДАННЫХ И ИСКУССТВЕННЫЙ ИНТЕЛЛЕКТ [in GameDev]
Отчет по лабораторной работе #5 выполнил(а):
- Лещишин Роман Александрович
- РИ-210914

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

## 5. Лабораторная работа. Интеграция экономической системы в проект Unity и обучение ML-Agent
## Цель работы
Обучение ML-Agent на примере экономической системы в Unity.

## Задание 1
Измените параметры файла. yaml-агента и определить какие параметры и 
как влияют на обучение модели.

Обучение модели на стандартных значениях параметров.

Стандартные параметры Economic.yaml:

![Image_1Economic](https://user-images.githubusercontent.com/114608473/208230734-ea46db26-767b-4c0f-8353-817ff01649cc.jpg)

Cцена в Unity
![Image_1TrainingMLA](https://user-images.githubusercontent.com/114608473/208230449-57001425-9950-448a-bb97-028b2aef1a1b.jpg)

Результаты обучения в TensorBoard
![Image_1TensorBoard](https://user-images.githubusercontent.com/114608473/208234228-f9326f0c-d53d-4d40-95f9-902a61e4f3bb.jpg)

По графикам видно, что общее вознаграждение Cumulative Reward растёт, а потеря значения Value Loss, уменьшается.

Какие параметры и как влияют на обучение модели:

Learning_rate

learning_rate - коэффициент скорости обучения. Скорость обучения определяет величину изменений, которую оптимайзер может внести за один раз. Нужно подбирать оптимальное значение: если взять слишком большое - то обучение будет не стабильным - модель будет быстрее обучаться, но и шаги станут больше и модель может застрять на месте; если взять слишком маленькое - модель будет заметно дольше обучаться и точно так же может застревать на месте. Значение следует уменьшать, если обучение нестабильно, а вознаграждение не увеличивается постоянно. Попробовал увеличить параметр до 1.0e-4 и обучить модель:

![Image_1Learning_rate](https://user-images.githubusercontent.com/114608473/208234269-71791bdd-c0ef-4feb-b64c-f8fca396b40e.jpg)

Как видно из графиков, из-за того, что значение увеличилось, сеть "застопарилась" и даже пошла в обратном направлении на промежутке 30000 - 40000 steps.

![Image_1Learning_rate2](https://user-images.githubusercontent.com/114608473/208235190-943e8814-4c89-4698-b36c-82c26cd249ed.jpg)

Вознаграждение увеличивается немного плавнее в отличие от стандартных параметров, остальные графики почти такие же. Стало намного лучше в сравнении с предыдущим значением параметра learning_rate: 1.0e-4.

На 1 эпохе, перцептрон не успел обучиться, значит слишко мало.
![Image_1ORtr1](https://user-images.githubusercontent.com/114608473/207904208-fc7c7521-ca2e-4b74-ac64-eb246914aa6e.jpg)
На 3 эпохе значение ошибки осталось тем же.
![Image_1ORtr3](https://user-images.githubusercontent.com/114608473/207904593-91e3f7f4-a760-405d-851e-5d7a3c85b728.jpg)
Перцептрон обучился на 5 эпохе.
![Image_1ORtr5](https://user-images.githubusercontent.com/114608473/207904728-ac2ce7c9-1599-4753-9b4f-18daa57412c2.jpg)
Для закрепления проверил значение ошибки на 8 эпохах.
![Image_1ORtr8](https://user-images.githubusercontent.com/114608473/207904889-4fec54c5-ba1e-4a67-b0a4-78c9856e9e56.jpg)
Вычисление AND

Для обучения этой операции перцептрону потребовалось больше эпох, чем в OR.
![Image_2ANDtr1](https://user-images.githubusercontent.com/114608473/207905229-f851b8c2-949b-4249-93c0-dea48901d101.jpg)
![Image_2ANDtr9](https://user-images.githubusercontent.com/114608473/207905283-a98c19b1-adaa-43c3-a14f-20977c0f1ed0.jpg)
Из значений ошибки можно придти к выводу, что перцептрону для успешного обучения нужно как минимум 9 эпох.

Вычисление NAND

Значения ошибки при обучении очень похожи на операцию AND.
![Image_3NANDtr1](https://user-images.githubusercontent.com/114608473/207906562-ede778b6-1dbe-430e-b210-f6fd606caf08.jpg)
![Image_3NANDtr8](https://user-images.githubusercontent.com/114608473/207906588-0e6b0f58-32df-4212-8021-4b2cf0cb7a95.jpg)
Вычисление XOR

При увеличении количества эпох, значение ошибки только увеличивается, что доказывает утверждение Minsky о XOR problem.
![Image_4XORtr1](https://user-images.githubusercontent.com/114608473/207906987-701830bf-15a5-40f2-a9da-45b73587267b.jpg)
![Image_4XORtr16](https://user-images.githubusercontent.com/114608473/207907081-9f2c0f6b-f1da-4884-a0bc-2dfdf3f077f0.jpg)
Перцепторон может обучаться вычислению только линейных функций, а XOR таковой не является.
## Задание 2
Построить графики зависимости количества эпох от ошибки обучения. Указать от чего зависит необходимое количество эпох обучения.

График OR

![Image_graficOR](https://user-images.githubusercontent.com/114608473/207915129-f70fb653-52b4-4f77-aaac-dc0502e0e7ce.jpg)

График AND

![Image_graficAND](https://user-images.githubusercontent.com/114608473/207915334-496981f7-71a7-455c-b0ac-79f1ed3f7ac9.jpg)

График NAND

![Image_graficNAND](https://user-images.githubusercontent.com/114608473/207915467-49cf6c22-c3ef-4bbd-8835-bc28acfa7e9f.jpg)

График XOR

![Image_graficXOR](https://user-images.githubusercontent.com/114608473/207915547-62c1864e-9872-4b4b-91a8-2b20e6bf065a.jpg)

Задание 2 выводы.

Для логического выражения OR, требуется меньше эпох для обучения перцептрона, чем у выражений AND и NAND, которым требуется больше эпох для обучения, и, желательно, чтобы их было больше восьми. А график зависимости значений ошибки от эпох выражения XOR ещё раз доказывает, что перцептрон не может обучиться, и с каждой новой эпохой его TotalError увеличивается.

Необходимое количество эпох обучения зависит от bias (смещения) и weights (весов). Это можно увидеть в скрипте Perceptron.cs.
## Задание 3
### Какова роль параметра Lr? Ответьте на вопрос, приведите пример выполнения кода, который подтверждает ваш ответ. В качестве эксперимента можете изменить значение параметра.

- Перечисленные в этом туториале действия могут быть выполнены запуском на исполнение скрипт-файла, доступного [в репозитории](https://github.com/Den1sovDm1triy/hfss-scripting/blob/main/ScreatingSphereInAEDT.py).
- Для запуска скрипт-файла откройте Ansys Electronics Desktop. Перейдите во вкладку [Automation] - [Run Script] - [Выберите файл с именем ScreatingSphereInAEDT.py из репозитория].

```py

import ScriptEnv
ScriptEnv.Initialize("Ansoft.ElectronicsDesktop")
oDesktop.RestoreWindow()
oProject = oDesktop.NewProject()
oProject.Rename("C:/Users/denisov.dv/Documents/Ansoft/SphereDIffraction.aedt", True)
oProject.InsertDesign("HFSS", "HFSSDesign1", "HFSS Terminal Network", "")
oDesign = oProject.SetActiveDesign("HFSSDesign1")
oEditor = oDesign.SetActiveEditor("3D Modeler")
oEditor.CreateSphere(
	[
		"NAME:SphereParameters",
		"XCenter:="		, "0mm",
		"YCenter:="		, "0mm",
		"ZCenter:="		, "0mm",
		"Radius:="		, "1.0770329614269mm"
	], 
)

```

## Выводы

Абзац умных слов о том, что было сделано и что было узнано.

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
