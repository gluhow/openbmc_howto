[SDK проекта](sdk.md)
[Сборка](build.md) программы для OpenBmc
Для очистки программы при сборке в Bitbake `bitabke {program} -c cleanall`

Просмотр параметров ядра:
```
zcat /proc/config.gz | grep 
```

##  Измененные файлы
`/run/initramfs/rw/cow`

## Создание патча
см. [Создать патч](bitbake.md)
## Отправка патча
В общий репозиторий отправка осуществляется через [Gerrit](gerrit)

# Просмотр исходников
Зачастую исходники удобно смотреть через https://grok.openbmc.org

# Вывод отладочной инфы
```
#include <iostream>
std::cout<<"Hello World" <<std::endl;
```
# Debug для определенной программы
Для некоторых программ (например U-boot) для включения отладки для определенного файла нужно в этот файл до всех `#INCLUDE` написать `#define DEBUG 1

## BMCWeb
Для включения дебажного вывода в BMCWeb добавьте в .bbappend
```
EXTRA_OEMESON:append = " \
     -Dbmcweb-logging=enabled \
     "
```

#  Сборка отдельной программы Meson
```
. .../sdk/environment-setup...
meson build -Dbuildtype=debugoptimized
ninja -C build/
aarch64-openbmc-linux-strip build/
```
# Просмотр логов
Если лог программы сделан через systemd `log<level::ERR>(...` то дополнительную информацию можно посмотреть через journalctl
```
journalctl -f -o verbose -u unit.service
```
# Инструмент отладки
https://github.com/amboar/culvert
# Отладка [phy](phy)