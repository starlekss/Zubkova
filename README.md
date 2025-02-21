# Zubkova
Перед началом работы происходит установка Linux Oracle на VirtualBox,со следующими параметрами: 2 ядра, 4096 МБ оперативной памяти, а также при установке выбран английский язык.

Далее устанавливаем утилиту wget для скачивания файлов из интернета при помощи команды .
1. sudo yum install wget

![image](https://github.com/user-attachments/assets/8e4159ce-489a-429f-bee6-f631c59235b7)

Следующим шагом является установка утилиты curl (в данном случае она уже установлена, данной командй выполняется проверка этого)

2. sudo yum install curl

![image](https://github.com/user-attachments/assets/4ff3633d-5c9a-4fa0-956a-6ff2cfbc0bae)

После этого используется команда, которая добавляет репозиторий Docker в список доступных репозиториев для yum, что позволяет впоследствии установить Docker.

3. sudo wget -P /etc/yum.repos.d/ https://download.docker.com/linux/centos/docker-ce.repo

![image](https://github.com/user-attachments/assets/7789a60b-b21a-4f77-8fc8-60be58694b6f)

Последующим шагом является использование команды, которая устанавливает необходимые компоненты Docker

4. sudo yum install docker-ce docker-ce-cli containerd.io

![image](https://github.com/user-attachments/assets/ca4390f7-d974-41ef-aa54-2a93321a54e6)
![image](https://github.com/user-attachments/assets/9985b547-238b-4274-9ba5-c171573ef681)

Далее запускается команда, которая делает две вещи: включает Docker для автоматического запуска при каждой загрузке системы, а также немедленно запускает службу Docker.

5. sudo systemctl enable docker --now

![image](https://github.com/user-attachments/assets/434ef98e-1550-4313-ad4a-321f869b20c7)

После выполнении команды, переменная COMVER будет содержать версию последнего релиза Docker Compose.

6. COMVER=$(curl -s https://api.github.com/repos/docker/compose/releases/latest | grep 'tag_name' | cut -d\" -f4)
   
![image](https://github.com/user-attachments/assets/1a212480-639d-4f8a-8ea1-6a4999b0c8d4)

7. 




