# Системы управления роботами и фреймворк для принятия решений

Прежде, чем погрузиться в написание нашей управляющей системы, давайте поговорим о теории, используемой для создания модульной, быстрой и гибкой системы управления роботами. Как я упоминал ранее, мы будем использовать два различных способа: систему мягкого реального времени и цикл НОРД. Первый предоставит нам фундамент для простого управления роботом, второй - основу для его автономности.

**Система мягкого реального времени**

Основной концепт работы робота, особенно движущегося, весьма прост. Существует основной управляющий цикл, повторяющий одни и те же действия раз за разом. Он считывает данные с датчиков, просматривает команды от оператора \(или же автономных систем робота\), изменяет состояние робота, основываясь на этих командах, посылает инструкции на двигатели и приводы, чтобы заставить робота двигаться:

![](.gitbook/assets/image%20%285%29.png)

Диаграмма выше показывает цикл НОРД, интегрированный в нашего робота. Робот может действовать как автономно, так и принимать команды от управляющей станции через сеть WiFi.

Все, что требуется от нас - заставить управляющий цикл все время работать по одной схеме. Нам нужно задать частоту обновления цикла, благодаря чему все системы робота станут работать лучше. Без какого-либо управления временем все системы робота будут требовать различное количество времени для выполнения, и все задачи по планированию и передвижению усложнятся в разы.

Если Вы ранее использовали ПИД-контроллеры для, например, движения робота с неизменной скоростью или нацеливания камеры на движущийся объект, Вы поймете важность временных шагов для получения хороших результатов.

**Управляющие циклы**

Чтобы управлять нашим роботом, мы должны установить какой-либо цикл обратной связи. Пусть, например, скажем роботу проехать 30 см вперёд. Роботу необходимо послать команду на движение двигателям и запустить какой-то механизм для измерения пройденного расстояния. Мы можем использовать различные способы, но будем использовать просто часы. Пусть робот проезжает 7.5 см в секунду. Управляющий цикл должен начать движения, и далее, при каждом проходе цикла, проверять, не прошло ли 4 секунды. Если прошли, он подаёт на двигатели команду остановки. Таймер в таком случае выступает в качестве управления, двигатели - управляемая система. Следующая диаграмма показывает простейший управляющий цикл. Мы хотим поддерживать постоянную температуру в баке с водой:

![](.gitbook/assets/image%20%287%29.png)

**Клапан** регулирует количество тепла, передаваемого от огня к баку. **Датчик температуры** определяет, холодная вода, горячая, или же она достигла подходящей температуры. **Контроллер** использует эту информацию для управления клапаном. Такая схема называется **закрытым управляющим циклом**.

Теперь же давайте подумаем об этом как о процессе. Мы начинаем процесс, получаем обратную связь, показывающую наш прогресс, изменяем или останавливаем процесс, основываясь на обратной связи. Этот может быть как управление скоростью, когда нам нужно заставить робота двигаться с заданной скоростью, или управление направлением, когда робот должен прицелиться или развернуться в заданном направлении.



Цель этих примеров - показать устройство управляющих систем. Делать всё это постоянно в цикле и есть управление в реальном времени.



Жёсткое реальное время подразумевает исполнение процесса чётко в заданный промежуток времени, т.е. процессы всегда занимают одно и то же время на выполнение.

Проблема этого способа заключается в том, что компьютер с запущенной ОС постоянно прерывается другими процессами, потоками, задачами. По своему опыту Вы знаете, что запуск одного и того же приложения, например, текстового редактора, всегда занимает разное количество времени, т.к. ОС прерывает этот процесс для выполнения других.

Такого рода поведение недопустимо для системы, в которой необходимо заранее знать продолжительность процесса с точностью до миллисекунды. Можно легко представить, что произошло бы, если бы автопилот самолёта постоянно прерывался бы доступом к диску и сети.

**Операционная система реального времени \(ОСРВ\)** позволяет программистам и разработчикам получить полный контроль над тем, как и когда выполняются процессы, когда и на сколько их можно прерывать и можно ли вообще. Управляющие циклы в ОСРВ всегда занимают одно и то же количество времени, что делает их очень надёжными. Важно знать, что в системе со жёстким реальным временем аппаратное обеспечение осуществляет контроль за соблюдением временных ограничений и обеспечение доступности ресурсов компьютера.

Мы может создать систему жёсткого реального времени на базе микроконтроллера Arduino, т.к. у него нет ОС и он может выполнять только одно задание единовременно. У нас есть полный контроль над временем исполнения любой программы. Так же у нашего робота будет более “способный” процессор - Raspberry Pi 3 с запущенной Linux. Этот компьютер, обладающей уже значительной мощью, может выполнять несколько задач одновременно, например, поддерживать ОС, сеть, графику, предоставлять пользовательский интерфейс и даже позволять одновременную работу нескольких пользователей.

