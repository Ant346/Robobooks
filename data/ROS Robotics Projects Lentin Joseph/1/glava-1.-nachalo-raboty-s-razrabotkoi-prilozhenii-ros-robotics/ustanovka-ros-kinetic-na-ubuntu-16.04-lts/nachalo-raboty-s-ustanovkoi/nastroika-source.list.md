# Настройка source.list

Следующим шагом является разрешение пакетов ROS с сервера репозитория ROS, называемого packages.ros.org.  Подробная информация о сервере хранилища ROS должна быть указана в source.list, который находится в / etc / apt /.

Следующая команда выполнит эту работу для ROS Kinetic, Jade и Indigo:

**`sudo sh -c 'echo "deb`**[**`http://packages.ros.org/ros/ubuntu`**](http://packages.ros.org/ros/ubuntu)**`$ (Lsb_release-sc) main "> /etc/apt/sources.list.d/ros-latest.list '`**

