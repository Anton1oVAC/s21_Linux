## Part 1. Установка ОС
1. Узнаю версию Ubuntu, с помощью команды:
-cat /etc/issue.
![](./Screenshot/1.png)

## Part 2. Создание пользователя
1.  Создаю нового пользователя и добавляю его в группу adm
![](./Screenshot/2.1.png)
2. Вывод команды: 
-cat /etc/passwd
![](./Screenshot/2.2.png)

## Part 3. Настройка сети ОС
1. Задать название машины вида user-1               
Создал новый (hostname - user-1) с помощью команды:           
-sudo vim /etc/hostname              
И делаю перезагрузку:
-reboot        
![](./Screenshot/3.1.png)
2. Установил временную зону, которая соответствует текущему положению:        
![](./Screenshot/3.2-Time%20zone.png)
3. Вывел названия сетевых интерфейсов с помощью консольной команды:
-ifconfig       
![](./Screenshot/3.3%20ifconfig.png)
* lo (local loopback - локальная петля). Служит для подключения по сети к этому же компьютеру и не требует дополнительной настройки.
4. С помощью консольной команды получаю ip адрес устройства, на котором работаю, от DHCP сервера:
-hostname -I        
![](./Screenshot/3.4-%20ip%20от%20DHCP.png)
* Dynamic Host Configuration Protocol (DHCP) — автоматический предоставляет IP адреса и прочие настройки сети (маску сети, шлюз и т.п) компьютерам и различным устройствам в сети.
5. С помощью команды узнаю свой внешний ip-адрес шлюза:
-wget -O - -q icanhazip.com        
![](./Screenshot/3.5.1-внеш.png)
C мощью команд узнаю внутренний IP-адрес шлюза, он же по умолчанию: 
-ip addr или -ip route       
![](./Screenshot/3.5.2-внутр.png)
![](./Screenshot/3.5.3-По%20умол.png)
6. Чтобы задать статичные найтройки, нужно изменить файл с помощью команды:        
-sudo vim /etc/netplan/00-installer-config.yaml        
![](./Screenshot/3.6.2-изменение:ready.png)
После пропинговываю удаленные хосты 1.1.1.1 и ya.ru:        
![](./Screenshot/3.6.3-ping1.1.1.1.png)        
![](./Screenshot/%203.6.4-ping%20ya.ru.png)

##  Part 4.  Обновление ОС
1. Обновляю системные пакеты до последней версии командой:
-sudo apt-get upgrade
![](./Screenshot/4.png)

## Part 5. Использование команды sudo
1. Разрешаю пользователю, созданному в Part 2, выполнять команду sudo. Для этого использую команду:
-sudo usermod -aG sudo user21  
С помощью команды: -su переключаюсь на новую учетную запись и поменял hostname
![](./Screenshot/5.png)
* Sudo — это утилита, предоставляющая привилегии root для выполнения административных операций в соответствии со своими настройками. Она позволяет легко контролировать доступ к важным приложениям в системе. По умолчанию, при установке Ubuntu первому пользователю (тому, который создаётся во время установки) предоставляются полные права на использование sudo. Т.е. фактически первый пользователь обладает той же свободой действий, что и root. 

## Part 6. Установка и настройка службы времени
1. Вывожу корректное время командой:
-timedatectl show
![](./Screenshot/6.png)

## Part 7. Установка и использование текстовых редакторов
1. Установить текстовые редакторы, нужно было установить только редактор joe, vim и nano уже были установлены: 
-sudo apt install joe

###VIM
1. ![](./Screenshot/7.1-vim%20wq.png)  
2. ![](./Screenshot/7.2-vim%20q!.png)
3. ![](./Screenshot/7.3-vim%20search.png)
4. ![](./Screenshot/7.4-nano%20save.png)
* Создаю файл vim test_VIM.txt     
* Выхожу из режима редактирования и сохраняю файл: нажимаю esс и ввожу :wq     
* Выход без сохранения: :q!        
* Поиск: /<текст, который хотим найти>    
* Замена: :s/<что хотим изменить>/<на что хотим заменить>

