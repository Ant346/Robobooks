# 8.5 Навигация и локализация с использованием карты и amcl

Если у вас нет оборудования для построения карты с использованием вашего собственного робота, вы можете использовать тестовую карту в rbx1\_nav / maps для этой главы. В противном случае, если вы создали собственную карту, следуя инструкциям в предыдущем разделе, вы можете использовать ее здесь. 

ROS использует amcl package для локализации робота на существующей карте с использованием текущих данных сканирования, поступающих с лазера или встроенной камеры робота. Но прежде чем попробовать amcl на реальном роботе, давайте запустим искусственную локализацию в симуляторе ArbotiX.
