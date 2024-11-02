# Ansible Playbook for Installing Clickhouse and Vector

## Описание

Этот Ansible playbook предназначен для установки и настройки Clickhouse и Vector на целевых серверах. 

## Предварительные требования

Перед запуском playbook убедитесь, что выполнены следующие требования:

- Ansible версии 2.9 или выше установлен на контроллере.
- Управляемые узлы настроены и могут быть достигнуты через SSH.
- Имеется доступ к интернету для загрузки пакетов.

## Переменные

- `clickhouse_version`: Версия Clickhouse, которую следует установить. Задается в playbook или в инвентори файле.
- `clickhouse_packages`: Список пакетов Clickhouse для установки. Обычно включает `clickhouse-server`, `clickhouse-client` и `clickhouse-common-static`.

## Инструкции по установке

1. **Cклонируйте репозиторий:**

```shell
   git clone https://github.com/SergueiMoscow/Ansible_02.git
   cd Ansible_02
```

2. **Подготовьте инвентори файл:**

Укажите целевые хосты, добавив их в файл инвентори, например [`prod.yml`]`inventory/prod.yml`:
```yml
clickhouse:
  hosts:
    clickhouse:
      ansible_connection: docker
```


3. **Запуск playbook:**

   Выполните команду для запуска playbook:

```shell
   ansible-playbook -i inventory.ini playbook.yml
```
   
## Роли и задачи

- **Установка Clickhouse:**
  - Скачивает необходимые пакеты.
  - Устанавливает их с помощью `yum`.
  - Создаёт базу данных `logs`.

- **Установка Vector:**
  - Загружает и запускает скрипт для добавления репозитория.
  - Устанавливает Vector из репозитория.
  - Создаёт и активирует systemd сервис для Vector.

## Обработка ошибок

В playbook предусмотрены механизмы для обработки ошибок при загрузке пакетов Clickhouse. В случае неудачи с основных зеркал, playbook пытается загрузить резервный пакет.
