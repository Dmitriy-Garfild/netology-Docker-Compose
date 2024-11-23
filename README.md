# netology-Docker-Compose

Сценарий выполнения задачи:
Установите docker и docker compose plugin на свою linux рабочую станцию или ВМ.
Если dockerhub недоступен создайте файл /etc/docker/daemon.json с содержимым: {"registry-mirrors": ["https://mirror.gcr.io", "https://daocloud.io", "https://c.163.com/", "https://registry.docker-cn.com"]}
Зарегистрируйтесь и создайте публичный репозиторий с именем "custom-nginx" на https://hub.docker.com (ТОЛЬКО ЕСЛИ У ВАС ЕСТЬ ДОСТУП);
скачайте образ nginx:1.21.1;
Создайте Dockerfile и реализуйте в нем замену дефолтной индекс-страницы(/usr/share/nginx/html/index.html), на файл index.html с содержимым:

	<html>
	<head>
	Hey, Netology
	</head>
	<body>
	<h1>I will be DevOps Engineer!</h1>
	</body>
	</html>
Соберите и отправьте созданный образ в свой dockerhub-репозитории c tag 1.0.0 (ТОЛЬКО ЕСЛИ ЕСТЬ ДОСТУП).
Предоставьте ответ в виде ссылки на https://hub.docker.com/<username_repo>/custom-nginx/general .

решение 1

https://hub.docker.com/repository/docker/garfild406/netology_homework/general

https://github.com/Dmitriy-Garfild/netology-Docker-Compose/blob/main/1.jpg



Задача 2
Запустите ваш образ custom-nginx:1.0.0 командой docker run в соответвии с требованиями:
имя контейнера "ФИО-custom-nginx-t2"
контейнер работает в фоне
контейнер опубликован на порту хост системы 127.0.0.1:8080
Не удаляя, переименуйте контейнер в "custom-nginx-t2"
Выполните команду date +"%d-%m-%Y %T.%N %Z" ; sleep 0.150 ; docker ps ; ss -tlpn | grep 127.0.0.1:8080 ; docker logs custom-nginx-t2 -n1 ; docker exec -it custom-nginx-t2 base64 /usr/share/nginx/html/index.html
Убедитесь с помощью curl или веб браузера, что индекс-страница доступна.
В качестве ответа приложите скриншоты консоли, где видно все введенные команды и их вывод.
решение 2
1. docker run -d --name "otrepyev-D-A-custom-nginx-t2" -p 127.0.0.1:8080:80 garfild406/netology_homework:1.0.0




2. docker rename "otrepyev-D-A-custom-nginx-t2" "custom-nginx-t2"



3 работа выполняется в windows, по этому линуксовые команды заменены на аналоги из PowerShell


PS C:\Users\Dim\Desktop\project\docker_compose_homework> Get-Date -Format "dd-MM-yyyy HH:mm:ss.fffffff zzz"
19-11-2024 13:43:40.3711564 +03:00
PS C:\Users\Dim\Desktop\project\docker_compose_homework> docker ps
CONTAINER ID   IMAGE                            	COMMAND              	CREATED      	STATUS      	PORTS                	NAMES
615a2ebbd577   garfild406/netology_homework:1.0.0   "/docker-entrypoint.…"   11 minutes ago   Up 11 minutes   127.0.0.1:8080->80/tcp   custom-nginx-t2
PS C:\Users\Dim\Desktop\project\docker_compose_homework> $port='8080'
PS C:\Users\Dim\Desktop\project\docker_compose_homework> Get-NetTcpConnection -State Listen | Where-Object {$_.LocalPort -eq "$port"} | Select-Object LocalAddress,LocalPort,OwningProcess,@{Name="Process";Expression={(Get-Process -Id $_.OwningProcess).ProcessName}} | Sort-Object -Property LocalPort | Format-Table

LocalAddress LocalPort OwningProcess Process
------------ --------- ------------- -------
127.0.0.1     	8080      	6136 com.docker.backend


PS C:\Users\Dim\Desktop\project\docker_compose_homework> docker logs custom-nginx-t2 -n1
172.17.0.1 - - [19/Nov/2024:10:33:29 +0000] "GET /favicon.ico HTTP/1.1" 404 153 "http://127.0.0.1:8080/" "Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:132.0) Gecko/20100101 Firefox/132.0" "-"
PS C:\Users\Dim\Desktop\project\docker_compose_homework> docker exec -it custom-nginx-t2 base64 /usr/share/nginx/html/index.html
PGh0bWw+DQo8aGVhZD4NCkhleSwgTmV0b2xvZ3kNCjwvaGVhZD4NCjxib2R5Pg0KPGgxPkkgd2ls
bCBiZSBEZXZPcHMgRW5naW5lZXIhPC9oMT4NCjwvYm9keT4NCjwvaHRtbD4=

What's next:
	Try Docker Debug for seamless, persistent debugging tools in any container or image → docker debug custom-nginx-t2
	Learn more at https://docs.docker.com/go/debug-cli/
PS C:\Users\Dim\Desktop\project\docker_compose_homework>

4.





