# Подглава 10.4 Установка OpenCV в Ubuntu Linux

Самый простой способ установить OpenCV в Ubuntu Linux - это получить пакеты Debian. На момент написания этой статьи последней версией является версия 2.4, которую можно установить с помощью следующей команды:

`$ sudo apt-get install ros-indigo-vision-opencv libopencv-dev  python-opencv` 

`$ rospack profile`

Чтобы проверить вашу установку, попробуйте следующие команды:

`$ python` 

`>>> from cv2 import cv` 

`>>> quit()`

Предполагая, что вы не получите ошибку импорта, вы должны быть готовы к работе, и вы можете перейти к следующему разделу. Если вместо этого вы получаете сообщение об ошибке: 

`ImportError: No module named cv2`

тогда либо OpenCV не установлен должным образом, либо ваш путь к Python указан неправильно. Библиотека OpenCV Python хранится в файле cv2.so. Чтобы убедиться, что он установлен, выполните команду:

`$ locate cv2.so | grep python`

Вы должны получить вывод, похожий на:

`/usr/lib/python2.7/dist-packages/cv2.so`