### NANO
1. ![](./Screenshot/7.4-nano%20save.png)
2. ![](./Screenshot/7.5-nano%20no%20save.png)      
3. ![](./Screenshot/7.6-nano%20search.png)
4. ![](./Screenshot/7.7-nano%20to%20replace.png)
5. ![](./Screenshot/7.8-nano%20with.png)
6. ![](./Screenshot/7.9-nano%20replace.png)
* Создаю файл nano test_NANO.txt       
* Выхожу с сохранением: "control+O", затем нажимаю "enter"
* Выход без сохранения: "control+X", затем "N (no)"      
* Поиск: "control+W", затем пишу нужное слово и нажимаю "enter"
* Замена: "control+\" <"что хотим изменить" + "enter"> + <"на что хотим заменить" + "enter"> + "Y" или "N" применить, или отклонить 

### JOE
1. ![](./Screenshot/7.10-joe%20save.png)
2. ![](./Screenshot/7.11-joe%20no%20save.png)
3. ![](./Screenshot/7.12-joe%20search.png)
4. ![](./Screenshot/7.13-joe%20replace.png)

* Создаю файл joe test_mcedit.txt       
* Сохранить и выйти "control+K+X"
* Выйти без сохранения "control+C"
* Поиск: "control+K+F", пишу нужно слово/цифру нажимаю на "B" и "enter"
* Замена : "control+K+F", пишу нужно слово/цифру нажимаю на "R" и "enter", после выбираю на что заменить, и выбираю "Y" "N"

## Part 8. Установка и базовая настройка сервиса SSHD
1. Установливаю службу SSHd.
-sudo apt-get install ssh
-sudo apt install openssh-server
![](./Screenshot/8.1-%20install%20ssh.png)
2. Добавляю автостарт службы при загрузке системы и проверяю статус.
-sudo systemctl enable ssh
-systemctl status ssh
![](./Screenshot/8.2-%20status%20active.png)
3. Перенастраиваю службу SSHd на порт 2022 и перезагружаю ssh-сервер, чтобы изменения вступили в силу.
-sudo vim /etc/ssh/sshd_config
-systemctl restart sshd
![](./Screenshot/8.3-%20port2022.png)
![](./Screenshot/8.3.1-restart%20sshd.png)
4. Использую команду ps, для отображения процесса sshd
-ps -A | grep sshd
![](./Screenshot/8.4-%20ps%20-A.png)
* ps (показывает запущенные процессы, выполняемые пользователем в окне терминала);
* ps -e или ps -A (Чтобы просмотреть все запущенные процессы);
* ps -d (Чтобы показать все процессы, кроме лидеров сессии);
* ps -d -N (можно инвертировать вывод с помощью переключателя -N. Например, если хочу вывести только лидеров сеансов)
* ps T (увидеть только процессы, связанные с этим терминалом);
* ps r (просмотреть все работающие (running) процессы);
* ps -p 'pid' (если вы знаете идентификатор процесса PID, вы можете просто использовать следующую команду, для вывода процесса с этим 'pid');
* ps -p 'pid1' 'pid2'
* ps U 'userlist' (найти все процессы, выполняемые конкретным пользователем);
* ps -ef (получить полный список);
5. Перезагрузить систему
Вывод команды -netstat -tan
![](./Screenshot/8.5-%20netstat%20-tan.png)
* -t (--tcp) отображает соедниеня только по tcp
* -a (--all) вывод всех активных подключений TCP 
* -n (--numeric) вывод активных подключений TCP с отображением адресов и номеров портов в числовом формате
* Proto: Название протокола (протокол TCP или протокол UDP);
* recv-Q: очередь получения сети
* send-Q: Сетевая очередь отправки
* Local Address адрес локального компьтера и используемы номер порта
* Foreign Address адрес и номер удаленного компьтера к которомц подключен сокет
* State состояние сокетв
* 0.0.0.0 означает IP-адрес на локальной машине

