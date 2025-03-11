# GD
Отчет по виртуалке
Перед началой установки, нужно установить Linux Oracle на VirtualBox, для этого нужно:
Иметь образ Linux Выделить 2+ ядер. Выделать 4096+ МБ оперативы, и обязательно при установки мы выбираем английский язык.
Мы переходим к установке docker с использованием grafana. Вводим следующий код: Устанавливаем утилиту Wget

`sudo yum install wget`


![image](https://github.com/user-attachments/assets/cfef4eba-675a-4168-bb65-d66d7c346f03)


Устанавливаем утилиту Curl


![image](https://github.com/user-attachments/assets/bc0eb306-052a-436f-9bd7-b019b4e66b48)

Скачиваем файл репозитория
`sudo wget -P /etc/yum.repos.d/ https://download.docker.com/linux/centos/docker-ce.repo`

Нам выходит ошибка по причине того, что при копировании команды она не вставилась в комиандную строку. Напечатов полностью, был пропущен пробел

![image](https://github.com/user-attachments/assets/47cdf15b-c4a4-4cde-9f60-af3b13d063e0)

Ошибка вторая, неправильное наименнование файла

![image](https://github.com/user-attachments/assets/7a24ef9e-3b77-410d-becb-ac526bc2cbd4)


Установка репозитория была завершена.

![image](https://github.com/user-attachments/assets/185edf26-b09b-469a-a2b7-b26c62481700)

Установливаем dosker 
`sudo yum install docker-ce docker-ce-cli containerd.io.`

![image](https://github.com/user-attachments/assets/8406764c-0c5f-4219-8140-205e8e49512d)

Мы разрешаем автозапуск и запускаем 
`sudo systemctl enable docker --now`

![image](https://github.com/user-attachments/assets/4b9512ac-8a21-481d-905e-7ba7c6813b98)

Смотрим есть ли пакет curl 
`sudo yum install curl`

![image](https://github.com/user-attachments/assets/7832dca2-61ab-4cf4-be02-a2598905d31b)

Объявляем переменной COMVER, полученной в результате запроса curl, хранящей в себе номер последней версии Docker Compose
`COMVER=$(curl -s https://api.github.com/repos/docker/compose/releases/latest | grep 'tag_name' | cut -d\" -f4)`

![image](https://github.com/user-attachments/assets/fb3c04c3-2ab9-4f65-981a-8256bfdc3087)

Теперь скачиваем скрипт docker-compose последней версии
`sudo curl -L "https://github.com/docker/compose/releases/download/$COMVER/docker-compose-$(uname -s)-$(uname -m)" -o /usr/bin/docker-compose`

![image](https://github.com/user-attachments/assets/8e52426c-160c-40e7-a7b1-20469c80a2dd)

Предоставляем права на выполнения файла docker-compose
`sudo chmod +x /usr/bin/docker-compose`

![image](https://github.com/user-attachments/assets/fdf99ad9-8582-4275-b431-8f305897ea92)

Проверяем установленную версию Docker Compose.

![image](https://github.com/user-attachments/assets/704b8364-6f20-475b-bb70-ee9817b43569)

Соглашаемся скачать git
`git clone https://github.com/skl256/grafana_stack_for_docker.git`

![image](https://github.com/user-attachments/assets/691b7cd9-dbb9-403c-bfce-40fa71e6c627)

Переходим в папку
`cd grafana_stack_for_docker`

![image](https://github.com/user-attachments/assets/a2d2fe15-d1f3-4334-b5c2-f0ef477e4391)

Создаёт полный путь /mnt/common_volume/swarm/grafana/config, включая все необходимые промежуточные каталоги
`sudo mkdir -p /mnt/common_volume/swarm/grafana/config`

![image](https://github.com/user-attachments/assets/0d26dfc8-e153-415d-b2e9-119a50ae17e8)

Создаёт структуру каталогов для Grafana и связанных с ней компонентов
`sudo mkdir -p /mnt/common_volume/grafana/{grafana-config,grafana-data,prometheus-data}`

![image](https://github.com/user-attachments/assets/32daf972-eaec-47dd-9620-8bfeb598c03e)

Все файлы и каталоги в указанных директориях будут переданы в собственность текущему пользователю и его группе.
`sudo chown -R $(id -u):$(id -g) {/mnt/common_volume/swarm/grafana/config,/mnt/common_volume/grafana}`

![image](https://github.com/user-attachments/assets/faee54c3-c367-4567-83db-73f040d5478e)

Файл grafana.ini уже существует, команда обновит его временные метки. Если файла не будет команда создаст новый пустой файл, укажет имя по указанному пути
`touch /mnt/common_volume/grafana/grafana-config/grafana.ini`

![image](https://github.com/user-attachments/assets/7e987637-6b35-47ea-b472-752187dd0b6f)

Команда копирует все файлы и подкаталоги из директории config в директорию
`cp config/* /mnt/common_volume/swarm/grafana/config/`

![image](https://github.com/user-attachments/assets/0d3b8ca7-9167-4664-b6d3-e7ef0e4d41aa)

Команда переименовывает файл grafana.yaml в docker-compose.yaml.
`mv grafana.yaml docker-compose.yaml` 

![image](https://github.com/user-attachments/assets/bebe964f-db20-4c25-ab0d-140eaa667780)

Команда создает и запускает контейнеры в фоновом режиме используя конфигурацию из файла docker-compose.yml. Но с правами суперпользхователя
`sudo docker compose up -d`

![image](https://github.com/user-attachments/assets/a3ed6f06-5527-4f2e-ba61-482266d7e30f)

Заходим в Grafana
![image](https://github.com/user-attachments/assets/feb6b8fc-396b-4393-a900-c597ea726519)

sudo vi docker-compose.yaml
команда открывает файл docker-compose.yaml в текстовом редакторе vi с правами суперпользователя, что позволяет вам редактировать его содержимое.
Нас перекинет в текстовый редактор
Что-бы что-то изменить в тесковом редакторе нажмите insert на клавиатуре
Что бы сохранить что-то в этом документе нажимаем Esc пишем :wq! В этом текставом редакторе мы должны поставить node-exporter после services

Команда открывает файл prometheus.yaml в текстовом редакторе vi с правами суперпользователя.
`sudo vi prometheus.yaml`
Что бы выйти нам нужно нажать ESC+shift и на : на букве ж
потом ввести q!

![image](https://github.com/user-attachments/assets/77565952-20bc-4e19-b092-8126a27d323e)

Отображаем список запущенных контейнеров и их статусов. Эта команда показываем статусы всех сервиров определённых в файле docker-compose.yml.
`sudo vi docker-compose ps`

![image](https://github.com/user-attachments/assets/c92738b5-b441-4b76-92e5-f71dee2f3cef)

Мы заходили в файл dosker.compose.yaml, а после мы сделали команду `sudo docker compose stop` выполяем остановку контейниров. Данная команда останавливает работу запущенных контейнеров, но не удаляет их.

![image](https://github.com/user-attachments/assets/d885c4d7-715f-424d-b8a8-8c33b21fc1d6)

После мы снова вводим `sudo docker compose up -d`. Данная команда запускает приложение в фоновом режиме, то есть, в этом режиме контейнеры будут работать в фоновом режиме, и вывод команды не будет отображаться в терминале.

![image](https://github.com/user-attachments/assets/b6bf5158-879f-4111-b41a-3bbc397e3aa2)

Используем ещё одну команду `sudo docker compose down`. Данаая команда останавливает и удаляет все контейнеры, а также тома, связанные с ними, определённые в файле docker-compose.yml.

![image](https://github.com/user-attachments/assets/afe07953-6d6b-4a89-ae2d-89d9f43e7dae)

Ещё раз поднимаем `sudo docker compose up -d` для того что бы звпстить контейнеры.
![image](https://github.com/user-attachments/assets/cefa7235-2b2b-4efb-bebc-fa071462987d)

Создаем папку 1 и переносим туда файлы docker-compose.yaml и prometeus.yaml


![image](https://github.com/user-attachments/assets/e0fdc421-61b5-43fd-99a6-556262f52d02)

![image](https://github.com/user-attachments/assets/57562b8b-2ee4-4e73-8b9b-66a24fbec7bd)


Команда создаёт на компьютере точную копию репозитория, включая все его данные, историю и ветви. Используется для клонирования удалённого репозитория
`git clone https://githab.com/GerasikinaD/GD.git`

![image](https://github.com/user-attachments/assets/6a6b263b-dadd-42c7-b17d-26e75fee8534)


Пользователь с правами администратора открывает файл grafana.yaml для редактирования. 
`sudo vi grafana.yaml`
![image](https://github.com/user-attachments/assets/09182d54-9242-4b5b-96a9-eb4b41b2403e)

Команда `ls` выводит список содержимого домашнего каталога. В выходных данных отображаются такие каталоги, как Desktop, Downloads, Documents, Music Public, Pictures Templates, grafana_stack_for_docker

`cd grafana_stack_for_docker/`
Используется команду cd для смены текущего каталога на grafana_stack_for_docker, который был найден в списке домашнего каталога.

`ls` перечисляет содержимое каталога. На выходе отображаются файлы и каталоги, такие как config, GD, Screenshot_Loki.png, docker-compose.yaml, Readme.md и Screenshot_Prometheus.png

`cd GD Снова меняется каталог, на этот раз на каталог GD, который был в списке grafana_stack_for_docker

`ls` перечисляет содержимое GD каталога, показывая 1 и README.md

`cd 1` меняем каталог на каталог 1.

`ls` на выходе отображаются docker-compose.yaml и prometeus.yaml.

`mv prometeus.yaml prometheus.yaml` переименовывыем prometeus.yaml в prometheus.yaml. Обратите внимание на опечатку в первом случае. Эта команда, скорее всего, приведёт к ошибке «Нет такого файла или каталога» или аналогичной.

`ls` перечисляем каталоги на выходе отображаются docker-compose.yaml и prometheus.yaml

`sudo docker compose down` запускаеся docker compose down с помощью sudo, что останавливает и удаляет контейнеры Docker, определённые в файле docker-compose.yaml в текущем каталоге.

![image](https://github.com/user-attachments/assets/d4829fc3-26bb-49f8-854b-7b6703df9cee)

`sudo vi prometheus.yaml`
команда открывает файл prometheus.yaml в текстовом редакторе vi с правами суперпользователя.
/mnt/common_volume/swarm/grafana/config/prometheus.yaml - исправить targets: на exporter:9100,

![image](https://github.com/user-attachments/assets/236f2430-14bb-46f7-96c9-eb03fcfef1e2)

`cp prometheus.yaml prometheus.yaml1` Пытаемся скопировать файл prometheus.yaml в новый файл с именем prometheus.yaml1
Использует `ls` команду для перечисления содержимого config каталога.

Выходные данные команды ls показывают файлы в каталоге:
loki.yaml,
prometheus.yaml,
prometheus.yaml1 (копия, которая была только что создана),
promtail.yaml,
web-config.yaml.

![image](https://github.com/user-attachments/assets/6c8463bf-76d4-4e1f-a737-d058982944fe)

`cd` cd без аргумента, который по умолчанию должен возвращать в домашний каталог пользователя.

`ls` команда ls выводит список содержимого домашнего каталога. В выходных данных отображаются такие каталоги, как Desktop, Downloads, Documents, Music Public, Pictures Templates, grafana_stack_for_docker.

`cd grafana_stack_for_docker/` Используется команда cd для смены текущего каталога на grafana_stack_for_docker, который был найден в списке домашнего каталога

`ls` Приглашение показывает, что пользователь теперь находится в grafana_stack_for_docker каталоге.

ls перечисляет содержимое каталога.

На выходе отображаются файлы и каталоги, такие как config, GD, Screenshot_Loki.png, docker-compose.yaml, Readme.md и Screenshot_Prometheus.png.

`cd GD` снова меняется каталог, на этот раз на каталог GD, который был в списке grafana_stack_for_docker.

`ls` ls перечисляет содержимое GD каталога, показывая 1 и README.md

`cd 1` пытаемся использовать правильную команду «cd», чтобы сменить каталог на «1»

`ls`  перечисляется содержимое каталога 1.

На выходе отображаются «docker-compose.yaml» и «prometheus.yaml».

`sudo cp prometheus.yaml /mnt/common_volume/swarm/grafana/config:` пытаемся скопировать файл prometheus.yaml из текущего каталога (/mnt/common_volume/swarm/grafana/config). «sudo» означает, что потребуются повышенные права.

![image](https://github.com/user-attachments/assets/4934c936-e64d-45fe-94af-e7cc9ab1fcda)

`sudo vi ptometheus.yaml` 

sudo - выполняет следующую команду с правами администратора.
vi — текстовый редактор в Unix-подобных системах (vim в современных системах). Пользователь пытается открыть файл ptometheus.yaml для редактирования. В нём есть опечатка (ptometheus вместо prometheus).
ptometheus.yaml - Имя файла, которое пользователь пытается изменить (но с ошибкой в написании). Очень вероятно, что пользователь хотел открыть файл с исправленным именем prometheus.yaml.

`sudo docker compose up -d` 

Снова используется sudo для выполнения следующей команды в качестве суперпользователя.
docker compose up -d:
docker compose up команда — это часть интерфейса командной строки Docker Compose. Она указывает Docker Compose на необходимость создания (при необходимости) и запуска контейнеров, определённых в файле docker-compose.yaml в текущем каталоге.
-d - Отдельный режим. Этот флаг указывает Docker Compose на необходимость запуска контейнеров в фоновом режиме.

![image](https://github.com/user-attachments/assets/e09a16fd-83ec-46f6-a710-70d56a3184c9)


переходим на сайт `localhost:3000`

![image](https://github.com/user-attachments/assets/f63d959a-bcac-4d05-8040-68e73d6c83cc)

Открываем сайт
![image](https://github.com/user-attachments/assets/ff47f5b9-9a11-46bd-a825-7d9ce3d10d74)

Далее мы делаем действия:

пользователь и пароль: `admin`

код графаны `1816`

код прометеуса: `http://prometheus:9090`

выбираем вкладку Dashboards и создаем Dashboard

ждем кнопку +Add visualization, а после "Configure a new data source"

выбираем Prometheus

Connection

`http://prometheus:9090`

![image](https://github.com/user-attachments/assets/ecc2bb72-6ef6-48cc-a2f3-9ca92decb4df)

Authentication

Basic authentication

User: `admin`

Password: `admin`

Нажимаем на Save & test и должно показывать зелёную галочку

вкладку Dashboards и создаем Dashboard

 ![image](https://github.com/user-attachments/assets/b2184a59-99ce-41db-b872-b29fcc884a7a)
 
ждем кнопку "Import dashboard"

Find and import dashboards for common applications at grafana.com/dashboards: 1860 //ждем кнопку Load

Select Prometheus ждем кнопку "Import"

Полученный результат:

![image](https://github.com/user-attachments/assets/9fa10006-0897-4eb3-8ffd-469a018466ae)




 




