# 08-ansible-03-yandex  
Netology 08-ansible-03-yandex Moiseenko A.N.  
  
Домашнее задание к занятию 3 «Использование Ansible»  
  
Подготовка к выполнению  
  
  1. Подготовьте в Yandex Cloud три хоста: для clickhouse, для vector и для lighthouse.  
  2. Репозиторий LightHouse находится по ссылке.  
  
Основная часть  
  
  1. Допишите playbook: нужно сделать ещё один play, который устанавливает и настраивает LightHouse.  
  2. При создании tasks рекомендую использовать модули: get_url, template, yum, apt.  
  3. Tasks должны: скачать статику LightHouse, установить Nginx или любой другой веб-сервер, настроить его конфиг для открытия LightHouse, запустить веб-сервер.  
  4. Подготовьте свой inventory-файл prod.yml.  
  5. Запустите ansible-lint site.yml и исправьте ошибки, если они есть.  
  6. Попробуйте запустить playbook на этом окружении с флагом --check.  
  7. Запустите playbook на prod.yml окружении с флагом --diff. Убедитесь, что изменения на системе произведены.  
  8. Повторно запустите playbook с флагом --diff и убедитесь, что playbook идемпотентен.  
  9. Подготовьте README.md-файл по своему playbook. В нём должно быть описано: что делает playbook, какие у него есть параметры и теги.  
  10. Готовый playbook выложите в свой репозиторий, поставьте тег 08-ansible-03-yandex на фиксирующий коммит, в ответ предоставьте ссылку на него.  


Решение.  

  






Playbook site.yml содержит 4 play'я task'ов которые устанавливают Clickhouse, Vector, Nginx и Lighthouse на хосты clickhouse-01, vector-01, lighthouse-01. Имена хостов и данные для аутентификации указаны в файле inventory/prod.yml   . Каждый play можно выполнить отдельно, используя тэги: Install Clickhouse, Install Vector,Install Nginx и Install LightHouse.
Плейбук использует 4 файла с переменными: 3 файла для каждой из групп хостов индивидуально:

playbook/group_vars/clickhouse/clickhouse_vars.yml
playbook/group_vars/vector/vector_vars.yaml
playbook/group_vars/lighthouse/lighthouse_vars.yaml
и один файл, применяемый для всез групп хостов:
playbook/group_vars/all/all_vars.yml
Для конфигурации Vector и Nginx используются шаблоны конфигов:

playbook/templates/vector/vector.yaml.j2
playbook/templates/nginx/ligthouse.conf.j2
