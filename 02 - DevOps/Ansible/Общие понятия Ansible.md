Ansible - это инструмент автоматизации, используемый для управления конфигурациями, развертывания приложений и других задач DevOps. Он позволяет упростить управление инфраструктурой благодаря декларативному подходу и использованию YAMAL-файлов

# Основные особенности
1. Безагентная архитектура:
	1. Ansible не требует установки агентов на целевых узлах
	2. Для управления используется протокол SSH
2. Простота:
	1. Файлы конфигурации (playbooks) пишутся на языке YAML, который легко читается и понимается
3. Масштабируемость:
	1. Подходит как для управления несколькими серверами, так и для сложных распределенных систем
4. Модульность:
	1. Ansible использует модули для выполнения задач (например, модули для работы с файлами, установкой пакетов, управлением сервисами  и т.д.)
5. Идемпотентность:
	1. Ansible гарантирует, что изменения вносятся только если это необходимо, предотвращая повторное выполнение действий
# Основные компоненты Ansible
1. Управляющий узел (Control Node):
	1. Сервер или ПК, где установлен Ansible
	2. Отсюда выполняются команды и плейбуки
2. Управляемые узлы (Managed Nodes):
	1. Сервера или устройства, которые контролирует Ansible
	2. Доступ к ним осуществлен по SSH
3. Инвентарь (Inventory)
	1. Список управляемых узлов (серверов)
	2. Файл по умолчанию `/etc/ansible/hosts`
Пример:
```ini
[web_servers]
server1.example.com
server2.example.com

[db_servers]
db1.example.com
```
4. Модули (Modules):
	1. Основные единицы выполнения задач. Примеры:
		1. `copy`: копирование файлов
		2. `yum`, `apt`: управление пакетами
		3. `service`: управление системными сервисами
5. Задачи (Tasks):
	1. Единичные действия, которые выполняются на узлах
	2. Определяются в плейбуках
6. Плейбуки (Playbooks):
	1. Файлы YAML, описывающие последовательность задач для выполнения
Пример:
```yaml
- hosts: web_servers
  tasks:
	  - name: Установить nginx
	    apt:
			name: nginx
			state: present
			
	  - name: Убедиться что nginx запущен
	    service:
		    name: nginx
		    state: started
```
# Принципы работы Ansible
1. Подготовка инвентаря:
	1. Создание файла инвентаря с IP-адресами или именами серверов
2. Написание плейбука:
	1. Описать какие задачи нужно выполнить, используя YAML
3. Выполнение команд
	1. Запуск плейбука: `ansible-playbook playbook.yml`
	2. Одноразовая команда: `ansible all -m ping`
	   здесь `-m` указывает модуль (например, `ping`)
# Установка Ansible
На большинстве дистрибутивов Linux Ansible можно установить через менеджер пакетов
```bash
sudo apt install ansible
```