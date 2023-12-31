# KP3S_Marlin_2.1.2.1
Прошивка Marlin 2.1.2.1 с Input Shaping для 3D-принтера Kingroon KP3S

Добро пожаловать в репозитарий!
Здесь Вы найдете файлы, необходимые для сборки прошивки Marlin версии 2.1.2.1 для принтера Kingroon KP3S 3.0. Так случилось, что после Klipper-а мне пришлось вернуть обратно прошивку Marlin в связи с продажей принтера. Увы мне не удалось найти прошивку Marlin с Input Shaping в открытом виде, поэтому пришлось собрать прошивку самому.

Особенности прошивки:
- За основу прошивки взят стандартный Marlin 2.1.2.1, который был взят с официального репозитария https://github.com/MarlinFirmware/Marlin/releases. Вам также для сборки прошивки он понадобится.
- Максимальная скорость 250 мм/с, ускорения 4000 мм/с^2 (взято с прошивки Klipper, принтер не рассыпался, живой. Всегда можно уменьшить, если страшно)
- Штатная голова принтера.
- Для уменьшения шума в простое, кулер хотенда подключен к разъему второго экструдера, в прошивке настроено отключение кулера при температуре хотенда ниже 50 градусов. Ничего страшного не произойдет, если вы не переподключите кулер, главное не перепутать полярность при переподключении.
- Датчик уровня BLTouch, крепление BLTouch справа (модель https://drive.google.com/drive/folders/1eDY91nCIgY-3owwBqj1e4Szzl0qyVd9j, с официального руководства Kingroon), карта стола по 16 точкам (а оно точно надо?). датчик работает как концевик, стандартный концевик следует отключить на плате и вместо него подключить контакты датчика. 
- Возможность калибровки PID экструдера и стола
- Включенный Linear Advance (у меня по калибровкам с K3D вышло 0.08)
- Включенный Input Shaping и возможность редактирования частот шейпера ZV из меню (сам взял коэфициенты шейпера MZV с прошивки Klipper, поэтому **ИХ НУЖНО КАЛИБРОВАТЬ!**)
- Штатный экран повернут на 90 градусов, использовалась модель https://www.thingiverse.com/thing:5319887 (можно не поворачивать, но полгода назад Marlin не умел)
- Используется английский язык интерфейса. Если кто найдет способ завести русский или украинский язык без кракозябр вместо букв, то буду очень признателен, хотя язык интерфейса это наименее важная вещь в функционировании сложных технических устройств.
- В моем экземпляре принтера с чипом GD303... увы не работала SD-карта. После долгого поиска всё-таки удалось выяснить причину, спасибо https://github.com/dmgualb/KP5L/tree/main, удалось выяснить что проблема в файле **Marlin\src\HAL\STM32\tft\tft_fsmc.cpp**. Советую попробовать сначала не заменять этот файл, а попробовать собрать прошивку и проверить без него, вдруг повезет.
- Для особо ленивых в папке **bin** находится готовый файл прошивки. Манипуляции с прошлого абзаца уже заранее были проделаны. Закидываем на флешку, подключаем к принтеру, и перезагружаем принтер (рекомендуют еще подождать 30 секунд после отключения, но я не ждал, ничего страшного не случилось). 

В ЛЮБОМ СЛУЧАЕ ПРИ ИСПОЛЬЗОВАНИИ ГОТОВОГО ФАЙЛА ПРОШИВКИ ИЛИ СБОРКИ ПРОШИВКИ САМОСТОЯТЕЛЬНО НА ОСНОВЕ ИСХОДНЫХ КОДОВ С ЭТОГО РЕПОЗИТАРИЯ АВТОР НЕ НЕСЁТ НИКАКОЙ ОТВЕТСТВЕННОСТИ ЗА ПОВРЕЖДЕНИЕ ОБОРУДОВАНИЯ, ВЫ ДЕЛАЕТЕ ВСЕ НА СВОЙ СТРАХ И РИСК, ПОДУМАЙТЕ ПРЕЖДЕ, ЧЕМ ПЕРЕПРОШИВАТЬ ПРИНТЕР!

Что сделать после прошивки (хотя все и так знают):
1. Проверить работу флешки, при необходимости пересобрать прошивку (если флешка не работает, то при попытке печати gcode ничего не будет происходить)
2. Проверить движение по осям и парковку домой
3. Откалибровать Z-Offset. 
4. Откалибровать PID экструдера и PID стола, заодно можно узнать греется ли стол и экструдер. При достижении экструдером 50 градусов и выше должен заработать кулер хотенда.
5. Снять карту стола, посмотреть что щуп датчика везде касается стола, а не зажимов стола например
6. Провести тестовую печать
7. Откалибровать Linear Advance
8. Откалибровать Input Shaper (автор не успел откалиброваться, принтер был продан)
9. ... Ну и так далее

Спасибо! Всем добра!