## Part 9. Установка и использование утилит top, htop
1. Отчёт команды top:
* uptime - 1hour12min;
* количество авторизованных пользователей - 1;
* общую загрузку системы - 0.00, 0.00, 0.00
* общее количество процессов - 117;
* загрузку cpu - 0.1%;
* загрузку памяти - 168/7,74G;
* pid процесса занимающего больше всего памяти - 678 (top -o %MEM);
* pid процесса, занимающего больше всего процессорного времени - 1540 (top -o %CPU);
2. Скрины с выводом команды htop:
* отсортированному по PID, PERCENT_CPU, PERCENT_MEM, TIME
![](./Screenshot/9.1-%20htop%20cpu.png)
![](./Screenshot/9.2-htop%20pid.png)
![](./Screenshot/9.3-%20htop%20mem.png)
![](./Screenshot/9.4-%20htop%20time.png)
* отфильтрованному для процесса sshd
![](./Screenshot/9.5-%20htop%20sshd%20process.png)
* с процессом syslog, найденным, используя поиск
![](./Screenshot/9.6%20-%20htop%20syslog%20search.png)
* с добавленным выводом hostname, clock и uptime
![](./Screenshot/9.7%20-%20htop%20Right%20colum.png)

## Part 10. Использование утилиты fdisk
1. Запустить команду fdisk -l.
![](./Screenshot/10.1%20-%20fdisk%20-l.png)
* название жесткого диска - (Не показывает название);
* размер - 32GiB;
* количество секторов - 67108864;
* размер swap - 3.0Gi. (Для этого пришлось создать файл подкачки) 
![](./Screenshot/10.2%20-%20swap.png)

## Part 11. Использование утилиты df
1. Запустить команду df /.
* размер раздела - 14830568;
* размер занятого пространства - 6355200;
* размер свободного пространства - 7700200;
* процент использования - 46%;   
Определить и написать в отчёт единицу измерения в выводе - килобайт
2. Запустить команду df -Th.   
* размер раздела - 15G;
* размер занятого пространства - 6.1G;
* размер свободного пространства - 7.4G;
* процент использования  - 46%   
Определить и написать в отчёт тип файловой системы для раздела - ext4.
![](./Screenshot/11-%20df.png)

## Part 12. Использование утилиты du
1. Запустить команду du.
![](./Screenshot/12.1-%20du.png)
2. * Вывести размер папок /home, /var, /var/log (в байтах)
![](./Screenshot/12.2-%20du%20-s%20--block-size.png)
* Вывести размер папок /home, /var, /var/log (в человекочитаемом виде)
![](./Screenshot/12.2-%20du%20-sh.png)
3. Вывести размер всего содержимого в /var/log (не общее, а каждого вложенного элемента, используя *)
![](./Screenshot/12.3-%20var:log.png)

## Part 13. Установка и использование утилиты ncdu            
1. Установить утилиту ncdu.    
-sudo apt-get install ncdu    
Вывести размер папок /home, /var, /var/log.
![](./Screenshot/13.1%20-%20home.png)
![](./Screenshot/13.2%20-%20var.png)
![](./Screenshot/13.3%20-%20var:log.png)

## Part 14. Работа с системными журналами   
sudo vim /var/log/dmesg     
sudo vim /var/log/syslog          
sudo vim /var/log/auth.log          

1. Время последней успешной авторизации, имя пользователя и метод входа в систему (14:16:32; anton1o by LOGIN)
![](./Screenshot/14.1%20-%20last%20log%20auth.log.png)
2. Перезапускаю службу SSHd командой:    
-sudo systemctl restart ssh
3. Cкрин с сообщением о рестарте службы (искать в логах).
![](./Screenshot/14.2%20-%20syslog%20перезапуска%20ssh.png)

## Part 15. Использование планировщика заданий CRON
1. Пишу команду, чтобы сгенерировать новую таблицу cron.Команда: -crontab -e (На выбор дается 9 редакторов, выбираю nano). В конце прописываю "*/2 * * * *uptime", чтобы каждые две минуты выводилась информация о том, как долго работает система.
![](./Screenshot/15.1%20-%20start%20crontab.png)
* С помощью запроса: -cat /var/log/syslog вывел системный журнал о выполненой запланированной задачи.
![](./Screenshot/15.3%20-%20seccess.png)
* С помощью команды: -crontab -l посмотрел текущую задачу.
![](./Screenshot/15.2%20-%20inference%20crontab.png)
2. Командой: -crontab -r удалил задачу. И командой: -crontab -l увидел, что поставленых задач нету.
![](./Screenshot/15.4%20-%20delete%20crontab.png)