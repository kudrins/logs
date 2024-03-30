## Домашнее и дополнительное задание
## Сбор и хранение логов
```
В VMware vSphere 7
разворачиваются и настраиваются VMs
- centos-web 
    устанавливается nginx
    настраивается rsyslog
- centos-log
    настраивается rsyslog
- ubuntu-elk
    устанавливается elk
    устанавливается filebeat

cenos-web отправляет логи в 2 центральных системы
centos-web -> centos-log
  - все критичные логи
  - логи аудита
centos-web -> ubuntu-elk
  - логи nginx
  - логи аудита конфига nginx
ubuntu-elk
  - локольные логи filebeat
  
Файлы:

- /ansible/newvm.yml:              ansible playbook развертывания и настройки VMs
- /ansible/vars.yml                переменные для создания VMs в VMware vSphere 7
- /ansible/host:                   Inventory

VM cenos-web
- /centos-web/nginx.conf:          /etc/nginx/nginx.conf файл конфигурации nginx
- /centos-web/10-nginx.conf:       /etc/rsyslog.d/10-nginx.conf - настройка отправки
                                   логов аудита конфига nginx на elk
- /centos-web/20-crit.conf:        /etc/rsyslog.d/20-crit.conf - настройка отправки
                                   критичных логов на rsyslog VM centos-log
- /centos-web/30-audit.conf:       /etc/rsyslog.d/30-audit.conf - настройка отправки
                                   логов аудита на rsyslog VM centos-log

VM centos-log
- /centos-log/rsyslog.conf:        /etc/rsyslog.conf файл конфигурации rsyslog
                                   VM centos-log
VM ubuntu-elk
  настройка logstash
- /ubuntu-elk/filter.conf:         /etc/logstash/conf.d/filter.conf - фильтры
- /ubuntu-elk/input.conf:          /etc/logstash/conf.d/input.conf - входные данные
- /ubuntu-elk/output.conf:         /etc/logstash/conf.d/output.conf - выходные данные

- /ubuntu-elk/elk-key.txt          сообщение после установки elasticsearch

- /ubuntu-elk/kibana.yml           /etc/kibana/kibana.yml - конфигурационный файл kibana
- /ubuntu-elk/filebeat.yml         /etc/filebeat/filebeat.yml конфигурационный файл filebeat
 
- /scrins/centos-log.jpg:          скриншот сбора логов - rsyslog, VM centos-log
                                   логи аудита с VM centoos-web
- /scrins/centos-elk-nginx.jpg:    скриншот Elastic, VM ubuntu-elk
                                   логи nginx и аудита конфига nginx c VM centos-web                      
- /scrins/ubuntu-elk-filebeat.jpg: скриншот Elastic, VM ubuntu-elk
                                   локальные логи filebeat

При установке elk использовалась инструкция:
https://www.dmosk.ru/instruktions.php?object=elk-ubuntu#clients-install-ubuntu
```

 
