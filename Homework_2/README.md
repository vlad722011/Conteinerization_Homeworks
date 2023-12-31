# Курс - "Контейнеризация"
## Домашнее задание к семинару 2.
## Выполнил Бурсаев Владислав, группа 3775.

#### Первым делом подготовим систему для работы с контейнероами LXC

* Установим необходимые утилиты:

``` sudo apt install lxc ```

![Устанваливаем lxc](/Homework_2/Sourse/Установка_lxc.png)

#### Дожидаемся установки пакета и далее собственно приступим к созданию контейнера.

 * Для создания контейнера воспользуемся утилитой lxc-create с параметрами:

 ``` lxc-create -n test123 -t ubuntu ```


 ![Создаем контейнер](/Homework_2/Sourse/Cоздание_контейнера_запуск.png)


 ![Контейнер создан](/Homework_2/Sourse/Контейнер_создан.png)


* Проверим что контейнер создан. Воспользуемся утилитой:

``` lxc-ls ``` 

![Контейнер существует](/Homework_2/Sourse/Контейнер_существует.png)

![Контейнер существует](/Homework_2/Sourse/Контейнер_сущестует_2.png)

* Запустим контейнер

```lxc-start -n test123```

![Запустили контейнер](/Homework_2/Sourse/Start_conteiner.png)

![Запустили контейнер](/Homework_2/Sourse/Start.png)

* После того как контейнер запущен, можно подключиться к оболочке утилитой lxc-attach

``` lxc-attach -n test123 ```

* и посмотреть сколько памяти использует созданный контейнер

``` free -m ```

![Смотрим память](/Homework_2/Sourse/Смотрим_память_контейнера.png)

## Ограничение ресурсов контейнера на примере оперативной памяти.

* Для ограничения ресурсов контейнера необходимо редактировать конфигурационный файл контейнера.
Для этого откроем файл с конфигом контейнера в текстовом редакторе, предварительно остановив контейнер.

``` exit ```

``` lxc-stop -n test123 ```

![Остановили контейнер](/Homework_2/Sourse/Stop_conteiner.png)

``` nano /var/lib/lxc/test123/config  ```

![Файл конфига](/Homework_2/Sourse/Конфиг.png)

* Добавим параметр отвечающий за ограничение оперативной памяти.

``` lxc.cgroup2.memory.max = 256M ```

![Ограничили_память](/Homework_2/Sourse/Ограничение_памяти_2.png)

* Для применения настроек, контейнер необходимо перезапустить.

```  sudo lxc-stop -n test123  ```

```  sudo lxc-start -n test123  ```

* Теперь снова проверяем доступную контейнеру оперативную память.

``` sudo lxc-start -n test123  ```

``` lxc-attach -n teat123 ```

```   free -m  ```

![Ограниченная память у контейнера](/Homework_2/Sourse/Ограничили_память_2.png)

####   Настройки из конфигурационного файла успешно применились. 

