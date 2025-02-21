# Zubkova
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

![image](https://github.com/user-attachments/assets/735ac101-8d4c-43ec-99cf-091147f47beb)
![image](https://github.com/user-attachments/assets/37878b46-eede-4aea-add4-7f3c6ff73197)
