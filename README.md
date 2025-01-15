# Disaster-Recovery.-FHRP-Keepalived
# Задание 1
- Дана схема для Cisco Packet Tracer, рассматриваемая в лекции.
- На данной схеме уже настроено отслеживание интерфейсов маршрутизаторов Gi0/1 (для нулевой группы)
- Необходимо аналогично настроить отслеживание состояния интерфейсов Gi0/0 (для первой группы).
- Для проверки корректности настройки, разорвите один из кабелей между одним из маршрутизаторов и Switch0 и запустите ping между PC0 и Server0.
- На проверку отправьте получившуюся схему в формате pkt и скриншот, где виден процесс настройки маршрутизатора.


# Решение

![image](https://github.com/user-attachments/assets/4a116e6d-e34a-415a-b8bf-7bf92fd057ec)
![image](https://github.com/user-attachments/assets/8083988c-cead-4819-a4bf-3b6ce4e182a0)
![image](https://github.com/user-attachments/assets/3c45260d-e049-4e23-8438-46cacc6abacc)

файл https://github.com/Igorekpio/Disaster-Recovery.-FHRP-Keepalived/blob/main/hsrp_advanced_SYS-37.pkt



# Задание 2
- Запустите две виртуальные машины Linux, установите и настройте сервис Keepalived как в лекции, используя пример конфигурационного файла.
- Настройте любой веб-сервер (например, nginx или simple python server) на двух виртуальных машинах
- Напишите Bash-скрипт, который будет проверять доступность порта данного веб-сервера и существование файла index.html в root-директории данного веб-сервера.
- Настройте Keepalived так, чтобы он запускал данный скрипт каждые 3 секунды и переносил виртуальный IP на другой сервер, если bash-скрипт завершался с кодом, отличным от нуля (то есть порт веб-сервера был недоступен или отсутствовал index.html). Используйте для этого секцию vrrp_script
- На проверку отправьте получившейся bash-скрипт и конфигурационный файл keepalived, а также скриншот с демонстрацией переезда плавающего ip на другой сервер в случае недоступности порта или файла index.html


<details>

```
#!/bin/bash
if [[ $(netstat -tuln | grep LISTEN | grep :80) ]] && [[ -f /var/www/html/index.nginx-debian.html ]]; then
        exit 0
else
        sudo systemctl stop keepalived.service
fi
```

</details>

Файл конфига https://github.com/Ivashka80/Disaster-recovery_Keepalived/blob/main/keepalived.conf

![image](https://github.com/user-attachments/assets/c24a9163-8d56-43da-a24f-d2f61f6dd3bf)

![image](https://github.com/user-attachments/assets/ec89ee72-2511-434e-a951-63d97ef9a638)




