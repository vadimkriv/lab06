## Laboratory work VI

Данная лабораторная работа посвещена изучению средств пакетирования на примере **CPack**

```sh
$ open https://cmake.org/Wiki/CMake:CPackPackageGenerators
```

## Tasks

- [ ] 1. Создать публичный репозиторий с названием **lab06** на сервисе **GitHub**
- [ ] 2. Выполнить инструкцию учебного материала
- [ ] 3. Ознакомиться со ссылками учебного материала
- [ ] 4. Составить отчет и отправить ссылку личным сообщением в **Slack**


## Report

```sh
vadim@vadim-VirtualBox:~$ export GITHUB_USERNAME=polenk0
vadim@vadim-VirtualBox:~$ export GITHUB_EMAIL=gadik13377@gmail.com
vadim@vadim-VirtualBox:~$ alias edit=nano
vadim@vadim-VirtualBox:~$ alias gsed=sed
vadim@vadim-VirtualBox:~$ cd ${GITHUB_USERNAME}/workspace
vadim@vadim-VirtualBox:~/polenk0/workspace$ pushd .
~/polenk0/workspace ~/polenk0/workspace
vadim@vadim-VirtualBox:~/polenk0/workspace$ source scripts/activate
vadim@vadim-VirtualBox:~/polenk0/workspace$ git clone https://github.com/${GITHUB_USERNAME}/lab05 projects/lab06
Клонирование в «projects/lab06»...
remote: Enumerating objects: 35, done.
remote: Counting objects: 100% (35/35), done.
remote: Compressing objects: 100% (19/19), done.
remote: Total 35 (delta 8), reused 35 (delta 8), pack-reused 0
Получение объектов: 100% (35/35), 5.60 КиБ | 5.60 МиБ/с, готово.
Определение изменений: 100% (8/8), готово.
vadim@vadim-VirtualBox:~/polenk0/workspace$ cd projects/lab06
vadim@vadim-VirtualBox:~/polenk0/workspace/projects/lab06$ git remote remove origin
vadim@vadim-VirtualBox:~/polenk0/workspace/projects/lab06$ git remote add origin https://github.com/${GITHUB_USERNAME}/lab06
vadim@vadim-VirtualBox:~/polenk0/workspace/projects/lab06$ gsed -i '/project(print)/a\
> set(PRINT_VERSION_STRING "v\${PRINT_VERSION}")
> ' CMakeLists.txt
vadim@vadim-VirtualBox:~/polenk0/workspace/projects/lab06$ gsed -i '/project(print)/a\
set(PRINT_VERSION\
  \${PRINT_VERSION_MAJOR}.\${PRINT_VERSION_MINOR}.\${PRINT_VERSION_PATCH}.\${PRINT_VERSION_TWEAK})
' CMakeLists.txt
vadim@vadim-VirtualBox:~/polenk0/workspace/projects/lab06$ gsed -i '/project(print)/a\
set(PRINT_VERSION_TWEAK 0)
' CMakeLists.txt
vadim@vadim-VirtualBox:~/polenk0/workspace/projects/lab06$ gsed -i '/project(print)/a\
set(PRINT_VERSION_PATCH 0)
' CMakeLists.txt
vadim@vadim-VirtualBox:~/polenk0/workspace/projects/lab06$ gsed -i '/project(print)/a\
set(PRINT_VERSION_MINOR 1)
' CMakeLists.txt
vadim@vadim-VirtualBox:~/polenk0/workspace/projects/lab06$ gsed -i '/project(print)/a\
set(PRINT_VERSION_MAJOR 0)
' CMakeLists.txt
vadim@vadim-VirtualBox:~/polenk0/workspace/projects/lab06$ git diff
diff --git a/CMakeLists.txt b/CMakeLists.txt
index d69c488..b89b76c 100644
--- a/CMakeLists.txt
+++ b/CMakeLists.txt
@@ -7,6 +7,13 @@ option(BUILD_EXAMPLES "Build examples" OFF)
 option(BUILD_TESTS "Build tests" OFF)
 
 project(print)
+set(PRINT_VERSION_MAJOR 0)
+set(PRINT_VERSION_MINOR 1)
+set(PRINT_VERSION_PATCH 0)
+set(PRINT_VERSION_TWEAK 0)
+set(PRINT_VERSION
+  ${PRINT_VERSION_MAJOR}.${PRINT_VERSION_MINOR}.${PRINT_VERSION_PATCH}.${PRINT_VERSION_TWEAK})
+set(PRINT_VERSION_STRING "v${PRINT_VERSION}")
 
 add_library(print STATIC ${CMAKE_CURRENT_SOURCE_DIR}/sources/print.cpp)
 
vadim@vadim-VirtualBox:~/polenk0/workspace/projects/lab06$ touch DESCRIPTION && edit DESCRIPTION
vadim@vadim-VirtualBox:~/polenk0/workspace/projects/lab06$ touch ChangeLog.md
vadim@vadim-VirtualBox:~/polenk0/workspace/projects/lab06$ export DATE="`LANG=en_US date +'%a %b %d %Y'`"
vadim@vadim-VirtualBox:~/polenk0/workspace/projects/lab06$ cat > ChangeLog.md <<EOF
> * ${DATE} ${GITHUB_USERNAME} <${GITHUB_EMAIL}> 0.1.0.0
- Initial RPM release
> EOF
vadim@vadim-VirtualBox:~/polenk0/workspace/projects/lab06$ cat > CPackConfig.cmake <<EOF
> include(InstallRequiredSystemLibraries)
> EOF
vadim@vadim-VirtualBox:~/polenk0/workspace/projects/lab06$ cat >> CPackConfig.cmake <<EOF
> set(CPACK_PACKAGE_CONTACT ${GITHUB_EMAIL})
set(CPACK_PACKAGE_VERSION_MAJOR \${PRINT_VERSION_MAJOR})
set(CPACK_PACKAGE_VERSION_MINOR \${PRINT_VERSION_MINOR})
set(CPACK_PACKAGE_VERSION_PATCH \${PRINT_VERSION_PATCH})
set(CPACK_PACKAGE_VERSION_TWEAK \${PRINT_VERSION_TWEAK})
set(CPACK_PACKAGE_VERSION \${PRINT_VERSION})
set(CPACK_PACKAGE_DESCRIPTION_FILE \${CMAKE_CURRENT_SOURCE_DIR}/DESCRIPTION)
set(CPACK_PACKAGE_DESCRIPTION_SUMMARY "static C++ library for printing")
> EOF
vadim@vadim-VirtualBox:~/polenk0/workspace/projects/lab06$ cat >> CPackConfig.cmake <<EOF
> set(CPACK_RESOURCE_FILE_LICENSE \${CMAKE_CURRENT_SOURCE_DIR}/LICENSE)
set(CPACK_RESOURCE_FILE_README \${CMAKE_CURRENT_SOURCE_DIR}/README.md)
> EOF
vadim@vadim-VirtualBox:~/polenk0/workspace/projects/lab06$ cat >> CPackConfig.cmake <<EOF
> set(CPACK_RPM_PACKAGE_NAME "print-devel")
set(CPACK_RPM_PACKAGE_LICENSE "MIT")
set(CPACK_RPM_PACKAGE_GROUP "print")
set(CPACK_RPM_CHANGELOG_FILE \${CMAKE_CURRENT_SOURCE_DIR}/ChangeLog.md)
set(CPACK_RPM_PACKAGE_RELEASE 1)
> EOF
vadim@vadim-VirtualBox:~/polenk0/workspace/projects/lab06$ cat >> CPackConfig.cmake <<EOF
> set(CPACK_DEBIAN_PACKAGE_NAME "libprint-dev")
set(CPACK_DEBIAN_PACKAGE_PREDEPENDS "cmake >= 3.0")
set(CPACK_DEBIAN_PACKAGE_RELEASE 1)
> EOF
vadim@vadim-VirtualBox:~/polenk0/workspace/projects/lab06$ cat >> CPackConfig.cmake <<EOF
> include(CPack)
> EOF
vadim@vadim-VirtualBox:~/polenk0/workspace/projects/lab06$ cat >> CMakeLists.txt <<EOF
> include(CPackConfig.cmake)
> EOF
vadim@vadim-VirtualBox:~/polenk0/workspace/projects/lab06$ gsed -i 's/lab05/lab06/g' README.md
vadim@vadim-VirtualBox:~/polenk0/workspace/projects/lab06$ git add .
vadim@vadim-VirtualBox:~/polenk0/workspace/projects/lab06$ git commit -m"added cpack config"
[master 783f09d] added cpack config
 4 files changed, 30 insertions(+)
 create mode 100644 CPackConfig.cmake
 create mode 100644 ChangeLog.md
 create mode 100644 DESCRIPTION
vadim@vadim-VirtualBox:~/polenk0/workspace/projects/lab06$ git tag v0.1.0.0
vadim@vadim-VirtualBox:~/polenk0/workspace/projects/lab06$ git push origin master --tags
Перечисление объектов: 40, готово.
Подсчет объектов: 100% (40/40), готово.
При сжатии изменений используется до 8 потоков
Сжатие объектов: 100% (24/24), готово.
Запись объектов: 100% (40/40), 6.44 КиБ | 6.44 МиБ/с, готово.
Всего 40 (изменений 10), повторно использовано 33 (изменений 8), повторно использовано пакетов 0
remote: Resolving deltas: 100% (10/10), done.
To https://github.com/polenk0/lab06
 * [new branch]      master -> master
 * [new tag]         v0.1.0.0 -> v0.1.0.0
vadim@vadim-VirtualBox:~/polenk0/workspace/projects/lab06$ cmake -H. -B_build
CMake Deprecation Warning at CMakeLists.txt:1 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.


-- The C compiler identification is GNU 13.2.0
-- The CXX compiler identification is GNU 13.2.0
-- Detecting C compiler ABI info
-- Detecting C compiler ABI info - done
-- Check for working C compiler: /usr/bin/cc - skipped
-- Detecting C compile features
-- Detecting C compile features - done
-- Detecting CXX compiler ABI info
-- Detecting CXX compiler ABI info - done
-- Check for working CXX compiler: /usr/bin/c++ - skipped
-- Detecting CXX compile features
-- Detecting CXX compile features - done
-- Configuring done (0.5s)
-- Generating done (0.0s)
-- Build files have been written to: /home/vadim/polenk0/workspace/projects/lab06/_build
vadim@vadim-VirtualBox:~/polenk0/workspace/projects/lab06$ cmake --build _build
[ 50%] Building CXX object CMakeFiles/print.dir/sources/print.cpp.o
[100%] Linking CXX static library libprint.a
[100%] Built target print
vadim@vadim-VirtualBox:~/polenk0/workspace/projects/lab06$ cd _build
vadim@vadim-VirtualBox:~/polenk0/workspace/projects/lab06/_build$ cpack -G "TGZ"
CPack: Create package using TGZ
CPack: Install projects
CPack: - Run preinstall target for: print
CPack: - Install project: print []
CPack: Create package
CPack: - package: /home/vadim/polenk0/workspace/projects/lab06/_build/print-0.1.0.0-Linux.tar.gz generated.
vadim@vadim-VirtualBox:~/polenk0/workspace/projects/lab06/_build$ cd ..
vadim@vadim-VirtualBox:~/polenk0/workspace/projects/lab06$ cmake -H. -B_build -DCPACK_GENERATOR="TGZ"
CMake Deprecation Warning at CMakeLists.txt:1 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.


-- Configuring done (0.0s)
-- Generating done (0.0s)
-- Build files have been written to: /home/vadim/polenk0/workspace/projects/lab06/_build
vadim@vadim-VirtualBox:~/polenk0/workspace/projects/lab06$ cmake --build _build --target package
[100%] Built target print
Run CPack packaging tool...
CPack: Create package using TGZ
CPack: Install projects
CPack: - Run preinstall target for: print
CPack: - Install project: print []
CPack: Create package
CPack: - package: /home/vadim/polenk0/workspace/projects/lab06/_build/print-0.1.0.0-Linux.tar.gz generated.
vadim@vadim-VirtualBox:~/polenk0/workspace/projects/lab06$ mkdir artifacts
vadim@vadim-VirtualBox:~/polenk0/workspace/projects/lab06$ mv _build/*.tar.gz artifacts
vadim@vadim-VirtualBox:~/polenk0/workspace/projects/lab06$ tree artifacts
artifacts
└── print-0.1.0.0-Linux.tar.gz

1 directory, 1 file
vadim@vadim-VirtualBox:~/polenk0/workspace/projects/lab06$ popd
~/polenk0/workspace
vadim@vadim-VirtualBox:~/polenk0/workspace$ export LAB_NUMBER=06
vadim@vadim-VirtualBox:~/polenk0/workspace$ git clone https://github.com/tp-labs/lab${LAB_NUMBER} tasks/lab${LAB_NUMBER}
Клонирование в «tasks/lab06»...
remote: Enumerating objects: 117, done.
remote: Counting objects: 100% (37/37), done.
remote: Compressing objects: 100% (4/4), done.
remote: Total 117 (delta 35), reused 33 (delta 33), pack-reused 80
Получение объектов: 100% (117/117), 1.33 МиБ | 2.69 МиБ/с, готово.
Определение изменений: 100% (36/36), готово.
vadim@vadim-VirtualBox:~/polenk0/workspace$ mkdir reports/lab${LAB_NUMBER}
vadim@vadim-VirtualBox:~/polenk0/workspace$ cp tasks/lab${LAB_NUMBER}/README.md reports/lab${LAB_NUMBER}/REPORT.md
vadim@vadim-VirtualBox:~/polenk0/workspace$ cd reports/lab${LAB_NUMBER}
vadim@vadim-VirtualBox:~/polenk0/workspace/reports/lab06$ edit REPORT.md
vadim@vadim-VirtualBox:~/polenk0/workspace/reports/lab06$ gist REPORT.md
```

