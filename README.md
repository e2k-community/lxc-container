# lcx_node

Роль предназначена для настройки LXC на хостах с ОС Эльбрус (версия 7.2).

## Требования

Для работы требуется:

* На сервере ОС Эльбрус версии от 7.2
* На сервере нужно установить модуль: python3-lxc (например через pip `sudo pip3 install python3-lxc`)

## Переменные используемые для настройки

Для конфигурации используются два массива:

* `containers` - структура с описанием контейнера.
* `absent_containers` - список имен контейнеров которые нужно удалить. 

### Конфигурация

Для создания контейнеров информация берется из массива `containers`, который представляет структуру следующего содержания:

```
containers:
  - name: <container name>
    template: <template name>
    opts: <lxc-create options>
    start_auto: [0|1]
```
Значения полей:
* `name` - имя создаваемого контейнера.
* `template` - имя LXC шаблона из которого будет создаваться новый контейнер.
* `opts` - опции для шаблона.
* `start_auto:` - флаг запуска контейнера при загрузке ОС. Возможные значения `0` или `1`, `0` - не запускать, `1` - запускать.

Пример конфигурации:

```
containers:
  - name: vm-test-01
    template: tar
    opts: "--imgtar /opt/e2k-comm/templates/osl-template-0.0.0.tar.gz"
    start_auto: 1
```

### Удаление ненужных контейнеров

Удаление ненужных контейнеров осуществляется через массив `absent_containers` в который заносятся имена контейнеров (поле `name` из массива `containers`).

```
absent_containers:
  - vm-test-01
  - vm-test-02
```

## Зависимости

* community.general.lxc_container

## Примеры


TODO: Примеры

## License

GNU/GPL

## Автор

Stanislav V. Emets <stas@emets.su>