Задача 3
Воспользуйтесь docker help или google, чтобы узнать как подключиться к стандартному потоку ввода/вывода/ошибок контейнера "custom-nginx-t2".
Подключитесь к контейнеру и нажмите комбинацию Ctrl-C.
Выполните docker ps -a и объясните своими словами почему контейнер остановился.
Перезапустите контейнер
Зайдите в интерактивный терминал контейнера "custom-nginx-t2" с оболочкой bash.
Установите любимый текстовый редактор(vim, nano итд) с помощью apt-get.
Отредактируйте файл "/etc/nginx/conf.d/default.conf", заменив порт "listen 80" на "listen 81".
Запомните(!) и выполните команду nginx -s reload, а затем внутри контейнера curl http://127.0.0.1:80 ; curl http://127.0.0.1:81.
Выйдите из контейнера, набрав в консоли exit или Ctrl-D.
Проверьте вывод команд: ss -tlpn | grep 127.0.0.1:8080 , docker port custom-nginx-t2, curl http://127.0.0.1:8080. Кратко объясните суть возникшей проблемы.
Это дополнительное, необязательное задание. Попробуйте самостоятельно исправить конфигурацию контейнера, используя доступные источники в интернете. Не изменяйте конфигурацию nginx и не удаляйте контейнер. Останавливать контейнер можно. пример источника
Удалите запущенный контейнер "custom-nginx-t2", не останавливая его.(воспользуйтесь --help или google)
В качестве ответа приложите скриншоты консоли, где видно все введенные команды и их вывод.

решение 3

1 ,2,3


Ctrl-C. Эта комбинация отправляет сигнал прерывания (SIGINT) контейнеу, что обычно приводит к его остановке.

4,5,6 
docker exec -it custom-nginx-t2 bash
apt-get update
apt-get install nano



7  nano /etc/nginx/conf.d/default.conf




8.
 

9,10. т.к выполняется работа на windows я приведу скриншот что по старому порту , страничка не доступна т.к. мы поменяли слушаемый порт на 81





11. docker rm -f custom-nginx-t2




Задача 4
Запустите первый контейнер из образа centos c любым тегом в фоновом режиме, подключив папку текущий рабочий каталог $(pwd) на хостовой машине в /data контейнера, используя ключ -v.
Запустите второй контейнер из образа debian в фоновом режиме, подключив текущий рабочий каталог $(pwd) в /data контейнера.
Подключитесь к первому контейнеру с помощью docker exec и создайте текстовый файл любого содержания в /data.
Добавьте ещё один файл в текущий каталог $(pwd) на хостовой машине.
Подключитесь во второй контейнер и отобразите листинг и содержание файлов в /data контейнера.
В качестве ответа приложите скриншоты консоли, где видно все введенные команды и их вывод.

решение 4

т.к. работаю в windows то просто подключу папку d:\docker

docker run -it -v d:/docker:/data centos:centos7.9.2009


команда it срезу дает нам доступ в нутрь и мы видим мой тестовый файл test.txt
собственно второй конейнер и тоже все видно


добавим файл


ну я уже вижу в вижел студио что он у меня появился :) , также создал финальный файл в директории через вижел студию и сейчас посмотрим на другом контейнере.






Задача 5
Создайте отдельную директорию(например /tmp/netology/docker/task5) и 2 файла внутри него. "compose.yaml" с содержимым:
version: "3"
services:
  portainer:
    network_mode: host
    image: portainer/portainer-ce:latest
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock

"docker-compose.yaml" с содержимым:
version: "3"
services:
  registry:
    image: registry:2

    ports:
    - "5000:5000"

И выполните команду "docker compose up -d". Какой из файлов был запущен и почему? (подсказка: https://docs.docker.com/compose/compose-application-model/#the-compose-file )
Отредактируйте файл compose.yaml так, чтобы были запущенны оба файла. (подсказка: https://docs.docker.com/compose/compose-file/14-include/)


Выполните в консоли вашей хостовой ОС необходимые команды чтобы залить образ custom-nginx как custom-nginx:latest в запущенное вами, локальное registry. Дополнительная документация: https://distribution.github.io/distribution/about/deploying/


Откройте страницу "https://127.0.0.1:9000" и произведите начальную настройку portainer.(логин и пароль адмнистратора)


Откройте страницу "http://127.0.0.1:9000/#!/home", выберите ваше local окружение. Перейдите на вкладку "stacks" и в "web editor" задеплойте следующий компоуз:


version: '3'

services:
  nginx:
    image: 127.0.0.1:5000/custom-nginx
    ports:
      - "9090:80"

Перейдите на страницу "http://127.0.0.1:9000/#!/2/docker/containers", выберите контейнер с nginx и нажмите на кнопку "inspect". В представлении <> Tree разверните поле "Config" и сделайте скриншот от поля "AppArmorProfile" до "Driver".


Удалите любой из манифестов компоуза(например compose.yaml). Выполните команду "docker compose up -d". Прочитайте warning, объясните суть предупреждения и выполните предложенное действие. Погасите compose-проект ОДНОЙ(обязательно!!) командой.


В качестве ответа приложите скриншоты консоли, где видно все введенные команды и их вывод, файл compose.yaml , скриншот portainer c задеплоенным компоузом.


решение 5

При выполнении команды docker compose up -d, будет запущен файл docker-compose.yaml, так как по умолчанию Docker Compose ищет файл именно с именем docker-compose.yaml.






