# Каталог src

Файл запуска будет запущен с помощью файла start\_training.py. 

 Это файл, который организует обучение. Давайте посмотрим, что он делает шаг за шагом:

* Инициализирует узел ROS

```text
rospy.init_node('drone_gym', anonymous=True)
```

* Создает атмосферу Gym

```text
env = gym.make('QuadcopterLiveShow-v0')
```

Это основной класс, который предоставляет OpenAI. Каждый эксперимент OpenAI должен быть определен в определенной среде . При такой организации разные разработчики могут тестировать различные алгоритмы, всегда сравнивая их с одной и той же средой. Следовательно, мы можем сравнить, какой алгоритм лучше в одних и тех же условиях.

Среда определяет доступные агенту действия, способы расчета вознаграждения на основе его действий и результатов, а также способы получения состояния мира агента.

Каждая среда в OpenAI должна определять следующие вещи:

•	Функция \_reset, которая устанавливает среду обучения в ее начальное состояние.

•	Функция \_step, которая производит изменения в среде на основе последнего выполненного действия, а затем наблюдает за новым состоянием среды. Основываясь на этих двух вещах, он генерирует вознаграждение.

•	Функция \_seed, используемая для инициализации генератора случайных чисел.

•	Функция render используется для отображения на экране того, что происходит в окружающей среде.

•	Какова задача, которую агент должен решить в этой среде.

•	Количество возможных действий в окружающей среде. В нашем случае мы позволяем роботу выполнить 5 действий.

•	Способ расчета вознаграждения, полученного агентом. Это точки, предоставляемые агенту на каждом шаге, основанные на том, насколько хорошо или насколько плохо он сделал в окружающей среде для решения поставленной задачи.

•	Способ, определяющий, решена ли поставленная задача.

![](../.gitbook/assets/image%20%283%29.png)

Загрузка параметров алгоритма с сервера ROS param

```text
 Alpha = rospy.get_param("/alpha")
  Epsilon = rospy.get_param("/epsilon")
  Gamma = rospy.get_param("/gamma")
  epsilon_discount = rospy.get_param("/epsilon_discount")
  nepisodes = rospy.get_param("/nepisodes")
  nsteps = rospy.get_param("/nsteps")
```

Это те параметры, которые нужны нашему алгоритму обучения. Этот раздел будет меняться в зависимости от параметров, необходимых вашему алгоритму.

