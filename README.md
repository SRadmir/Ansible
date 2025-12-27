# Отчет по лабораторной работе: Основы Ansible

## Цель работы
Освоить базовые принципы работы с Ansible для автоматизации управления инфраструктурой.

## Выполненные этапы

### 1. Установка Ansible на macOS
```bash
brew install python3
pip3 install ansible
ansible --version
```
### 2. Генерация SSH-ключей
```
ssh-keygen -t rsa -b 4096 -f ~/.ssh/ansible_key -N ""
chmod 600 ~/.ssh/ansible_key
```

### 3 Развертывание управляемого контейнера
```
# docker-compose.yml
version: '3.8'
services:
  managed-host:
    build: .
    container_name: ansible-managed-host
    ports:
      - "2222:22"
    restart: unless-stopped
```
### 4 Настройка инвентаря Ansible
```
[managed_hosts]
managed1 ansible_host=127.0.0.1 ansible_port=2222 ansible_user=ansible ansible_ssh_private_key_file=~/.ssh/ansible_key
```
### 5 Выполнение заданий

Получена информация о количестве ядер процессора
```
ansible -i inventory.ini managed1 -m setup -a "filter=ansible_processor_cores"
```
![](https://github.com/SRadmir/Ansible/blob/main/2025-12-27%2011.04.12.jpg)


Вывод информации о свободном месте на диске
```
ansible -i inventory.ini managed1 -m command -a "df -h"
```
![](https://github.com/SRadmir/Ansible/blob/main/2.jpg)

Создан тестовый файл на удаленном хосте
```
ansible -i inventory.ini managed1 -m copy -a "content='Hello from macOS\n' dest=/tmp/test.txt"
```
![](https://github.com/SRadmir/Ansible/blob/main/3.jpg)

### Вывод 
Лабораторная работа успешно завершена. Освоены базовые навыки работы с Ansible: установка, настройка инвентаря, выполнение ad-hoc команд и создание playbook. Полученный опыт позволяет применять Ansible для автоматизации управления инфраструктурой.


