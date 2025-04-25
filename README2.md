![image](https://github.com/user-attachments/assets/0540a437-30be-421a-9756-9daaebc4a5d0)Перед началом работы была установлена новая виртуальная машина и установлены гостевые дополнения.
После этого были установлены необходимые утилиты (wget, curl, git) при помощи команды `sudo yum install`

![image](https://github.com/user-attachments/assets/6c696423-c075-41e4-a593-6e48915bfc72)

Далее проверяется состояние firewall командой `sudo firewall-cmd --state`

![image](https://github.com/user-attachments/assets/fcb3f7cb-ba94-448e-8f48-7643c3800922)

Следующим шагом происходит установка утилиты **tar** для работы с архивами.

![image](https://github.com/user-attachments/assets/94a81bc4-fb46-4f12-8507-cf7bc0619239)

Для синхронизации времени была использована команда `sudo yum install chrony`

![image](https://github.com/user-attachments/assets/3a0363c8-c3e3-4812-a125-7b657906e2f4)

`systemctl enable chronyd` - включает chrony
`systemctl start chronyd` - запускает chrony

![image](https://github.com/user-attachments/assets/03a00533-9c09-4084-b96b-600d1b8b43c1)

При вводе команды `getenforce` был получен ответ Enforcing, вседствие чего пришлось использовать команды для отключения getenforce.

`sudo setenforce 0` - отключает SELinux (Security-Enhanced Linux) в системе
`sudo sed -i 's/^SELINUX=.*/SELINUX=disabled/g' /etc/selinux/config` - редактирует файл /etc/selinux/config и устанавливает SELinux в режим disabled

![image](https://github.com/user-attachments/assets/3f478861-2ac7-442e-a5da-2c147bca7570)

После был скачан Prometheus. 3.3.0 / 2025-04-15 при помощи команды `wget https://github.com/prometheus/prometheus/releases/download/v3.3.0/prometheus-3.3.0.linux-amd64.tar.gz`.

![image](https://github.com/user-attachments/assets/990dac7a-8804-44ee-9064-9e270a3d4b64)

Далее были созданы директории для Prometheus командой `sudo mkdir -p /etc/prometheus /var/lib/prometheus`.

![image](https://github.com/user-attachments/assets/69d48274-6811-4feb-ba33-bff62adbbbe1)

Командой `tar -zxf prometheus-*.linux-amd64.tar.gz` был разархивирован файл, а после командой `cd prometheus-*.linux-amd64` был омуществлен переход в папку  **prometheus-*.linux-amd64**.

![image](https://github.com/user-attachments/assets/3eb9b41c-9358-4712-8bb5-5edbc45bb1a0)

Для проверки корректности папки была использована команда `pwd`.

![image](https://github.com/user-attachments/assets/b208f0c6-e681-4cb4-b666-79d98c70b9cb)

Следующими командами файлы Prometheus были скопированны в системные директории.

`sudo cp prometheus promtool /usr/local/bin/`
`sudo cp prometheus.yml /etc/prometheus/`

![image](https://github.com/user-attachments/assets/59135fd7-41b5-49e9-9ded-e90de7e88275)

Используя двойную команду осуществляется удаляение файлов и директорий, связанные с Prometheus.

`cd .. && rm -rf prometheus-*.linux-amd64/ && rm -f prometheus-*.linux-amd64.tar.gz`

Также было проверено содержимое директории командой `ls -l`.

![image](https://github.com/user-attachments/assets/6b6d497d-8e41-4dd8-96e7-17898f985ef0)








