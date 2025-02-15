# GD
Отчет по виртуалке
Устанавливаем Wget
![image](https://github.com/user-attachments/assets/cfef4eba-675a-4168-bb65-d66d7c346f03)


пакет Curl установлен
![image](https://github.com/user-attachments/assets/bc0eb306-052a-436f-9bd7-b019b4e66b48)


Нам выходит ошибка по причине того, что при копировании команды она не вставилась в комиандную строку. Напечатов полностью, был пропущен пробел
![image](https://github.com/user-attachments/assets/47cdf15b-c4a4-4cde-9f60-af3b13d063e0)

Ошибка вторая, неправильное имя файла
![image](https://github.com/user-attachments/assets/7a24ef9e-3b77-410d-becb-ac526bc2cbd4)


Установка завершена.
![image](https://github.com/user-attachments/assets/185edf26-b09b-469a-a2b7-b26c62481700)

Установка тоже завершена данной команды. sudo yum install docker-ce docker-ce-cli containerd.io. Тут мы устанавливали dosker.
![image](https://github.com/user-attachments/assets/8406764c-0c5f-4219-8140-205e8e49512d)

Мы разрешаем автозапуск и запускаем в принципе
![image](https://github.com/user-attachments/assets/4b9512ac-8a21-481d-905e-7ba7c6813b98)

Посмотреть есть ли пакет curl 
Объявление переменной COMVER, полученной в результате curl запроса, хранящей в себе номер последней версии Docker Compose
![image](https://github.com/user-attachments/assets/7832dca2-61ab-4cf4-be02-a2598905d31b)
![image](https://github.com/user-attachments/assets/fb3c04c3-2ab9-4f65-981a-8256bfdc3087)

Теперь скачиваем скрипт docker-compose последней версии
sudo curl -L "https://github.com/docker/compose/releases/download/$COMVER/docker-compose-$(uname -s)-$(uname -m)" -o /usr/bin/docker-compose
![image](https://github.com/user-attachments/assets/8e52426c-160c-40e7-a7b1-20469c80a2dd)

Предоставляем права на выполнения файла docker-compose
![image](https://github.com/user-attachments/assets/fdf99ad9-8582-4275-b431-8f305897ea92)

Установленная версия docker
![image](https://github.com/user-attachments/assets/704b8364-6f20-475b-bb70-ee9817b43569)

Соглашаемся скачать git
![image](https://github.com/user-attachments/assets/691b7cd9-dbb9-403c-bfce-40fa71e6c627)

Переходим в папку
![image](https://github.com/user-attachments/assets/a2d2fe15-d1f3-4334-b5c2-f0ef477e4391)

Создаёт полный путь /mnt/common_volume/swarm/grafana/config, включая все необходимые промежуточные каталоги
![image](https://github.com/user-attachments/assets/0d26dfc8-e153-415d-b2e9-119a50ae17e8)

Создаёт структуру каталогов для Grafana и связанных с ней компонентов
![image](https://github.com/user-attachments/assets/32daf972-eaec-47dd-9620-8bfeb598c03e)

Все файлы и каталоги в указанных директориях будут переданы в собственность текущему пользователю и его группе
![image](https://github.com/user-attachments/assets/faee54c3-c367-4567-83db-73f040d5478e)

Файл grafana.ini уже существует, команда обновит его временные метки 
![image](https://github.com/user-attachments/assets/7e987637-6b35-47ea-b472-752187dd0b6f)

Команда копирует все файлы и подкаталоги из директории config в директорию
![image](https://github.com/user-attachments/assets/0d3b8ca7-9167-4664-b6d3-e7ef0e4d41aa)

Команда переименовывает файл grafana.yaml в docker-compose.yaml.
![image](https://github.com/user-attachments/assets/bebe964f-db20-4c25-ab0d-140eaa667780)

Команда создает и запускает контейнеры в фоновом режиме используя конфигурацию из файла docker-compose.yml. Но с правами суперпользхователя
![image](https://github.com/user-attachments/assets/a3ed6f06-5527-4f2e-ba61-482266d7e30f)

Заходим в Grafana
![image](https://github.com/user-attachments/assets/feb6b8fc-396b-4393-a900-c597ea726519)


