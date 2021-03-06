# Мастеркласс Internet of Things (IoT)
Связываем простые устройства с Интернетом.

### Описание
На воркшопе мы познакомимся с популярным микроконтроллером ESP8266 и технологией Google Firebase. ESP8266 позволяет выполнять простые программы и соединяться с Интернетом через встроенный Wi-Fi. Данное сочетание делает плату отличным стартом для тех, кто создает продукты для сферы Интернет Вещей. Firebase - гибкий инструмент для мобильных и веб-приложенией. Применение: Firebase можно  использовать не только в Интернете или мобильных устройствах, но и в “подключенных гаджетах”.
В ходе воркшопа мы сделаем первые шаги с ESP8266 - соединим необходимые проводки, светодиоды и кнопки, подключим к компьютеру, настроим среду разработки Arduino IDE. Затем напишем программу для ESP8266 и подключим к облачному сервису Firebase. В результате, вы получите двустороннюю связь между устройством и мобильным (или веб) приложением.

Вам потребуется:
* Наш набор
* Ноутбук
* Вайфай и подключение к Интернету

Время работы - 2 часа, размер комадны - 1-3 человека
### Цель
На Воркшопе мы соберем одну схемку - кнопка, красная или зеленая лампочка, модуль esp8266. Исходный код уже написан, необходимо будет скачать его с гитхаба, открыть в Arduino IDE и модифицировать 4 строчки. 
## Первый этап. [Настройка программного обеспечения](https://github.com/firebase/firebase-arduino/tree/master/examples/FirebaseRoom_ESP8266#software-setup)

1. Скачать среду новую разработки [Arduino](http://www.arduino.cc/en/main/software), примерно 100Мб (не младше ```1.6.4```) 
2. Установить ее и зайти в ```Preferences```
3. Вбить следующую строчку ```http://arduino.esp8266.com/stable/package_esp8266com_index.json``` в поле ```Additional Board Manager URLs```
4. Открыть ```Boards manager``` из меню ```Tools > Board```
5. В окне найти ```esp8266``` и установить (надо скачать порядка 150Мб). 
6. После этого вы можете программировать платы, основанные на чипе esp8266. Более подробно об ПО для esp8266 можно почитать [тут](https://github.com/esp8266/Arduino)
7.  Установить драйвер для преобразователя USB-UART. Для Windows ([32-bit](http://www.ifamilysoftware.com/Drivers/PL-2303_Driver_Installer.exe), [64-bit](http://www.ifamilysoftware.com/Drivers/PL2303_64bit_Installer.exe)), для [Mac](https://github.com/changux/pl2303osx/raw/master/PL2303_Serial-USB_on_OSX_Lion.pkg), для Linux драйвера уже включены в известные репозитории (Ubuntu, Debian и др.).
8. Скачать [zip-архив](https://github.com/firebase/firebase-arduino/archive/master.zip) репозитория с драйвером Firebase для Arduino 
9. Удалить папку ```thing``` из директории ```/firebase-arduino-master/src/``` этого архива (из-за нее не компилируются программы, она нам не нужна сегодня)
10. В Arduino IDE установить драйвер Firebase через ```Sketch > Include Library > Add .ZIP Library...```

## Второй этап. Сборка схемы.

![Схема для FirebaseRoom_ESP8266](/firebase ESP workshop_bb.png "Схема для FirebaseRoom_ESP8266")

1. Взять набор
 * Модуль ESP8266
 * Макетная плата
 * Последовательный порт USB-UART
 * Набор проводков
 * Светодиод, кнопка, резистор
 * Провод USB
2. Собрать схему под рисунку
3. Подключить USB-UART к компьютеру. 

## Третий этап. [Настройка Firebase](https://github.com/firebase/firebase-arduino/tree/master/examples/FirebaseRoom_ESP8266#configuration)
1. Открыть пример ```File > Examples > FirebaseArduino > FirebaseRoom_ESP8266```
2. В примере ```FirebaseRoom_ESP8266``` заменить поля ```WIFI_SSID``` и ```WIFI_PASSWORD```для подключения WiFi.  
3. Открыть [консоль Firebase](https://firebase.google.com/console/) и создать новую базу данных (```Database```) 
4. Скопировать URL-адрес базы данных (без https:// и /) и заменить в программе ```FIREBASE_HOST```
5. Найти "секрет" базы данных (```⚙ > Project Settings > Database > Database secrets```) и заменить в программе ```FIREBASE_AUTH```
6. Заменить ```pinMode(buttonPin, INPUT)``` на ```pinMode(buttonPin, INPUT_PULLUP)```
7. Выбрать плату ```Generic ESP8266 Module``` в ```Board > ESP8266 Modules```
8. Выбрать последовательный порт ```Tools > Port``` (```Port > /dev/tty...``` в Linux, ```/dev/cu.PL2303...``` в Mac, ```COM...``` в Windows)
9. Установить скорость ```Upload Speed > 115200```
10. Залить программу через ```Sketch > Upload```

## Четвертый этап. [Результат](https://github.com/firebase/firebase-arduino/tree/master/examples/FirebaseRoom_ESP8266#play)
1. Открыть консоль Firebase, отобразить данные (Data)
2. Изменить ```redlight``` с ```0``` на ```1```
3. Убедиться, что лампочка загорелась
4. Нажать кнопку на макетной плате
5. Убедиться, что ```pushbutton``` изменился с ```0``` на ```1```

## Это все, мы достигли результата. 
Призываем модифицировать код, добавить новые сенсоры и собрать свой проект на ESP-Firebase
