# Создание Tarkov сервера Dayz Standalone | Expansion | Realistic Modifications | Карта DayZone
## _Создание Локального Сервера_

Для создания сервера нам понадобится скачать с Библиотеки Steam во вкладке `"Инструменты"` DayZServer. После установки заходим в папку через Свойства и расположение Локальных файлов. Наблюдаем небольшое количество Папок и Файлов. Создаем новую Папку и называем ее `profiles`. Самого файла старта сервера нет, нужно его создать. Создаем текстовый документ, копируем текст ниже и вставляем.
![explorer_KPr6njCBZ6](https://github.com/user-attachments/assets/ee5c36aa-6f17-4999-bfea-4c6764f33025)
## Start.bat
Для запуска нашего сервера, потребуется создать `.bat` файл. 
Создаем текстовый документ, копируем текст ниже и вставляем.
```sh
@echo off
:start
::Server name
set serverName=MyServer
::Server files location
set serverLocation="C:\Program Files (x86)\Steam\steamapps\common\DayZServer"
::Server Port
set serverPort=2302
::Server config
set serverConfig=serverDZ.cfg
::Logical CPU cores to use (Equal or less than available)
set serverCPU=2
::Sets title for terminal (DONT edit)
title %serverName% batch
::DayZServer location (DONT edit)
cd "%serverLocation%"
echo (%time%) %serverName% started.
::Launch parameters (edit end: -config=|-port=|-profiles=|-doLogs|-adminLog|-netLog|-freezeCheck|-filePatching|-BEpath=|-cpuCount=)
start "DayZ Server" /min "DayZServer_x64.exe" -config=%serverConfig% -port=%serverPort% -cpuCount=%serverCPU% -dologs -adminlog -netlog -freezecheck "-BEpath=C:\Program Files (x86)\Steam\steamapps\common\DayZServer\battleye" "-profiles=C:\Program Files (x86)\Steam\steamapps\common\DayZServer\profiles" "-mod=" "-servermod="
::Time in seconds before kill server process (14400 = 4 hours)
timeout 14390
taskkill /im DayZServer_x64.exe /F
::Time in seconds to wait before..
timeout 10
::Go back to the top and repeat the whole cycle again
goto start
```
В строчке `-BEpath=` указать месторасположение античита с папки сервера и указываем папку в строке `-profiles` с расположением этой папки на DayZServer.
Теперь меняем разрешение текстового файла с `".txt" на ".bat".` Этот батник можно назвать любым именем.
## Как зайти на свой сервер
После запуска сервера откроется командная строка с отсчетом секунд до Рестарта и Консоль.
Открываем лаунчер DayZ, разворачиваем на весь экран, переходим во вкладку слева "Серверы" и тут находим `ЛВС`, где и будет возможность подключиться к серверу.

Чтобы отключить сервер нужно закрыть консоли.
ОК, хорошо, сервер запустился, персонаж появился, но просто ванильный DayZ - скучно.
Давайте я расскажу про установку модов, начнём с простейшего.
## Как устанавливать модификации
Скачиваем мод [@CF](https://steamcommunity.com/sharedfiles/filedetails/?id=1559212036) и  [@VPPAdminTools](https://steamcommunity.com/sharedfiles/filedetails/?id=1828439124). Заходим в лаунчер, справа от мода будет стрелочка, нажимаем ее, открывается дополнительная информация о моде, снизу справа нажимаем на три точки и на "скопировать в папку", указываем папку с DayZSever. Таким образом копируем моды в папку с сервером. После этого открываем каждый мод, заходим в папку `"Keys"` и копируем содержащийся в нем файл в папку `"Keys"`, но уже в папке DayZServer. Делаем это с каждым модом.
Затем начинаем редактировать стартовый батник запуска сервера, а именно в длинной строчке находим `"-mod="`. Сюда после знака `"="` вставляем `БЕЗ Пробелов` название модов, должно получиться `"-mod=@CF;@VPPAdminTools"`.

Прошу заметить, что названия модов разделяются только знаком `";"` и только им, не пробелом, не двоеточием, ничем другим.
И так, моды установлены, ключи прописаны, в Start.bat всё прописано. Отлично, теперь запускаем сервер. После полной прогрузки консоли сервер закрываем.
## Настройка VPPAdminTools
Отправляемся в папку `"Profiles"`, где видим появление новой папки `"VPPAdminTools"`. Отправляемся по пути. Открываем этот текстовый файл, удаляем все и в него вставляем свой Steam64ID. Таким образом мы обозначаем моду, что такой `ID` имеет доступ к Админ-панели.
```sh
DayZServer\profiles\VPPAdminTools\Permissions\SuperAdmins
```
Открываем `"credentials"`, сюда вписываем пароль от Админ панели.
```sh
DayZServer\profiles\VPPAdminTools\Permissions
```

Готово, мод установлен, админка прописана. Запускаем сервер, заходим. Сразу лезем в настройки привязки клавиш, заходим во вкладку `"VPP"` и настраиваем на удобные вам клавиши.
## Установка модификаций
- Из необходимых модификаций нам потребуется [@Dabs Framework](https://steamcommunity.com/workshop/filedetails/?id=2545327648)
- Из необходимых модификаций нам потребуется [@DayZ Editor Loader](https://steamcommunity.com/workshop/filedetails/?id=2276010135)

В Файле `Start.bat`, получится примерно так:
```sh
-mod=@CF;@VPPAdminTools;@Dabs Framework;@DayZ Editor Loader
```
Все эти модификации, устанавливаем точно так же, как и @CF, @VPPAdminTools.
Эти модификации пригодятся нам для дальнейшей работы.
## Установка карты DayZone
- Из необходимых модификаций нам потребуется [@STALKER: DayZone | Map Public](https://steamcommunity.com/sharedfiles/filedetails/?id=2469798930)

В Файл `Start.bat` мы добавляем карту. Получится примерно так:
```sh
-mod=@CF;@VPPAdminTools;@Dabs Framework;@DayZ Editor Loader;@STALKER- DayZone - Map Public
```
## Установка миссии DayZone | dayz.dz_map 
Переходим по следующему пути:
```sh
DayZServer\mpmissions
```
Переименовываем папку dayzOffline.chernarusplus в dayz.dz_map. Возвращаемся в корень папки сервера, ищем файл под названием `serverDZ.cfg.` Листаем до `41` строки, и так же заменяем название миссии на `dayz.dz_map`.
![image](https://github.com/user-attachments/assets/4e35906e-56ed-413e-8012-cd6654f71165)
С установкой карты и миссии мы закончили, теперь необходимо запустить сервер и дождаться полной загрузки `консоли`, после чего можете проверить, действительно ли нужная вам карта запустилась.
![image](https://github.com/user-attachments/assets/7b344aef-d1dd-47d0-821a-3395effd091a)
## Настройка спавна игроков
Переходим по следующему пути:
```sh
DayZServer\mpmissions\dayz.dz_map
```
1) Создаем папку с названием `"CustomSpawnPlayerConfig"`
2) Перекидываем в эту папку файлы, указанные ниже (Распаковать из Архива)
- Скачать Архив [Тык-Тык](https://disk.yandex.ru/d/OU_LdTG-42tP0w)

Переходим по следующему пути:
```sh
DayZServer\mpmissions\dayz.dz_map
```
Тут находим файл `init.c`, добавляем следующие данные в `1` строку
```sh
#include "$CurrentDir:mpmissions\dayz.dz_map\CustomSpawnPlayerConfig\init_mod.c"
```
Выглядит это следующим образом:
![image](https://github.com/user-attachments/assets/dbae23e6-ab45-47fe-a48d-45ee9a7f2ed6)

Переходим по следующему пути:
```sh
DayZServer\profiles
```
Тут нам нужно создать текстовый файл под названием `CustomSpawnPlayerConfig`, в нем мы и будем прописывать наших игроков.
Предлагаю создать персональный сет и точку спавна для `Администрации`, сделаем мы это следующим образом:

Открываем и правим файл `Sets.c`, На строке `11` разберём с вами ячейку `case 1`. Как мы видим, данная ячейка содержит в себе класснеймы одежды (Набор Администрации). 
На строке `13` мы видим строчку `My_Custom_Spawn_Parameters.RemoveAllItems(player);`, Данная строка, удаляет все `Ванильные` предметы и одежду, которые успели заспавниться на игроке. После удаления всех предметов игрока нужно одеть, согреть, накормить и спать уложить ✨  Приступим к примеру:
```sh
			case 1: //Сет Админов (Сет с номером 1)
			{
				My_Custom_Spawn_Parameters.RemoveAllItems(player); //Удалили всю одежду
				itemCreated = player.GetInventory().CreateInInventory("BeanieHat_Beige");//Шапочку накинули
				itemCreated = player.GetInventory().CreateInInventory("CanvasPants_Beige");//Штаны натянули
				itemCreated = player.GetInventory().CreateInInventory("HikingJacket_Black");//Куртку накинули
				itemCreated = player.GetInventory().CreateInInventory("Sneakers_Black");//Ножки согрели
				itemCreated = player.GetInventory().CreateInInventory("SodaCan_Cola");//Напоили
				itemCreated = player.GetInventory().CreateInInventory("Pumpkin");//Накормили
				break;
			}
```
Сохраняем наши изменения, переходим в папку `profiles`, и открываем ранее созданный нами файл `CustomSpawnPlayerConfig`.
Теперь нам нужно прописать игрока на данный `case 1`. Делаем это так:
```sh
76561198141889254|SurvivorM_Oliver|1|12955.091797 16.115206 7993.588379
```
`Памятка:`
```sh
UID|Skin_player|sets_numbers|points_spawns
Steam_id_64|Скин персонажа|Указываем номер case|Позиция спавна
```
Теперь осталось прописать `Жмыхов`, со своей позицией и рандомной одеждой. Открываем и правим файл `Sets.c`, На строке `61` мы видим позицию `284.188721 146.691284 2475.827881`, нам нужно поменять её на свою. Заходим на свой сервер, запуская файл `Start.bat`, телепортируемся на место где хотим видеть спавн `Жмыхов`, смотрим в небо и нажимаем английскую букву `P`. В вашем буфере обмена появится информация, содержащая позицию персонажа, вставляем её в любое удобное для вас место, вырезаем и меняем позицию.

`Буфер обмена будет выглядить так:`
```sh
Position: <4937.222168, 70.421173, 3030.905029> //Не брать эти цифры, показаны для примера!!!
Orientation: <-167.945129, 0.000000, -0.000000>
Config-Type: SurvivorM_Niki
```
![image](https://github.com/user-attachments/assets/26f007ed-be3b-47e2-91ae-75e0b26b60fe)
По такому же принципу мы одеваем `Жмыхов`, начиная с `69` строки.
На этом всё, мы научились прописывать игроков!
[Подробная Информация](https://s-platoon.ru/topic/7539-personalnyy-skin-tochka-spavna-i-set-s-lutom-pri-respavne-startovyy-lut-dlya-vseh/)
`P.s - Отдельное спасибо Автору 123new`

 `Примечание:`
```sh
- Если вы используете другую Карту, в файле init_mod.c необходимо изменить путь до миссии в первых двух строчках
- Указание позиций спавна ставится без `,`
```
## Настройка серверного мода (Не Клиент)

Переходим по следующему пути:
```sh
DayZServer
```
Установка серверной модификации от клиент-серверной не отличается ничем, как правило, кроме того, что на стороне клиента (игрока) она не требуется. Т.е. игроку не нужно предпринимать никаких действий для входа на сервер с такой установленной модификацией! А вот на стороне сервера модификация ставится.

Создаём папку, под названием `@Servermod`, заходим в неё и тут же создаем папку `Addons`.
![image](https://github.com/user-attachments/assets/f7841415-6f16-497a-a181-a2e008f5ceec)
- Из необходимых модификаций нам потребуется [@Armband Protection (RELIFE)](https://steamcommunity.com/sharedfiles/filedetails/?id=2871588037)

Скачиваем  `Armband Protection`, копируем файл из мода в наш Серверный `@Servermod` в папку `Addons`.
![image](https://github.com/user-attachments/assets/ab6acdc7-5ce8-41c4-926f-86407566a173)
`Памятка:`
```sh
- Перечисления класснеймов идут через `,`
```
После чего, в папке `profiles` будет создана папка `RELIFE`, в ней мы и найдём файл конфигурации.
```sh
{
  "HiddenClothes": [
    {
      "ItemType": "Класснейм_Повязки"
    }, //Должна стоять `Запятая`, так как идёт перечисление класснеймов
    {
      "ItemType": "Класснейм_Повязки_2"
    }, //Должна стоять `Запятая`, так как идёт перечисление класснеймов    
    {
      "ItemType": "Класснейм_Повязки_3"
    } //Перечисление закончилось, `Запятой` быть не должно
  ]
}
```
`Примечание:`
```sh
- Если на игроке будут надеты следующие вещи: Класснейм_Повязки, Класснейм_Повязки_2, его перестанут атаковать
Зомби/Мутанты, в основном это делается для RP серверов, для таких группировок как Монолит и Грех.
- Удалить все подсказки после знаков //
```
## Настройка SVisual
![image](https://github.com/user-attachments/assets/6b2f334f-98a1-4d34-ba1f-6d949df6d88a)
```sh
{
  "ddofIntensity": {
    "constrain": true,
    "message": "#STR_SUDE_LAYOUT_OPTIONS_CONSTRAINED",
    "min": 0.3,
    "max": 0.3
  },
  "ddofEnabledIn3PP": {
    "constrain": true,
    "message": "#STR_SUDE_LAYOUT_OPTIONS_CONSTRAINED",
    "value": true
  },
  "ddofEnabledInVehicle": {
    "constrain": true,
    "message": "#STR_SUDE_LAYOUT_OPTIONS_CONSTRAINED",
    "value": false
  },
  "headbobIntensity": {
    "constrain": true,
    "message": "#STR_SUDE_LAYOUT_OPTIONS_CONSTRAINED",
    "min": 2,
    "max": 2
  },
  "headbobEnabledIn3PP": {
    "constrain": true,
    "message": "#STR_SUDE_LAYOUT_OPTIONS_CONSTRAINED",
    "value": false
  },
  "motionBlurIntensity": {
    "constrain": true,
    "message": "#STR_SUDE_LAYOUT_OPTIONS_CONSTRAINED",
    "min": 0.03,
    "max": 0.03
  },
  "bloomIntensity": {
    "constrain": true,
    "message": "#STR_SUDE_LAYOUT_OPTIONS_CONSTRAINED",
    "min": 0,
    "max": 0
  },
  "headLeanAngle": {
    "constrain": true,
    "message": "#STR_SUDE_LAYOUT_OPTIONS_CONSTRAINED",
    "min": 25,
    "max": 25
  }
}
```
## Настройка SGunPlay (Реалистичная стрельба)
![image](https://github.com/user-attachments/assets/4f5d25c6-cf75-47e5-a3bd-5c3dd7e70d63)
```sh
{
  "adsFOVMultiplier": {
    "constrain": true,
    "message": "#STR_SUDE_LAYOUT_OPTIONS_CONSTRAINED",
    "min": 0.4,
    "max": 0.4
  },
  "adsFOVMagnOpticsMultiplier": {
    "constrain": true,
    "message": "#STR_SUDE_LAYOUT_OPTIONS_CONSTRAINED",
    "min": 0.4,
    "max": 0.4
  },
  "adsDOFIntensity": {
    "constrain": true,
    "message": "#STR_SUDE_LAYOUT_OPTIONS_CONSTRAINED",
    "min": 0,
    "max": 0
  },
  "hideWeaponBarrelInOptic": {
    "constrain": true,
    "message": "#STR_SUDE_LAYOUT_OPTIONS_CONSTRAINED",
    "value": true
  },
  "hideClothingInOptic": {
    "constrain": true,
    "message": "#STR_SUDE_LAYOUT_OPTIONS_CONSTRAINED",
    "value": true
  },
  "lensZoomStrength": {
    "constrain": true,
    "message": "#STR_SUDE_LAYOUT_OPTIONS_CONSTRAINED",
    "min": 0.62,
    "max": 0.62
  },
  "deadzoneLimits": {
    "constrain": true,
    "message": "#STR_SUDE_LAYOUT_OPTIONS_CONSTRAINED",
    "min": [0, 0, 0, 0],
    "max": [1, 1, 1, 1]
  },
  "resetDeadzoneOnFocus": {
    "constrain": true,
    "message": "#STR_SUDE_LAYOUT_OPTIONS_CONSTRAINED",
    "value": true
  },
  "showDynamicCrosshair": {
    "constrain": true,
    "message": "#STR_SUDE_LAYOUT_OPTIONS_CONSTRAINED",
    "value": false
  },
  "dynamicCrosshairType": {
    "constrain": true,
    "message": "#STR_SUDE_LAYOUT_OPTIONS_CONSTRAINED",
    "value": 0
  },
  "dynamicCrosshairRGBA": {
    "constrain": true,
    "message": "#STR_SUDE_LAYOUT_OPTIONS_CONSTRAINED",
    "min": [0, 0, 0, 0],
    "max": [255, 255, 255, 255]
  }
}
```
## Установка и Настройка SuppressionMod
- Из необходимых модификаций нам потребуется [@SuppressionMod](https://steamcommunity.com/sharedfiles/filedetails/?id=2934318559)

Переходим по следующему пути:
```sh
DayZServer\profiles\Suppression
```
`EarProtectionItems.json`
В этом файле прописываются класснеймы наушников, которые помогут обезопасить игрока от оглушения.
```sh
TankerHelmet
TankerHelmetGreen
TankerHelmetRed
TankerHelmetBlue
Headphones
```
`SuppressionSettings.json`
Настройка конфигурации выглядит следующим образом:
```sh
{
    "Suppression_Normal_Decay": 10.0, //Подавление нормального спада
    "Suppression_Fast_Decay": 15.0, //Подавление быстрого разрушения
    "Suppresion_Protection_Decay": 40.0, //Подавление защит действия
    "Suppression_Max_Value": 200.0, //Максимальное значение подавления
    "Suppression_Muffle_Start": 140.0 //Подавление разрушения старта
}
```
`Примечание:`
```sh
- Вы должны удалить все подсказки из файла, которые начинаются после //Подсказка
- Не забываем перекидывать ключ модификации, в папку Keys в корне сервера
```
## Настройка Types (Время жизни предметов)
## Установка Expansion
![image](https://github.com/user-attachments/assets/cae21126-b78b-4009-a818-e5c39ee6f5e5)
- Из необходимых модификаций нам потребуется [DayZ-Expansion-Bundle](https://steamcommunity.com/sharedfiles/filedetails/?id=2572331007)
- Из необходимых модификаций нам потребуется [DayZ-Expansion-Licensed](https://steamcommunity.com/sharedfiles/filedetails/?id=2116157322)
## Настройка Безопасной Зоны
## Настройка Трейдеров
## Настройка Квестов
## Источники информации
```sh
https://steamcommunity.com/sharedfiles/filedetails/?id=2950062701
https://dayz-code.ru/topic/30-установка-модов-серверные-и-клиентские-моды/
```
