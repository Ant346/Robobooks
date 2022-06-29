# Модуль 1. Основные понятия

![Kobuki](../.gitbook/assets/image%20%2831%29.png)

![](../.gitbook/assets/image%20%2811%29.png)



• Робот: **Turtlebot** **2**

Предполагаемое время для завершения: 1,5 часа.

Симулированный робот: Turtlebot 2

Что вы изучите в этом модуле?

• Как структурировать и запускать программы ROS2 \(пакеты и launch файлы\)

• Как создавать базовые программы для ROS2 \(на C ++\)

• Основные понятия ROS2: узлы, клиентские библиотеки и т.д.

![&#x420;&#x43E;&#x431;&#x43E;&#x442; Kobuki](../.gitbook/assets/image%20%2840%29.png)

## Что такое ROS2?



## Движение робота с помощью ROS2

В правом углу экрана у вас есть первый симулированный робот: робот Turtlebot 3 около большой стены.

### Как вы двигаете Turtlebot?



Поскольку ранее созданная программа ROS2 \(исполняемая\), которая позволяет вам перемещать робота с помощью клавиатуры, уже существует, давайте запустим эту программу ROS2 для управления роботом.

#### Пример 1.1



Выполнить в WebShell \# 1

```text
[ ]: source ~/.bashrc_bridge
[ ]: export ROS_MASTER_URI=http://localhost:11311
[ ]: ros2 run ros1_bridge dynamic_bridge
```



Выполнить в WebShell \# 2

```text
[ ]: source /opt/ros/crystal/setup.bash 
[ ]: ros2 run teleop_twist_keyboard teleop_twist_keyboard
```

Вывод WebShell \# 1

```text
[ ]: Control Your Turtlebot!
Moving around:
u          i           o
j          k          l
m         ,          .
q/z : increase/decrease max speeds by 10%
w/x : increase/decrease only linear speed by 10% e/c : increase/decrease only angular speed by 10% space key, k : force stop
anythin else : stop smoothly
CTRL-C to quit
```

Теперь вы можете использовать ключи, указанные в выводе WebShell, для перемещения робота. Основные ключи следующие:

![&#x41A;&#x43B;&#x44E;&#x447;&#x438; &#x434;&#x43B;&#x44F; &#x443;&#x43F;&#x440;&#x430;&#x432;&#x43B;&#x435;&#x43D;&#x438;&#x44F; &#x440;&#x43E;&#x431;&#x43E;&#x442;&#x43E;&#x43C; Kobuki](../.gitbook/assets/image%20%281%29.png)



**ros2** - это ключевое слово, используемое для всех команд ROS2. Для запуска программ у вас есть два варианта:

• Запустите программу ROS2, непосредственно запустив **исполняемый файл**.

• Запустите программу ROS2, запустив **launch файл**.

Структура команды для непосредственного запуска исполняемого файла выглядит следующим образом:

```text
[ ]: ros2 run  <package_name><executable_file>
```



Cтруктура команды для использования lauch файла структура команды будет выглядеть следующим образом:

```text
[ ]: ros2 launch  <package_name><executable_file>
```

Как видите, эта команда также имеет два параметра: первый - это имя пакета, содержащего launch файл з, а второй - имя самого launch файла \(который хранится внутри пакета\).

## ROS1 Bridge



Как вы уже знаете, ROS2 очень молод по сравнению со своим старшим братом ROS1. Из-за этого существует множество пакетов и симуляций, которые еще не доступны для ROS2. К счастью, у нас есть ROS1 Bridge, чтобы заполнить эти пробелы.

По сути, этот пакет обеспечивает сетевой мост, который обеспечивает обмен сообщениями между ROS1 и ROS2. Таким образом, мы можем использовать пакеты или симуляции, которые сделаны для ROS1, в ROS2.

В любом случае, не беспокойтесь об этом прямо сейчас. Вы узнаете больше о ROS1 Bridge в следующей главе.

## А сейчас... что такое пакет?



Все эти файлы организованы в пакете со следующей структурой:

• **папка запуска**: содержит launch файлы

• **папка src**: исходные файлы \(cpp, python\)

• **CMakeLists.txt**: список правил cmake для компиляции

• **package.xml**: информация о пакете и зависимости Каждая программа ROS, которую вы хотите выполнить, собрана в пакет. Каждая созданная вами программа ROS должна быть собрана в пакет. Пакеты являются основной системой организации программ ROS.

## А также... что такое launch файлы?



#### Пример 1.2

В **Примере 1.1** вы использовали команду **ros2 run** для запуска узла **teleop\_twist\_keyboard**. Но также вы видели, что можете запускать узлы, используя то, что мы знаем как **launch файлы**.

Но... как они работают? Давайте рассмотрим это на примере. Если мы хотим запустить узел **teleop\_twist\_keyboard** с помощью launch файла, нам нужно будет создать что-то похожее на следующий скрипт Python.

```text
[ ]: """Launch a talker and a listener."""

    from launch import LaunchDescription

    import launch_ros.actions

    def generate_launch_description():

        return LaunchDescription([

            launch_ros.actions.Node(

                package='teleop_twist_keyboard',

    node_executable='teleop_twist_keyboard', output='screen'),  
        ])
```



```text
[ ]: from launch import LaunchDescription
import launch_ros.actions
```

Далее мы определяем функцию, которая будет возвращать объект **LaunchDescription**.

```text
[ ]: def generate_launch_description():

    return LaunchDescription([

        launch_ros.actions.Node(

            package='teleop_twist_keyboard',

    node_executable='teleop_twist_keyboard', output='screen'),  
        ])
```



1. package = ‘package\_name’ \# Имя пакета, содержащего код программы ROS для выполнения

2. node\_executable = ‘cpp\_executable\_name’ \# Имя исполняемого файла cpp, который мы хотим выполнить

3. output = ‘type\_of\_output’ \# Через какой канал мы распечатаем выходные данные программы

## Создание пакета



Когда мы хотим создавать пакет, нам нужно работать в очень специфическом рабочем пространстве ROS, которое называется **ROS** **workspace**. ROS workspace - это каталог на вашем жестком диске, где должны находиться **ваши собственные пакеты ROS2**, чтобы они могли использоваться ROS2. Обычно ROS workspace каталог называется **ros2\_ws**.

#### Пример 1.3



Выполнить в WebShell \# 1

```text
[ ]: source /opt/ros/crystal/setup.bash
```

Теперь перейдем к **ros2\_ws** в вашей веб-оболочке.

Выполнить в WebShell \# 1

```text
[ ]: cd ~/ros2_ws/
     pwd
```

Вывод WebShell \# 1

```text
[ ]: user ~ $ pwd
     /home/user/ros2_ws
```

Внутри этого рабочего пространства есть каталог с именем **src**. Эта папка будет содержать все созданные пакеты. Каждый раз, когда вы хотите создать пакет, вы должны находиться в этом каталоге \(**ros2\_ws /** **src**\). Введите в webshell **cd** **src**, чтобы перейти в исходный каталог.

Выполнить в WebShell \# 1

```text
[ ]: cd src
```

Теперь вы готовы создать ваш первый пакет! Чтобы создать пакет, введите в

webshell:

Выполнить в WebShell \# 1

```text
[ ]: ros2 pkg create my_package --build-type ament_cmake --dependencies
     rclcpp
```

Это создаст внутри вашего каталога «src» новый пакет с некоторыми файлами в нем. Мы проверим это позже. Теперь давайте посмотрим, как строится эта команда:

```text
[ ]: ros2 pkg create <package_name> --build-type ament_cmake --dependencies
     <package_dependecies>
```

**package\_name** - это имя пакета, который вы хотите создать, а **package\_dependencies** - это имена других пакетов ROS, от которых зависит ваш пакет.

#### Пример 1.4

```text
[ ]: ros2 pkg list
     ros2 pkg list | grep my_package
```



![&#x412; IDE &#x441;&#x43E;&#x437;&#x434;&#x430;&#x43D; &#x43F;&#x430;&#x43A;&#x435;&#x442; my\_package](../.gitbook/assets/image%20%2812%29.png)



## Скомпилируйте пакет



```text
[ ]: colcon build --symlink-install
```

Эта команда скомпилирует всю директорию src, и ее необходимо ввести в ros2\_ws

каталог для того, чтобы работать. Это **ОБЯЗАТЕЛЬНО**.

#### **Пример 1.5**

Перейдите в каталог ros2\_ws и скомпилируйте исходную папку. Вы можете сделать это, набрав:

Выполнить в WebShell \# 1

```text
[ ]: cd ~/ros2_ws
     colcon build --symlink-install
```

Иногда \(например, в больших проектах\) вы не захотите скомпилировать все свои пакеты, а только тот, в который вы внесли изменения. Вы можете сделать это с помощью следующей команды:

```text
[ ]: colcon build --symlink-install --packages-select <package_name>
```

Эта команда будет компилировать только указанные пакеты и их зависимости.

Попробуйте скомпилировать пакет my\_package с помощью этой команды.

Выполнить в WebShell \# 1

```text
[ ]: colcon build --symlink-install --packages-select my_package
```

Когда компиляция закончится, вам нужно будет найти исходное рабочее пространство. Вы можете сделать это с помощью следующей команды:

Выполнить в WebShell \# 1

```text
[ ]: source ~/ros2_ws/install/setup.bash
```




## **Моя первая программа** **ROS**

На этом этапе у вас должен быть создан ваш первый пакет…, но теперь с этим нужно что-то делать! Давайте сделаем нашу первую программу ROS2!

#### **Пример 1.6** 

1. Создайте файл C ++, который будет выполняться в каталоге **src** в my\_package. Для этого упражнения просто скопируйте этот простой код C ++ simple.cpp. Вы можете создать его **напрямую**, щелкнув правой кнопкой мыши на IDE в каталоге src вашего пакета и выбрав New File.

![&#x421;&#x43E;&#x437;&#x434;&#x430;&#x43D;&#x438;&#x435; &#x43D;&#x43E;&#x432;&#x43E;&#x433;&#x43E; &#x444;&#x430;&#x439;&#x43B;&#x430;](../.gitbook/assets/image%20%2837%29.png)



![&#x41D;&#x435; &#x441;&#x43E;&#x445;&#x440;&#x430;&#x43D;&#x435;&#x43D;&#x43E;](../.gitbook/assets/image%20%2847%29.png)

![&#x421;&#x43E;&#x445;&#x440;&#x430;&#x43D;&#x435;&#x43D;&#x43E;](../.gitbook/assets/image%20%2841%29.png)



Выполнить в WebShell \# 1

```text
[ ]: cd ~/ros2_ws/src/my_package
     mkdir launch
```

Вы также можете создать его через IDE.



Execute in WebShell \#1

```text
[ ]: touch launch/my_package_launch_file.launch.py
     chmod +x my_package_launch_file.launch.py
```

Вы также можете создать его через IDE.

4. Заполните этот файл запуска, как мы уже видели в этом курсе {Пример 1.3}.

Окончательный запуск должен выглядеть примерно так: my\_package\_launch\_file.launch

5. Измените файл **CMakeLists.txt**, чтобы создать исполняемый файл из файла C ++, который вы только что создали.

Примечание: это то, что **требуется при работе в ROS с C ++**. Когда вы закончите это упражнение, вы узнаете об этом больше. Пока просто следуйте инструкциям ниже.

В разделе **Build** вашего файла **CMakeLists.txt** добавьте следующие строки прямо над строкой **ament\_package \(\)**.


```text
[ ]:add_executable(simple_node src/simple.cpp)
    ament_target_dependencies(simple_node rclcpp)
    install(TARGETS
        simple_node
        DESTINATION lib/${PROJECT_NAME})
    install(DIRECTORY
        launch
        DESTINATION share/${PROJECT_NAME}/
    )
```

![](../.gitbook/assets/image%20%2823%29.png)



Выполнить в WebShell \# 1

```text
[ ]: cd ~/ros2_ws;
     colcon build --symlink-install 
     source ~/ros2_ws/install/setup.bash 
```



![](../.gitbook/assets/image%20%2839%29.png)



7. Наконец, выполните команду roslaunch в WebShell, чтобы запустить вашу программу.

Выполнить в WebShell \# 1

```text
ros2 launch my_package my_package_launch_file.launch.py 
```

#### 

Вы должны увидеть цитату Леи среди результатов команды roslaunch. 

Выполнить в WebShell \# 1

```text
[ ]: user:~/ros2_ws$ ros2 launch my_package 
     my_package_launch_file.launch.py
     [INFO] [launch]: process[simple_node-1]: started with pid [29595] 
     [INFO] [ObiWan]: Help me Obi-Wan Kenobi, you're my only hope
     [INFO] [launch]: process[simple_node-1]: process has finished cleanly 

```

### 

```text
[ ]: #include "rclcpp/rclcpp.hpp" 
     int main(int argc, char * argv[])
     {
rclcpp::init(argc, argv);
auto node = rclcpp::Node::make_shared("ObiWan"); 
RCLCPP_INFO(node->get_logger(), "Help me Obi-Wan Kenobi, you're my only hope"); 
       rclcpp::shutdown();
return 0; 
} 
```



```text
[]: // Здесь мы включаем все заголовки, необходимые для использования наиболее распространенных открытых частей системы ROS
// Здесь мы используем клиентскую библиотеку rclcpp, которая предоставляет API C ++ для взаимодействия с ROS
// Всегда, когда мы создаем новый файл C ++, нам нужно добавить это:
#include "rclcpp / rclcpp.hpp"
      // Запускаем основную программу на C ++
      int main (int argc, char * argv [])
      {
        // Инициируем клиентскую библиотеку rclcpp
rclcpp :: init (argc, argv);
// Мы инициируем узел ROS под названием ObiWan
auto node = rclcpp :: Node :: make_shared ("ObiWan");
// Это то же самое, что и печать в ROS
RCLCPP_INFO (node-> get_logger (), «Help me Obi-Wan Kenobi, you're my only hope»);
// Мы закрываем клиентскую библиотеку 
rclcpp rclcpp :: shutdown ();
// Мы заканчиваем нашу программу
return 0;
}
```



### **Launch File {1.1-l}: my\_package\_launch\_file.launch.py**

В вашем my\_package\_launch\_file.launch должно быть что-то похожее: 

**Примечание.** Помните, что в приведенном ниже примере имя исполняемого файла C ++ в атрибуте node\_executable это simple\_node. Если вы назвали свой исполняемый файл C ++ с другим именем, на этом месте будет что-то другое.

```text
[ ]: """Launch a talker and a listener.""" 
    from launch import LaunchDescription 
    import launch_ros.actions 
    def generate_launch_description(): 
        return LaunchDescription([ 
            launch_ros.actions.Node(
                package='my_package', node_executable='simple_node',output='screen'), 
        ])

```

### 

При программировании на C ++ необходимо будет создавать двоичные файлы \(исполняемые файлы\) ваших программ, чтобы иметь возможность их выполнять. Для этого вам необходимо изменить файл **CMakeLists.txt** вашего пакета, чтобы указать, что вы хотите создать исполняемый файл вашего C ++.

Для этого вам нужно добавить несколько строк в ваш файл **CMakeLists.txt**. На самом деле эти строки уже есть в файле, но они закомментированы. Вы также можете найти их и раскомментировать. Чтобы бы вы не выбрали.

В предыдущем упражнении у вас были следующие строки:

```text
[ ]:add_executable(simple_node src/simple.cpp) 
    ament_target_dependencies(simple_node rclcpp) 
    install(TARGETS 
    simple_node 
    DESTINATION lib/${PROJECT_NAME} ) 
    # Install launch files. 
    install(DIRECTORY
      launch
    DESTINATION share/${PROJECT_NAME}/ 
    ) 

```

Но… что именно делают эти строки кода? Ну, в целом они делают следующее:

```text
[ ]: add_executable(simple_node src/simple.cpp)
```



```text
[ ]: ament_target_dependencies(simple_node rclcpp)
```

Эта строка добавляет все целевые зависимости исполняемого файла.

```text
[ ]:install(TARGETS 
    simple_node 
    DESTINATION lib/${PROJECT_NAME} 
)
```



```text
[ ]:install(DIRECTORY
    launch
    DESTINATION share/${PROJECT_NAME}/ 
)
```



## ROS узлы \(Nodes\)

Вы инициировали узел в предыдущем коде, но... что это за узел? Узлы \(Nodes\) ROS - это в основном программы, созданные в ROS. Чтобы увидеть, какие узлы на самом деле работают на компьютере, можно использовать команду ROS:

```text
[ ]: ros2 node list 
```

#### **Пример 1.7**

Введите эту команду в новой оболочке и найдите только что инициализированный узел \(ObiWan\).   


Выполнить в WebShell \# 1

```text
[ ]: ros2 node list
```

Не можете найти это? Мы зна,ем что ты не можете. Это происходит потому, что узел завершается, когда заканчивается программа C ++. Давайте изменим это.

Обновите файл C ++ simple.cpp следующим кодом:

### 

```text
[]: #include "rclcpp / rclcpp.hpp"
      int main (int argc, char * argv [])
      {
            rclcpp :: init (argc, argv);
            
            auto node = rclcpp :: Node :: make_shared ("ObiWan"); // Создаем объект Rate 2 Гц 
            
            rclcpp :: WallRate loop_rate (2);
            
            // Бесконечный цикл до нажатия Ctrl + C
            while (rclcpp :: ok ()) {
            
            RCLCPP_INFO (node-> get_logger (), «Help me Obi-Wan Kenobi, you're my only hope »);
rclcpp :: spin_some (node);

      // Бездействуем необходимое время для поддержания фиксированной скорости выше loop_rate.sleep ();
            } 
            rclcpp :: shutdown (); 
            return 0;
      }
// Эта программа создает бесконечный цикл, который повторяется 2 раза в секунду (2 Гц), пока не будет нажато Ctrl + C.
```



Выполнить в WebShell \# 1

```text
[ ]: ros2 launch my_package my_package_launch_file.launch.py 
```

Теперь попробуйте еще раз в другой WebShell:

Выполнить в WebShell \#2

```text
[ ]: source /opt/ros/crystal/setup.bash 
[ ]: ros2 node list
```



Выполнить в WebShell \# 1

```text
[ ]: user:~$ ros2 node list /launch_ros/ObiWan
```

Чтобы увидеть информацию о нашем узле, мы можем использовать следующую команду:

```text
[ ]: ros2 node info /ObiWan
```

Чтобы увидеть информацию о нашем узле, мы можем использовать следующую команду: 

Выполнить в WebShell \# 1

```text
[ ]: ros2 node info /ObiWan
```

Вывод WebShell \#1

```text
[ ]: user:~$ ros2 node info /ObiWan 
     /ObiWan 
      Subscribers:
       /parameter_events: rcl_interfaces/ParameterEvent 
      Publishers:
       /parameter_events: rcl_interfaces/ParameterEvent 
      Services:
       /ObiWan/describe_parameters: rcl_interfaces/DescribeParameters /ObiWan/get_parameter_types: rcl_interfaces/GetParameterTypes 
       /ObiWan/get_parameters: rcl_interfaces/GetParameters 
       /ObiWan/list_parameters: rcl_interfaces/ListParameters
       /ObiWan/set_parameters: rcl_interfaces/SetParameters
       /ObiWan/set_parameters_atomically: 
     rcl_interfaces/SetParametersAtomically 

```



## 

В предыдущем упражнении вы использовали клиентскую библиотеку **rclcpp**. Но что это такое? По сути, клиентские библиотеки ROS позволяют узлам, написанным на разных языках программирования, обмениваться данными. Существует базовая клиентская библиотека ROS \(RCL\), которая реализует общие функциональные возможности, необходимые для API ROS различных языков. Благодаря этому специфичные для языка клиентские библиотеки проще в написании и имеют более согласованное поведение.

Следующие клиентские библиотеки в настоящее время поддерживаются ROS2:

• **rclcpp** = C ++ клиентская библиотека

• **rclpy** = Python клиентская библиотека

Кроме того, сообщество ROS разработало другие клиентские библиотеки. Вы можете проверить следующую статья для более подробной информации: [https://index.ros.org/doc/ros2/ROS-2-Client-Libraries/](https://index.ros.org/doc/ros2/ROS-2-Client-Libraries/)

## Переменные среды

ROS использует набор системных переменных среды Linux для правильной работы. Вы можете проверить эти переменные, набрав:

```text
[]: export | grep ROS
```



```text
[ ]: user:~$ export | grep ROS
     declare -x ROS_DISTRO="crystal"
     declare -x ROS_IP="10.8.0.1"
     declare -x ROS_MASTER_URI="http://10.8.0.1:11311" 
     declare -x ROS_PYTHON_VERSION="3" 
     declare -x ROS_VERSION="2"
```



```text
[ ]: ROS_MASTER_URI -> Contains the url where the ROS Core is being 
     executed. Usually, your own computer (localhost).
     ROS_DISTRO -> Contains the ROS distribution that you are currently 
     using. 
```



**ПРИМЕЧАНИЕ 2:** На платформе, которую вы используете для этого курса, мы создали псевдоним для отображения переменных среды ROS. Этот псевдоним это **rosenv**. Набрав это в webshell, вы получите список переменных среды ROS. Важно, чтобы вы знали, что это **не официальная команда** **ROS**, поэтому вы можете использовать ее только при работе на этой платформе.

## А сейчас... что такое ROS2?

ROS2 - это, по сути, фреймворк, который позволяет нам делать все то, что мы показали вам в этой главе. Он обеспечивает базу для управления всеми этими процессами и связи между ними…, и многое, многое другое!! В этом уроке вы познакомились с ROS2, основными понятиями. ROS2 - чрезвычайно мощный инструмент. Если вы внимательно изучите наши курсы, вы узнаете намного больше о ROS2 и вы сможете делать практически вашими роботами практически все!
