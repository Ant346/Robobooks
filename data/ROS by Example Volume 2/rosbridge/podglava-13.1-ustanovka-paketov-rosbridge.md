# Подглава 13.1 Установка пакетов rosbridge

Чтобы установить rosbridge\_suite и вспомогательные пакеты, выполните следующие команды:

`$ sudo apt-get update  
$ sudo apt-get install ros-indigo-rosbridge-suite  ros-indigo- robot-pose-publisher ros-indigo-tf2-web-republisher $ rospack profile`

Нам также понадобится несколько пакетов JavaScript, которые обычно не распространяются как пакеты Debian. Эти пакеты уже включены в каталог rbx2\_gui / js, но если по какой-то причине вам необходимо переустановить их, вы можете запустить скрипт install-jspackages.sh следующим образом:

`$ roscd rbx2_gui/scripts   
$ sh install-js-packages.sh`

Скрипт загружает следующие пакеты Javascript:   
[http://cdn.robotwebtools.org/roslibjs/r5/roslib.min.js   
](http://cdn.robotwebtools.org/roslibjs/r5/roslib.min.js)[http://cdn.robotwebtools.org/mjpegcanvasjs/current/mjpegcanvas.min.js   
](http://cdn.robotwebtools.org/mjpegcanvasjs/current/mjpegcanvas.min.js)[http://cdn.robotwebtools.org/EventEmitter2/0.4.11/eventemitter2.min.js   
](http://cdn.robotwebtools.org/EventEmitter2/0.4.11/eventemitter2.min.js)[http://cdn.robotwebtools.org/EaselJS/0.6.0/easeljs.min.js   
](http://cdn.robotwebtools.org/EaselJS/0.6.0/easeljs.min.js)[http://cdn.robotwebtools.org/ros2djs/r2/ros2d.min.js   
](http://cdn.robotwebtools.org/ros2djs/r2/ros2d.min.js)[http://cdn.robotwebtools.org/ros3djs/current/ros3d.min.js   
](http://cdn.robotwebtools.org/ros3djs/current/ros3d.min.js)[http://threejs.org/build/three.min.js   
](http://threejs.org/build/three.min.js)[http://code.jquery.com/jquery1.10.2.min.js   
](http://code.jquery.com/jquery1.10.2.min.js)http://d3lp1msu2r81bx.cloudfront.net/kjs/js/lib/kineticv5.0.1.min.js

 Обратите внимание, что один дополнительный пакет Javascript, найденный по адресу [http://cdn.robotwebtools.org/nav2djs/current/nav2d.js](http://cdn.robotwebtools.org/nav2djs/current/nav2d.js) , необходимо настроить, чтобы исправить ошибку смещения при использовании карты для навигации. Версия, включенная в rbx2\_gui / js, была настроена для работы с тестовой картой, найденной в rbx2\_nav / maps / test\_map.yaml.  