**Мягкое реальное время** позволяет перейти к более расслабленному подходу. ПО продолжает следить за исполнением задач, обычно с помощью **кадров** \(заданных интервалов времени - совсем как кадры в фильмах\). Каждый кадр - это фиксированный временной отрезок, в основном 1/20 секунды, и программа разделяет задачи так, чтобы выполнять их в эти кадры. Мягкое реальное время больше подходит для нашей задачи по уборке комнаты, чем безопасная система жёсткого реального времени, кроме того, ОСРВ очень дорогие и требуют специального обучения. Мы будем рассматривать время исполнения управляющего цикла как систему обратной связи. Мы оставим дополнительное место в конце каждого цикла, чтобы позволить ОС завершить свою работу. Это позволит нам удостовериться, что цикл всегда совершается за одно и то же время. Так же, как и в примере с управляющим циклом, мы проведём измерение, определим ошибку и отредактируем данные при каждом проходе цикла.

Однако нам надо беспокоиться не только о времени обновления цикла. Так же необходимо помнить о колебаниях или случайных отклонениях во временном цикле, вызванных прерываниями ОС или другими вещами. Прерывание может увеличить время прохождения цикла, поэтому нам надо разработать управляющий цикл так, чтобы он мог выдержать определённое отклонение.

Сам процесс на практике оказывается довольно простым. Мы начинаем с инициализации таймера с настолько высокой точностью, насколько мы может установить. Мы пишем управляющий цикл на Python, поэтому будем использовать функцию `time.time()`, которая была разработана для измерения производительности программы. Каждый раз при вызове `time.time()` мы будем получать на выходе число с плавающей точкой, которое обозначает количество секунд в Unix-времени.

Принцип работы нашего процесса заключается в разделении всего на **кадры** фиксированного времени. Все, что мы будем делать, должно будет убраться в целое число кадров. Процессы будут выполняться со скоростью 30 кадров в секунду. С этой скоростью мы будем обновлять ожидаемое расположение робота, считывать показания с датчиков, посылать команды на двигатели. У нас так же есть и другие функции, работающие медленнее, чем 30 кадров в секунду, так что мы разделим их на несколько кадров. Некоторые функции будут вызываться в каждом кадре и работать со скоростью 30 кадров в секунду \(30 fps\). Например, у нас есть сонар, показания с которого обновляются 10 раз в секунду. Мы будем вызывать функцию `read sonar` каждый третий кадр. Мы сделаем так, чтобы частота вызова наших функций была одним из множителей 30, т.е. получим скорость в 30, 15, 10, 7.5, 6, 5, 4.28, …, 2 и 1 fps при вызове функции каждый первый, второй, третий и т.д. кадр. Мы можем даже получить скорость меньше 1 fps - функция, вызываемая каждая 60 кадров, будет выполняться раз в 2 секунды.

Нам нужно лишь удостовериться, что каждый процесс убирается в один кадр - 1/30 секунды или 0.033 секунды или 33 миллисекунды. Если процесс занимает больше времени, нам нужно или разделить его на части или запустить его в отдельном потоке или программе. Так же важно попытаться сбалансировать кадры и не производить все вычисления в одном. Следующая диаграмма показывает систему распределения задач, основанную на частоте 30 fps.

![](.gitbook/assets/image%20%286%29.png)

У нас есть четыре задачи для выполнения: **Задача А** работает на 15 fps, **Задача B** на 6 fps \(выполняется каждый пятый кадр\), **Задача С** на 10 fps \(каждые три кадра\) и **Задача D** на 30 fps, каждый кадр. Наш первый проход по расписанию \(выше\) включает в себя все четыре задачи, расположенные в одном кадре - в 1, 13, 25. Мы можем улучшить нагрузку, отложив запуск Задачи В на один кадр, как показано на нижнем расписании.

Это очень похоже на то, как работает мера в музыке, где мера - это определённое количество времени, а разные ноты имеют разную длительность - одна целая нота может возникнуть раз в меру, половинная - дважды и т.д.

Давайте же напишем небольшую программу для управления нашим временным циклом и немножко с ней поиграемся.

Это так волнительно, мы впервые пишем код вместе. Эта программа просто показывает временные промежутки управляющего цикла, который мы будем использовать в нашем роботе, и находится здесь только чтобы дать Вам немного поиграться с её параметрами и посмотреть на получившийся результат. Я думаю, это самая простая возможная версия цикла с мягким реальным временем, так что можете спокойно улучшать и изменять её.

На следующей диаграмме показано, что же мы будем делать в программе:

![](.gitbook/assets/image%20%284%29.png)

