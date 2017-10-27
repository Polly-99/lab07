## Laboratory work VII

Данная лабораторная работа посвещена изучению систем документирования исходного кода на примере **Doxygen**

```ShellSession
$ open https://www.stack.nl/~dimitri/doxygen/manual/index.html
```

## Tasks

- [x] 1. Создать публичный репозиторий с названием **lab07** на сервисе **GitHub**
- [x] 2. Выполнить инструкцию учебного материала
- [x] 3. Ознакомиться со ссылками учебного материала
- [x] 4. Составить отчет и отправить ссылку личным сообщением в **Slack**

## Tutorial

```ShellSession
$ export GITHUB_USERNAME=Polly-99
$ alias edit=vi
```
Создание директории новой лабы на основе предыдущей
```ShellSession
$ git clone https://github.com/${GITHUB_USERNAME}/lab06 lab07
$ cd lab07
$ git remote remove origin
$ git remote add origin https://github.com/${GITHUB_USERNAME}/lab07
```
Создание документации
```ShellSession
$ mkdir docs # создание директории
$ doxygen -g docs/doxygen.conf #создание doxygen.conf
$ cat docs/doxygen.conf # вывод файла doxygen.conf
```
Внесение изменений в doxygen.conf
```ShellSession
$ sed -i 's/\(PROJECT_NAME.*=\).*$/\1 print/g' docs/doxygen.conf
$ sed -i 's/\(EXAMPLE_PATH.*=\).*$/\1 examples/g' docs/doxygen.conf
$ sed -i 's/\(INCLUDE_PATH.*=\).*$/\1 examples/g' docs/doxygen.conf
$ sed -i 's/\(INPUT *=\).*$/\1 README.md include/g' docs/doxygen.conf
$ sed -i 's/\(USE_MDFILE_AS_MAINPAGE.*=\).*$/\1 README.md/g' docs/doxygen.conf
$ sed -i 's/\(OUTPUT_DIRECTORY.*=\).*$/\1 docs/g' docs/doxygen.conf
```

Замена "lab06" на "lab07" в файле README.md
```ShellSession
$ sed -i 's/lab06/lab07/g' README.md
```

```ShellSession
# документируем функции print 
$ edit include/print.hpp
```
Коммит изменений
```ShellSession
$ git add .
$ git commit -m"added doxygen.conf"
$ git push origin master
```
Вход в travis, активация проекта
```ShellSession
$ travis login --auto
$ travis enable
```

Создание новой ветки
```
$ doxygen docs/doxygen.conf
$ ls | grep "[^docs]" | xargs rm -rf ##Удаление всех файлов которые не содержат "docs"
$ mv docs/html/* . && rm -rf docs #Перемещение html в текущую директорию и удаление директории docs
$ git checkout -b gh-pages #создание ветви gh-pages и переключение на нее
$ git add . 
$ git commit -m"added documentation" 
$ git push origin gh-pages 
$ git checkout master # снова переключаемся на ветвь master
```

```ShellSession
$ mkdir artifacts && cd artifacts
$ screencapture -T 10 screenshot.jpg # или png
<Command>-T
$ open https://${GITHUB_USERNAME}.github.io/lab07/print_8hpp_source.html
$ gdrive upload screenshot.jpg # или png
$ SCREENSHOT_ID=`gdrive list | grep screenshot | awk '{ print $1; }'`
$ gdrive share ${SCREENSHOT_ID} --role reader --type user --email rusdevops@gmail.com
$ echo https://drive.google.com/open?id=${SCREENSHOT_ID}
```

## Report
Создание 
```ShellSession
$ cd ~/workspace/labs/
$ export LAB_NUMBER=07
$ git clone https://github.com/tp-labs/lab${LAB_NUMBER} tasks/lab${LAB_NUMBER}
$ mkdir reports/lab${LAB_NUMBER}
$ cp tasks/lab${LAB_NUMBER}/README.md reports/lab${LAB_NUMBER}/REPORT.md
$ cd reports/lab${LAB_NUMBER}
$ edit REPORT.md
$ gistup -m "lab${LAB_NUMBER}"
```
