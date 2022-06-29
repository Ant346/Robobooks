# Подглава 2.4.4.1 VNC

Я добавил в свой Pi 3 VNC – систему удаленного доступа к рабочему столу. С помощью неё вы можете работать с Pi 3, как будто вы подключили к нему монитор, клавиатуру и мышь. Поскольку Pi 3 физически установлен внутри робота, а робот активно передвигается, то подключить к нему периферию мы не сможем. Существуют различные версии VNC, но я выбрал RealVNC. Вам нужны сервер и клиент для VNC. Сервер – на Pi 3, в основном копирует изображение и отправляет его по Ethernet. Клиент принимает эти данные и выводит на другом компьютере. Установить сервер VNC на Pi 3 можно при помощи команды:

`sudo apt-get install realvnc-vnc-server`

Также RealVNC доступен по адресу [https://www.realvnc.com/en/raspberrypi/](https://www.realvnc.com/en/raspberrypi/). VNC чаще всего уже входит в Pi 3 Raspbian. 

После этого разберитесь с клиентской частью на управляющем устройстве. Я установил VNC на iPad. Поздравляю, теперь вы можете комфортно управлять вашим роботом.
