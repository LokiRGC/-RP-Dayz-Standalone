# Создание Tarkov сервера Dayz Standalone | Expansion | Realistic Modifications | Карта DayZone
## _Создание Локального Сервера_

Для создания сервера нам понадобится скачать с Библиотеки Steam во вкладке "инструменты" DayZServer. После установки заходим в папку через Свойства и расположение Локальных файлов. Наблюдаем небольшое количество Папок и Файлов. Создаем новую Папку и называем ее "profiles". Самого файла старта сервера нет, нужно его создать. Создаем текстовый документ, копируем текст ниже и вставляем.
![explorer_KPr6njCBZ6](https://github.com/user-attachments/assets/ee5c36aa-6f17-4999-bfea-4c6764f33025)
## Start.bat
Для запуска нашего сервера, потребуется создать .bat файл. 
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
В строчке -BEpath= указать месторасположение античита с папки сервера и указываем папку в строке -profiles с расположением этой папки на DayZServer.
Теперь меняем разрешение текстового файла с ".txt" на ".bat". Этот батник можно назвать любым именем.
## Как зайти на свой сервер
После запуска сервера откроется командная строка с отсчетом секунд до Рестарта и Консоль.
Открываем лаунчер DayZ, разворачиваем на весь экран, переходим во вкладку слева "Серверы" и тут находим ЛВС, где и будет возможность подключиться к серверу.

Чтобы отключить сервер нужно закрыть консоли.
ОК, хорошо, сервер запустился, персонаж появился, но просто ванильный DayZ - скучно.
Давайте я расскажу про установку модов, начнём с простейшего.
## Как устанавливать модификации
Скачиваем мод [@CF](https://steamcommunity.com/sharedfiles/filedetails/?id=1559212036) и  [@VPPAdminTools](https://steamcommunity.com/sharedfiles/filedetails/?id=1828439124). Заходим в лаунчер, справа от мода будет стрелочка, нажимаем ее, открывается дополнительная информация о моде, снизу справа нажимаем на три точки и на "скопировать в папку", указываем папку с DayZSever. Таким образом копируем моды в папку с сервером. После этого открываем каждый мод, заходим в папку "Keys" и копируем содержащийся в нем файл в папку "Keys", но уже в папке DayZServer. Делаем это с каждым модом.
Затем начинаем редактировать стартовый батник запуска сервера, а именно в длинной строчке находим "-mod=". Сюда после знака "=" вставляем БЕЗ пробелов название модов, должно получиться "-mod=@CF;@VPPAdminTools".

Прошу заметить, что названия модов разделяются только знаком ";" и только им, не пробелом, не двоеточием, ничем другим.
И так, моды установлены, ключи прописаны, в Start.bat всё прописано. Отлично, теперь запускаем сервер. После полной прогрузки консоли сервер закрываем.
## Настройка VPPAdminTools
Отправляемся в папку "Profiles", где видим появление новой папки "VPPAdminTools". Отправляемся по пути. Открываем этот текстовый файл, удаляем все и в него вставляем свой Steam64ID. Таким образом мы обозначаем моду, что такой ID имеет доступ к Админ-панели.
```sh
DayZServer\profiles\VPPAdminTools\Permissions\SuperAdmins
```
Открываем "credentials", сюда вписываем пароль от Админ панели.
```sh
DayZServer\profiles\VPPAdminTools\Permissions
```

Готово, мод установлен, админка прописана. Запускаем сервер, заходим. Сразу лезем в настройки привязки клавиш, заходим во вкладку "VPP" и настраиваем на удобные вам клавиши.
## Установка модификаций
- Из необходимых модификаций нам потребуется [@Dabs Framework](https://steamcommunity.com/workshop/filedetails/?id=2545327648)
- Из необходимых модификаций нам потребуется [@DayZ Editor Loader](https://steamcommunity.com/workshop/filedetails/?id=2276010135)

Все эти модификации, устанавливаем точно так же, как и @CF, @VPPAdminTools

## Источники информации
```sh
https://steamcommunity.com/sharedfiles/filedetails/?id=2950062701
```