Теперь давайте начнём писать код. Это будет довольно простой и прямой код на Python, мы добавим красивости в будущем. Начнём с импорта библиотек. Неудивительно, что начнём с модуля времени. Так же мы будем использовать функцию `mean` из `numpy` и `matplotlib` для отрисовки графика. Мы также будем выполнять какие-либо вычисления для симулирования нагрузки.

`import time  
from numpy import mean  
import matplotlib.pyplot as plt  
import math  
#`

Теперь надо добавить какие-нибудь параметры для управления тестированием. Здесь Вы можете поэкспериментировать с различными интервалами. Основное управление идёт через `FRAMERATE` - количество обновлений в секунду. Давайте начнём с 30, как и раньше:

`# установка частоты кадров - сколько раз в секунду выполнять цикл?  
FRAMERATE = 30  
# сколько времени занимает каждый кадр в секундах?  
FRAME = 1.0/FRAMERATE  
# инициализация myTimer  
# это одна из переменных таймера, где мы будем хранить время, полученное от ОС  
myTimer = 0.0`

Длительность теста будет задаваться переменной `counter`. Общее время выполнения теста - `FRAME` умножить на количество циклов, т.е. `counter`. В нашем примере, 2000 кадров делить на 30 fps получается 66.6 секунды, чуть более одной минуты:


counter = 2000`

Мы будем контролировать время двумя способами. Сначала мы измерим время, требующееся программе на выполнение вычислений в одном кадре. У нас уже есть заготовка программы, выполняющей большое количество математических вычислений, для обеспечения нагрузки.

Мы измерим, сколько времени потребуется на запуск управляющей функции, что займет какое-то время кадра. Далее мы посчитаем, сколько времени кадра осталось и скажет компьютеру ожидать оставшееся время. Использование функции `sleep` позволяет освободить компьютер для других задач. Второй способ управления циклом: измерять полное время выполнения кадра \(время на вычисления плюс время ожидания\) и проверять, не вышли ли мы за пределы кадра. Мы будем использовать `TIME_CORRECTION` для обрезания времени ожидания:

`# множитель для вычислений временного цикла  
TIME_CORRECTION = 0.0  
# место для хранения данных`

Мы соберём некоторые данные для построения графика “дрожания” в конце программы. Для этого мы будем использовать структуру dataStore. Мы определим её в начале программы, т.к. это требует некоторого времени:

`dataStore = []  
# начинаем программу  
# выведем заголовок, показывающий, что тест начался  
print “НАЧАЛО ПОДСЧЁТА: ВРЕМЯ КАДРА”, FRAME, “ВРЕМЯ РАБОТЫ:”, FRAME*counter  
# инициализация часов`

В этом шаге мы установим некоторые переменные для измерения времени. Как я уже упоминал, нам нужно выполнить много кадров одинаковой длины. У каждого кадра есть две части: часть вычислений и часть ожидания. `myTime` - это время начала кадра. `newTime` - время конца вычислений. Также мы будем использовать masterTime для подсчёта общего времени работы программы:

`myTime = newTime = time.time()  
# сохраним время начала на будущее  
masterTime = myTime  
# начинаем цикл  
for ii in range(counter):`

Следующая секция — это “нагрузка”. Это может быть как расчёт угла наклона руки, так и распознавание команд. В основном эта секция занимает большую часть кадра, поэтому давайте выполним эти вычисления 1000 раз:

 `# начинаем кадр  
 # далее идёт нагрузка на процессор  
 for ii in range(1000):  
 x = 100  
 y = 23 + ii  
 z = math.cos(x)  
 z1 = math.sin(y)  
 #  
 # узнаем время после завершения вычислений  
 # это и есть время вычислений в кадре  
 #`

Теперь узнаем время вычислений. Тогда мы сможем подсчитать, сколько времени потребуется на ожидание. Главное - помнить, что _время работы + время ожидания = время кадра_. Давайте назовём это время `timeError`:

 `new time = time.time()  
 # как много времени прошло с начала кадра  
 # time = UNIX-время в секундах  
 # так что нам надо вычесть время начала кадра  
 myTimer = newTime - myTime  
 # сколько времени осталось до конца кадра?  
 timeError = FRAME - myTimer`

Теперь добавим сюда немного информации из предыдущих кадров. `TIME_CORRECTION` - это небольшая регулировка ошибок таймеров в предыдущем кадре. Ранее мы определили её как ноль, чтобы сейчас она не была неопределённой. Так же мы проведём небольшую проверку времени сна, чтобы избежать вылета таймера при отрицательном времени:

