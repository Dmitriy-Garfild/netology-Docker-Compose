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

![alt text](https://github.com/Dmitriy-Garfild/netology-Docker-Compose/blob/main/1.PNG)

![alt text](https://github.com/Dmitriy-Garfild/netology-Docker-Compose/blob/main/2.PNG)



Задача 2

1.Запустите ваш образ custom-nginx:1.0.0 командой docker run в соответвии с требованиями:
имя контейнера "ФИО-custom-nginx-t2"
контейнер работает в фоне
контейнер опубликован на порту хост системы 127.0.0.1:8080
2.Не удаляя, переименуйте контейнер в "custom-nginx-t2"
3.Выполните команду 
	date +"%d-%m-%Y %T.%N %Z" ; sleep 0.150 ; docker ps ; ss -tlpn | grep 127.0.0.1:8080 ; docker logs custom-nginx-t2 -n1 ; docker exec -it custom-nginx-t2 base64 /usr/share/nginx/html/index.html
Убедитесь с помощью curl или веб браузера, что индекс-страница доступна.
В качестве ответа приложите скриншоты консоли, где видно все введенные команды и их вывод.

Решение 2

1.запускаем образ:
   
	docker run -d --name "otrepyev-D-A-custom-nginx-t2" -p 127.0.0.1:8080:80 garfild406/netology_homework:1.0.0

![alt text](https://github.com/Dmitriy-Garfild/netology-Docker-Compose/blob/main/3.PNG)

![alt text](https://github.com/Dmitriy-Garfild/netology-Docker-Compose/blob/main/4.PNG)


2. переименуем контейнер

	docker rename "otrepyev-D-A-custom-nginx-t2" "custom-nginx-t2"

![alt text](https://github.com/Dmitriy-Garfild/netology-Docker-Compose/blob/main/5.PNG)

3 работа выполняется в windows, по этому линуксовые команды заменены на аналоги из PowerShell

Get-Date -Format "dd-MM-yyyy HH:mm:ss.fffffff zzz"

docker ps

$port='8080'

Get-NetTcpConnection -State Listen | Where-Object {$_.LocalPort -eq "$port"} | Select-Object LocalAddress,LocalPort,OwningProcess,@{Name="Process";Expression={(Get-Process -Id $_.OwningProcess).ProcessName}} | Sort-Object -Property LocalPort | Format-Table

docker logs custom-nginx-t2 -n1

docker exec -it custom-nginx-t2 base64 /usr/share/nginx/html/index.html


![alt text](https://github.com/Dmitriy-Garfild/netology-Docker-Compose/blob/main/6.PNG)

4.

![alt text](https://github.com/Dmitriy-Garfild/netology-Docker-Compose/blob/main/7.PNG)



Задача 3
1. Воспользуйтесь docker help или google, чтобы узнать как подключиться к стандартному потоку ввода/вывода/ошибок контейнера "custom-nginx-t2".
2. Подключитесь к контейнеру и нажмите комбинацию Ctrl-C.
3. Выполните docker ps -a и объясните своими словами почему контейнер остановился.
4. Перезапустите контейнер
5. Зайдите в интерактивный терминал контейнера "custom-nginx-t2" с оболочкой bash.
6. Установите любимый текстовый редактор(vim, nano итд) с помощью apt-get.
7. Отредактируйте файл "/etc/nginx/conf.d/default.conf", заменив порт "listen 80" на "listen 81".
8. Запомните(!) и выполните команду nginx -s reload, а затем внутри контейнера curl http://127.0.0.1:80 ; curl http://127.0.0.1:81.
9. Выйдите из контейнера, набрав в консоли exit или Ctrl-D.
10. Проверьте вывод команд: ss -tlpn | grep 127.0.0.1:8080 , docker port custom-nginx-t2, curl http://127.0.0.1:8080. Кратко объясните суть возникшей проблемы.
11. Удалите запущенный контейнер "custom-nginx-t2", не останавливая его.(воспользуйтесь --help или google)
В качестве ответа приложите скриншоты консоли, где видно все введенные команды и их вывод.



решение 3

1 ,2,3

![alt text](https://github.com/Dmitriy-Garfild/netology-Docker-Compose/blob/main/8.PNG)

Ctrl-C. Эта комбинация отправляет сигнал прерывания (SIGINT) контейнеу, что обычно приводит к его остановке.

4,5,6 
  docker exec -it custom-nginx-t2 bash
  apt-get update
  apt-get install nano

![alt text](https://github.com/Dmitriy-Garfild/netology-Docker-Compose/blob/main/9.PNG)



7  nano /etc/nginx/conf.d/default.conf

![alt text](https://github.com/Dmitriy-Garfild/netology-Docker-Compose/blob/main/10.PNG)


8.
 
![alt text](https://github.com/Dmitriy-Garfild/netology-Docker-Compose/blob/main/11.PNG)


9,10. т.к выполняется работа на windows я приведу скриншот, показывающий, что по старому порту  страничка не доступна, т.к. мы поменяли слушаемый порт на 81


![alt text](https://github.com/Dmitriy-Garfild/netology-Docker-Compose/blob/main/12.PNG)


11. 
  docker rm -f custom-nginx-t2



Это дополнительное, необязательное задание. Попробуйте самостоятельно исправить конфигурацию контейнера, используя доступные источники в интернете. Не изменяйте конфигурацию nginx и не удаляйте контейнер. Останавливать контейнер можно. пример источника


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

![alt text](https://github.com/Dmitriy-Garfild/netology-Docker-Compose/blob/main/13.PNG)


команда it срезу дает нам доступ в нутрь и мы видим мой тестовый файл test.txt
собственно второй конейнер и тоже все видно

![alt text](https://github.com/Dmitriy-Garfild/netology-Docker-Compose/blob/main/14.PNG)

добавим файл

![alt text](https://github.com/Dmitriy-Garfild/netology-Docker-Compose/blob/main/15.PNG)

ну я уже вижу в вижел студио что у меня появился новый файл :) , также создал финальный файл в подключенной директории через вижел студию и сейчас посмотрим на другом контейнере.


![alt text](https://github.com/Dmitriy-Garfild/netology-Docker-Compose/blob/main/16.PNG)



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

1. При выполнении команды docker compose up -d, будет запущен файл docker-compose.yaml, так как по умолчанию Docker Compose ищет файл именно с именем docker-compose.yaml.

2.

![alt text](https://github.com/Dmitriy-Garfild/netology-Docker-Compose/blob/main/17.PNG)

3.

![alt text](https://github.com/Dmitriy-Garfild/netology-Docker-Compose/blob/main/18.PNG)


![alt text](https://github.com/Dmitriy-Garfild/netology-Docker-Compose/blob/main/19.PNG)





