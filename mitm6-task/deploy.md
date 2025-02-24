1. Настроить kali, Win10 Pro и Win16 Server в одной подсети (Например, подсеть: 192.168.1.0/24)
2. Поднять домен (например, имя Polytech) на Win16 Server и ввести туда Win10 Pro.
3. Скачать nmap, mitm6, impacket на kali.
4. Создать пользователя в домене с легким паролем. (Например логин: Petr пароль: Qwerty12)
5. Убедиться, что SMB протокол работает в сети, а также что протоколы Zeroconf отключены на Win10 Pro.
6. Отключить и убедиться, что DHCPv6 в сети отключён
7. Включить и убедиться, что IPv6 с динамическии присвоением включен на Win10 Pro.
8. Настроить скрипт по типу New-SmbMapping -RemotePath '\server' -Username "domain\username" -Password "password", который будет выполняться раз в пол минуты (или в другое короткое время). <br>
   Пример скрипта: New-SmbMapping -RemotePath '\\Polytech321\folder' -Username "Polytech\Petr" -Password "Qwerty12"
