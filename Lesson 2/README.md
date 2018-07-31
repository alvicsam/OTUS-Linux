Изменил Vagrantfile следующим образом:
1. Добавил диск sata5
2. Изменил секцию SHELL: 
    2.1 Создается массив (RAID5, 5 дисков)
    2.2 Конфиг пишется в /etc/mdadm.conf
    2.3 С помощью parted создается GPT таблица, создаются 5 разделов
    2.4 В цикле создается файловая система на 5 разделах
    2.5 В цикле добавляются строчки в fstab для автомонтирования при загрузке
    2.6 Создаются каталоги для монтирования
    2.8 Монтируются разделы в созданные выше каталоги

Ломал/чинил массив следующим набором команд:
mdadm --manage /dev/md0 --fail /dev/sdf
mdadm --manage /dev/md0 --remove /dev/sdf
mdadm --zero-superblock /dev/sdf
mdadm --manage /dev/md0 --add /dev/sdf