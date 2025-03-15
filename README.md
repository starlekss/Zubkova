# Zubkova

Задача выглядит следующим образом: 

![image](https://github.com/user-attachments/assets/6f93137e-1c8d-4d57-8627-67720dbcab51)

Перед началом работы происходит установка Linux Oracle на VirtualBox,со следующими параметрами: **2 ядра, 4096 МБ оперативной памяти**, а также при установке выбран **английский язык**.

Далее устанавливаем утилиту ***wget*** для скачивания файлов из интернета при помощи команды .
1. `sudo yum install wget`

![image](https://github.com/user-attachments/assets/8e4159ce-489a-429f-bee6-f631c59235b7)

Следующим шагом является установка утилиты ***curl*** (в данном случае она уже установлена, данной командй выполняется проверка этого)

2. `sudo yum install curl`

![image](https://github.com/user-attachments/assets/4ff3633d-5c9a-4fa0-956a-6ff2cfbc0bae)

После этого используется команда, которая добавляет репозиторий Docker в список доступных репозиториев для ***yum***, что позволяет впоследствии установить Docker.

3. `sudo wget -P /etc/yum.repos.d/ https://download.docker.com/linux/centos/docker-ce.repo`

![image](https://github.com/user-attachments/assets/7789a60b-b21a-4f77-8fc8-60be58694b6f)

Последующим шагом является использование команды, которая устанавливает необходимые компоненты Docker

4. `sudo yum install docker-ce docker-ce-cli containerd.io`

![image](https://github.com/user-attachments/assets/ca4390f7-d974-41ef-aa54-2a93321a54e6)
![image](https://github.com/user-attachments/assets/9985b547-238b-4274-9ba5-c171573ef681)

Далее запускается команда, которая делает две вещи: включает Docker для автоматического запуска при каждой загрузке системы, а также немедленно запускает службу Docker.

5. `sudo systemctl enable docker --now`

![image](https://github.com/user-attachments/assets/434ef98e-1550-4313-ad4a-321f869b20c7)

После выполнении команды, переменная ***COMVER*** будет содержать версию последнего релиза Docker Compose.

6. `COMVER=$(curl -s https://api.github.com/repos/docker/compose/releases/latest | grep 'tag_name' | cut -d\" -f4)`
   
![image](https://github.com/user-attachments/assets/1a212480-639d-4f8a-8ea1-6a4999b0c8d4)

После выполнения следующей команды, исполняемый файл Docker Compose будет доступен для запуска.

7. `sudo curl -L "https://github.com/docker/compose/releases/download/$COMVER/docker-compose-$(uname -s)-$(uname -m)" -o /usr/bin/docker-compose`

![image](https://github.com/user-attachments/assets/0259be5a-f105-455d-9444-41c3f37684c2)

Последующая команда предоставляет права на выполнение файлу ***/usr/bin/docker-compose***, а так же выполняется команда, выволящая на экран информацию о версии установленного Docker Compose.

8. `sudo chmod +x /usr/bin/docker-compose`
9. `docker-compose --version`

![image](https://github.com/user-attachments/assets/59f65146-0ea2-44f2-aaa9-eeea7e87a8a0)

Следующим шагом скачиваются все файлы и историю изменений из репозитория ***git***.

10. `git clone https://github.com/skl256/grafana_stack_for_docker.git`

![image](https://github.com/user-attachments/assets/1d7d8c74-781d-41f0-8cdf-c93e8dddeb57)

При выполнении команды выдается ошибка, исправляемая командой `sudo yum install git`, позволяющей установить пакеты git.

![image](https://github.com/user-attachments/assets/04387a49-2c18-4062-95d4-7efaa2f39717)

После этого все осуществляется корректно.

![image](https://github.com/user-attachments/assets/6189a7c3-3798-4c63-af38-4942f4781bfc)

Далее используется утилита ***cd*** (change directory) для смены текущего рабочего каталога в командной строке Linux, после чего выполняется ряд команд.

11. `cd grafana_stack_for_docker`

Эта команда использует утилиту mkdir для создания каталогов (директорий) на файловой системе.

12. `sudo mkdir -p /mnt/common_volume/swarm/grafana/config`
    
Эта команда использует утилиту ***mkdir*** с опцией -p и расширением фигурных скобок (brace expansion) для создания нескольких каталогов в файловой системе.

13. `sudo mkdir -p /mnt/common_volume/grafana/{grafana-config,grafana-data,prometheus-data}`
    
Эта команда использует утилиту ***chown*** для изменения владельца (owner) и группы (group) файлов и каталогов.

14. `sudo chown -R $(id -u):$(id -g) {/mnt/common_volume/swarm/grafana/config,/mnt/common_volume/grafana}`

Эта команда использует утилиту ***touch*** для создания пустого файла.

15. `touch /mnt/common_volume/grafana/grafana-config/grafana.ini`

Эта команда использует утилиту ***cp*** (copy) для копирования файлов.

16. `cp config/* /mnt/common_volume/swarm/grafana/config/`
    
Эта команда использует утилиту ***mv*** (move) для переименования файла, обычно приводя имя файла к стандартному или ожидаемому.

17. `mv grafana.yaml docker-compose.yaml`
    
Эта команда использует docker compose для запуска и управления приложением, определенным в файле ***docker-compose.yaml***. Она позволяет легко разворачивать и управлять сложными Docker-приложениями

18. `sudo docker compose up -d`
    
**-d** - Параметр -d в команде docker-compose up означает демонизирование процесса — запуск контейнеров в фоновом режиме.

![image](https://github.com/user-attachments/assets/735ac101-8d4c-43ec-99cf-091147f47beb)
![image](https://github.com/user-attachments/assets/37878b46-eede-4aea-add4-7f3c6ff73197)

19. `sudo docker compose stop`

Команда останавливает запущенные контейнеры без их удаления.

![image](https://github.com/user-attachments/assets/c86312bd-af46-4596-b030-66f4ee054682)

20. `sudo docker compose down`

Используемая команда для остановки и удаления контейнеров, сетей и томов, определенных в файле docker-compose.yml.

![image](https://github.com/user-attachments/assets/b04e92d1-7da7-4958-b2bc-29b88051b5a2)

21. `sudo docker compose ps`
    
Команда показывает информацию о контейнерах, управляемых Docker Compose, определенных в файле docker-compose.yml.

![image](https://github.com/user-attachments/assets/ab2365b4-43da-4bf1-88ef-c5bb73eb15da)

22. `pwd`

Команда выводит на экран абсолютный путь к текущей рабочей директории.

![image](https://github.com/user-attachments/assets/ded45dca-3500-4329-b36d-1cb4416ef451)

23. `sudo git clone https://github.com/starlekss/Zubkova`

При помощи этой команды происходит комирование репрозитория с Github.

![image](https://github.com/user-attachments/assets/5c1bf1f1-29e1-409b-a4c9-96c7d291ea62)

Также была использована команда `ls` для просмотра файлов в папке.

24. `sudo vi docker-compose.yaml`
    
Команда предназначена для открытия или создания файла docker-compose.yaml в текстовом редакторе vi с правами суперпользователя (root).

![image](https://github.com/user-attachments/assets/b8b300af-678e-4529-be4f-084640514473)
![image](https://github.com/user-attachments/assets/f6ebf3bb-26bb-4ff4-819e-3c4813c6b747)

25. `sudo vi prometeus.yaml`
    
Команда также используется для открытия или создания файла с именем prometheus.yaml в текстовом редакторе vi с правами суперпользователя (root).

![image](https://github.com/user-attachments/assets/681bccc8-0e1c-466f-90e0-35af7edaa3ef)
![image](https://github.com/user-attachments/assets/eaa94ac6-54c7-48ea-be47-7ca3079f148f)

# Grafana

Сайт: localhost:3000 
User & Password: admin

Зайдя на сайт выбирается Dashboards для создания Dashboard

![image](https://github.com/user-attachments/assets/8bfe99f0-8f37-4d6a-95c7-9de146e6915b)

Следующий шаг: +Add visualization, после Configure a new data source и выбирается Prometheus

![image](https://github.com/user-attachments/assets/564bdfb5-09b3-47b1-9fec-06d3a96b6629)

Настройка: 
Connection: `http://prometheus:9090`
Authentication: `Basic authentication`

В завершении `Save & test`

![image](https://github.com/user-attachments/assets/45066f6a-7e4e-4f36-b26b-bfdf38a6b659)

Далее, при помощи `Import dashboard` созданный Dashboard импортируется. 

`Find and import dashboards for common applications at grafana.com/dashboards: 1860`

![image](https://github.com/user-attachments/assets/c6c4684f-bb09-45e3-a6b3-438be377aa55)

В конце `Select Prometheus` и `Import`.

![image](https://github.com/user-attachments/assets/2b1634b5-af15-42d6-9bbc-d5316ad96304)

# VictoriaMetrics

![image](https://github.com/user-attachments/assets/dc1f771c-c49e-4cb4-8365-7ae73e3f2bb8)

![image](https://github.com/user-attachments/assets/700682e7-c47d-4df2-8a0e-3c6ad9197308)

![image](https://github.com/user-attachments/assets/a98be8b0-3697-49be-8787-d74194c9619a)


