# Подглава 2.4.4.2 Настройка рабочего места catkin

Для настройки рабочего пространства catkin на компьютере и Pi 3 следуйте инструкций [http://wiki.ros.org/catkin/Tutorials/create\_a\_workspace](http://wiki.ros.org/catkin/Tutorials/create_a_workspace). 

Если вы знакомы с ROS, то знаете, что такое рабочее пространство catkin. Все наши программы будут в нем, в пакете, который мы назовем tinman. Давайте продолжим и соберем это пакет вместе. Это займет всего несколько шагов. Начните в домашней директории:

mkdir –p catkin\_ws/src   
cd catkin\_ws/src   
catkin\_make   
source devel/setup.bash   
catkin\_create\_pkg tinman   
catkin\_make   
cd src/tinman/src   
mkdir script   
mkdir launch

Теперь структура ваших каталогов выглядит примерно так:

![](.gitbook/assets/image%20%2813%29.png)

