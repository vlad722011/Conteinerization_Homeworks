# Курс - "Контейнеризация"
## Домашнее задание к семинару 1.
## Выполнил Бурсаев Владислав, группа 3775.
### Изоляция на уровне файловой системы - chroot
* Итак, прежде всего открываем терминал сочетанием клавиш:- Ctrl+Alt+T
![Открываем терминал](/Homework_1/Sourse/Open_terminal.png)

#### Подготовка к использованию chroot:
* Для начала, создадим каталог "testfolder" в домашнем каталоге пользователя и в этом каталоге создадим необходимые дирректории (bin/, lib/, lib64/)

![Создаем необходимые директории](/Homework_1/Sourse/Create_dirrectorys.png)

* Проверяем, что директории созданы:

![Проверяем, что директории созданы](/Homework_1/Sourse/Check_that_the_directories_have_been_created.png)

* Копируем необходимые исполняемые файлы и библиотеки в созданные директории:

![Копируем необходимые исполняемые файлы и библиотеки](/Homework_1/Sourse/Executable_files_and_necessary_libraries_for_the_command_ls.png)

* Проверяем файл bash:

![Директория bin/](/Homework_1/Sourse/bash_file_in_bin_directory.png)

* Проверяем библиотеки:

![Директория lib/](/Homework_1/Sourse/Required_libraries_in_the_directory_lib.png)
![Директория lib64/](/Homework_1/Sourse/Required_libraries_in_the_directory_lib64.png)

* Запустим команду chroot для изменения корневой папки нашей текущей среды:

![Изменяем корень](/Homework_1/Sourse/Chroot_command.png)

#### Теперь мы находимся в изолированной среде с корнем, отличным от основной файловой системы. Оболочка интерпретатора Bash запущена в этой изолированной среде. Но кроме оболочки bash, другие команды в этой среде нам пока недоступны. Для работы с другими командами, в эту среду также необходимо добавить необходимые библиотеки и исполняемые файлы. Проделаем это на примере команды ls.

* Добавим необходимые файлы и библиотеки и проверим работоспособность команды ls:

![ls команда в изолированном пространстве](/Homework_1/Sourse/Running_ls_command_in_an_isolated_environment.png)

### Пространство имён.

#### Создание Пространства Имен для Сети:
* Воспользуемся командой ip для создания сетевого пространства имен. Создадим пространство имен с именем "testns" и убедимся что оно создано:

![Создаем сетеове пространство](/Homework_1/Sourse/Creating_an_isolated_network_space.png)

* Теперь используя команду ip, мы можем выполнить процесс в созданном пространстве имен:

![выполнить процесс в созданном пространстве имен](/Homework_1/Sourse/Execute_the_process_in_the_created_namespace.png)

#### Это подобно подключению процесса к изолированному свитчу, где процесс работает в собственной виртуальной сетевой среде.

#### Изоляция и Проверка:
* Внутри изолированной среды мы можем выполнить команды, такие как ip a, чтобы увидеть сетевые настройки. Однако, поскольку в этой среде нет реальных сетевых ресурсов, мы можем увидеть только виртуальные настройки.

![ip a в изолированном сетевом пространстве](/Homework_1/Sourse/ip_a_in_isolated_environment.png)

#### Просмотр Процессов:
* Выполнив команду ps, мы можем увидеть список всех процессов в текущем пространстве имен. Однако они будут ограничены только к процессам, которые работают в данной изолированной области.

![ip a в изолированном сетевом пространстве](/Homework_1/Sourse/ip_a_in_isolated_environment.png)

### Глубокая изоляция.

#### Применяя дополнительные параметры, мы можем углубить уровень изоляции:

* Изоляция по процессам и файловой системе:

![Утилита unshare](/Homework_1/Sourse/unshare.png)

* unshare - это утилита, которая позволяет сделать более глубокую изоляцию. Каждый ключ отвечает за что то отдельное:
1. --net — ограничевает сетевое пространство имен (ip -a)
2. --mount-proc — разграничивает процессы (ps aux)
3. --fork — изолирует память
4. --pid — изолирует дерево процессов
* Формально мы находимся внутри контейнера.

![ls](/Homework_1/Sourse/ls.png) 
![ls /](/Homework_1/Sourse/root.png) 
![ps_aux](/Homework_1/Sourse/ps_aux.png)