## Homework

После того, как вы настроили взаимодействие с системой непрерывной интеграции,</br>
обеспечив автоматическую сборку и тестирование ваших изменений, стоит задуматься</br>
о создание пакетов для измениний, которые помечаются тэгами (см. вкладку [releases](https://github.com/tp-labs/lab06/releases)).</br>
Пакет должен содержать приложение _solver_ из [предыдущего задания](https://github.com/tp-labs/lab03#задание-1)
Таким образом, каждый новый релиз будет состоять из следующих компонентов:
- архивы с файлами исходного кода (`.tar.gz`, `.zip`)
- пакеты с бинарным файлом _solver_ (`.deb`, `.rpm`, `.msi`, `.dmg`)

В качестве подсказки:
```sh
$ cat .travis.yml
os: osx
script:
...
- cpack -G DragNDrop # dmg

$ cat .travis.yml
os: linux
script:
...
- cpack -G DEB # deb

$ cat .travis.yml
os: linux
addons:
  apt:
    packages:
    - rpm
script:
...
- cpack -G RPM # rpm

$ cat appveyor.yml
platform:
- x86
- x64
build_script:
...
- cpack -G WIX # msi
```

Для этого нужно добавить ветвление в конфигурационные файлы для **CI** со следующей логикой:</br>
если **commit** помечен тэгом, то необходимо собрать пакеты (`DEB, RPM, WIX, DragNDrop, ...`) </br>
и разместить их на сервисе **GitHub**. (см. пример для [Travi CI](https://docs.travis-ci.com/user/deployment/releases))</br>

## Links

- [DMG](https://cmake.org/cmake/help/latest/module/CPackDMG.html)
- [DEB](https://cmake.org/cmake/help/latest/module/CPackDeb.html)
- [RPM](https://cmake.org/cmake/help/latest/module/CPackRPM.html)
- [NSIS](https://cmake.org/cmake/help/latest/module/CPackNSIS.html)

```
Copyright (c) 2015-2021 The ISC Authors
```
