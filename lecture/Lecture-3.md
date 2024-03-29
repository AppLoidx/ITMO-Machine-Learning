# Лекция №3

Темы:

<hr>

Метод опорных векторов

Метод деревьев



<hr>



## Примеры задач классификации

* Предсказание лояльности мутации
* Предсказание пола неизвестного пользователя
* Предсказание категории письма
* Определение языка для неизвестного текста
  (с учителем, без учителя активно здесь используются)
* Определение объекта на фотографиях



> **Задание** : посмотреть классификацию в видео



> **Напоминание**: спросить про результаты исследований в ЭКГ



## Методы классификации

 ### Линейный классификатор

Алгоритм классификации, основанный на построении линейно-разделяющей поверхности.

**В случае, двух классов**: разделяющей поверхностью является гиперплоскость, которое делит пространство признаков на два полу-пространства.

**Правила**:

1. Найти ближайшую пару точек в выпуклых оболочках обеих множеств.
2. Построить серединный перпендикуляр к отрезку ,соединяющему эти точки



При этом мы полагаем, что максимизация зазора между классами способствует более уверенной классификации. Для нас это означает что расстояние между двумя ближайшими точками, лежащими по разные стороны гиперплоскости - максимально.



Оптимальная разделяющая гиперплоскость - это плоскость, которая соответствует верхнему условию.

#### Метод опорных векторов (SVM)

**Support Vector Machine**

Это линейный алгоритм, который используется в задачах регрессии и классификации.

Цель метода найти плоскость разделяющую точки.



Отличия этого метода заключается в критерии качества разделимости. Меры разделимости основываются на понятии *зазора, который понимается как ширина разделяющей полосы между классами.



Данный метод отыскивает образцы, находящиеся на границе между классами



Алгоритм обучения находит среди элементов обучающего множества точки лежащие на границе двух подмножеств и строит между этими точками разделяющую поверхность. 

*Эти точки называются опорными векторами*



SVM бывает линейной и нелинейной



**Линейная классификация**

Считается хорошей, если область между границами пуста

Наилучшей функцией классификации является функция, для которой ожидаемый риск минимален.



**Нелинейная классификация**

Не всегда легко найти линейную границу между двумя классами.



Проводим увеличение размерности, то есть перенос данных из плоскости в трехмерное пространство, где возможно построить такую плоскость, которая идеально разделит наши образцы на два класса. Делается это с помощью добавления *Оператора ядра* (с математической стороны, это любая положительная определенная симметричная плоскость).



**Плюсы и минусы**

* Сложность построения модели заключается в том, что чем выше размерность пространства, тем сложнее с ним работать
* (-) Для классификации используется не все множество образцов, а лишь их небольшая часть, которая находится на границах
* (+) Для классификации данного метода достаточно небольшого набора данных.
* (+) Для использования данного алгоритма нет необходимости предварительно понимать поведение данных. Достаточно наблюдения за данными и связи внутри них.

* Метод работает по принципу *черного ящика* (работает в слепую)

* (-/+) Алгоритм очень чувствителен к выбросам (шумам). Выбросы в исходных данных становятся опорными объектами нарушителями и напрямую влияют на разделяющую гиперплоскость.

* (-) Нет единого общего метода построения спрямляющих пространства или ядер для конкретной задачи

  

### Метрика оценки качества (классификации)



`Accuracy = P/N` - процент верных предсказания (доля правильных ответов)

`P` - кол-во документов

`N` - размер обучающей выборки



Она присваивает всем документам одинаковый вес, что может быть некорректно, если распределение документов смещено в сторону одного.

На практике Accuracy может быть большим, но под конкретный класс работать плохо



Решить можно  переходом к изменению подхода к формальной оценке качества.



**Пример**

Идея: На сколько хорошо мы угадываем класс?

При классификации на два класса (да\нет) у нас может быть четыре исхода:

Строится **матрица неточностей**

1. TP (true positive) - положительное решение. Было `да`, предсказали `да`

2. TN (true negative) - Было `нет`, нашли `нет`
3. FP (false positive) - истинное значение было `нет`, но предсказали `да`
   **Ошибка первого рода**
4. FN (false negative) - истинное значение было `да`, а определили `нет`



**Recall and precision** 



**Precision** - доля правильно определенных документов из всех найденных.

**Recall** - доля правильных из всех документов. 

Recall демонстрирует способность алгоритма обнаружить данный класс, а precision различать этот класс от других классов. В отличие от аккуратности не зависят от несбалансированных данных. 



**Метрика F-мера** (в презентации формула!). Максимальна, когда максимальны `precision` и `recall` и наоборот стремится к нулю, если один из параметров стремится к нулю.



### ROC-кривая

Для оценки качества конкретной задачи можно использовать графический метод оценки.

ROC - кривая ошибок. Данная кривая представляет из себя линию от `0.0` до `1`

**ROC-кривая** это зависимость количества **верно классифицированных положительных примеров** (чувствительность, True Positive или Reacall, например) от количества **неверно классифицированных отрицательных** примеров. 

Количественную характеристику нам дает **AUC** - это площадь ограниченная ROC-кривой и осью X

Это доля ложных положительных классификаций. Чем выше показатель AUC, тем качественнее классификатор.

Каждая точка на графике представляет собой ...

Площадь под кривой показывает качество алгоритма (больше лучше), кроме этого важной является крутизна самой кривой. Мы хотим максимизировать `True Positive`, минимизируя `False Positive`



### Практические аспекты применения

1. Если есть возможность использования одной и той же метрики, используйте одну и ту же.
2. Внимательно выбирайте правильную метрику.
3. Учитывайте, что может быть сильная разная цена ошибки (например, при раке)
4. Выбросы могут сильно исказить метрику