| ![](.gitbook/assets/image%20%288%29.png) | Мы будем использовать функцию `max` как быстрый способ убедиться, что время сна будет больше или равно нулю. `Max` возвращает больший из двух данных аргументов. Альтернативой ему будет что то типа `if a < 0 : a = 0`. |
| :--- | :--- |


 `# время ожидания  
 # TIME_CORRECTION поможет учесть все время, затраченное на получение времени  
 # также она исправляет ошибки таймеров  
 # мы используем пропорциональное управление для обеспечения сходимости системы  
 # если убрать делитель, система начнёт колебаться и выйдет из-под контроля  
 sleepTime = timeError + (TIME_CORRECTION / 1.5)  
 # быстрый способ избавиться от отрицательных чисел  
 # которые возможны из-за колебаний  
 # и могут привести к вылету программы  
 sleepTime = max(sleepTime, 0.0)`

А вот и команда sleep. Команда sleep не всегда выполняет ожидание в течение заданного периода времени, поэтому нам надо будет в будущем проверить её работу на ошибки:

 `# отправляем процесс в ожидание  
 time.sleep(sleepTime)`

Теперь начинается секция исправления времени. Мы вычислим, сколько времени занял кадр целиком и вычтем его из времени кадра, которое мы хотели получить \(FRAME\). Дальше мы присвоим TIME\_CORRECTION это значение. Так же я сохраню получившееся время кадра для отображения его на графике в будущем, используя matplotlib. Этот метод - одно из самых полезных преимуществ Python:

  `# устанавливаем таймер для следующего кадра  
 time2 = time.time()  
 measuredFrameTime = time2 - myTime  
 TIME_CORRECTION = FRAME - measuredFrameTime  
 dataStore.append(measuredFrameTime * 1000)  
 myTime = time.time()`

На этом заканчивается цикл. Этот пример делает 2000 проходов по циклу со скоростью 30 кадров в секунду и выполняется за 66.6 секунд. Вы можете поэкспериментировать с различными длинами цикла и частотой кадров.

Теперь, после выполнения программы, составим небольшой отчёт и покажем график. Мы выведем время кадра и полное время работы программы, подсчитаем среднюю длину кадра \(полное время / число кадров\), выведем среднюю ошибку кадра, которую можем получить, найдя среднее значение данных в `dataStore`:

`# тест закончен - выводим результаты  
#  
# полное время работы программы  
endTime = time.time() - masterTime  
# вычисляем среднее время кадра  
avgTime = endTime / counter  
print “ПОДСЧЁТ ЗАКОНЧЕН”  
print “ПЛАНИРУЕМОЕ ВРЕМЯ КАДРА:”, FRAME, “СРЕДНЕЕ ВРЕМЯ КАДРА:”, avgTime  
print “ПЛАНИРУЕМОЕ ПОЛНОЕ ВРЕМЯ:”, FRAME * counter, “РЕАЛЬНОЕ ПОЛНОЕ ВРЕМЯ:”, endTime  
print “СРЕДНЯЯ ОШИБКА КАДРА:”, FRAME - avgTime, “СУММАРНАЯ ОШИБКА:”, (FRAME * counter) - endTime  
print “СРЕДНЕЕ ВРЕМЯ ОЖИДАНИЯ:”, mean(dataStore), “СРЕДНЕЕ ВРЕМЯ ВЫЧИСЛЕНИЙ:”, (FRAME * 1000) - mean(dataStore)  
# цикл закончен, выводим результат на график  
# давайте посмотрим на получившиеся колебания  
plt.plot(dataStore)  
plt.show()`

Далее будут показаны результаты выполнения программы. Учтите, что средняя ошибка составляет лишь 0.00018 секунды или же 0.18 миллисекунды при кадре в 33 миллисекунды:

`НАЧАЛО ПОДСЧЁТА: ВРЕМЯ КАДРА 0.0333333333333 ВРЕМЯ РАБОТЫ: 66.6666666667  
ПОДСЧЁТ ЗАКОНЧЕН  
ПЛАНИРУЕМОЕ ВРЕМЯ КАДРА: 0.0333333333333 СРЕДНЕЕ ВРЕМЯ КАДРА: 0.0331549999714  
ПЛАНИРУЕМОЕ ПОЛНОЕ ВРЕМЯ: 66.6666666667 РЕАЛЬНОЕ ПОЛНОЕ ВРЕМЯ: 66.3099999428  
СРЕДНЯЯ ОШИБКА КАДРА: 0.000178333361944 СУММАРНАЯ ОШИБКА: 0.356666723887  
СРЕДНЕЕ ВРЕМЯ ОЖИДАНИЯ: 33.1549999714 СРЕДНЕЕ ВРЕМЯ ВЫЧИСЛЕНИЙ: 0.178333361944`

На следующем графике показаны временный промежутки программы. “Пики” указывают на **колебания**, вызванные прерываниями ОС. Как можно увидеть, программа контролирует время кадра, допуская лишь небольшие колебания. Без такого контроля время кадра увеличивалось бы с течением программы:

![](.gitbook/assets/image%20%282%29.png)
