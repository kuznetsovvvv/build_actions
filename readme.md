##Лабораторная №4

#1)


Вы продолжаете проходить стажировку в "Formatter Inc." (см подробности).

В прошлый раз ваше задание заключалось в настройке автоматизированной системы CMake.

Сейчас вам требуется настроить систему непрерывной интеграции для библиотек и приложений, с которыми вы работали в прошлый раз.


Заходим в дирректорию 3 лабораторной работы, создаем новую последовательность дирректорий:

```bash
Команда:mkdir -p .github/workflows
```

создаем файл cmake.yml

```bash
Команда:touch cmake.yml
```
пишем в файл инструкцию по сборке на линукс:
```bash
name: CMake_Build

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]


  workflow_dispatch:

jobs:
  build:
    runs-on: ubuntu-latest
  
    
    steps:
    - name: checkout
      uses: actions/checkout@v3
    
    - name: Build a formatter library gcc
      run: |
        cmake -H. -B_build -DCMAKE_C_COMPILER=gcc
        cmake --build _build
      shell: bash
      working-directory: formatter_lib
      
    - name: Build a formatter_ex library clang
      run: |
        cmake -H. -B_build -DCMAKE_C_COMPILER=clang
        cmake --build _build
      shell: bash
      working-directory: formatter_ex_lib
      
    - name: Build a hello_world application gcc
      run: |
        cmake -H. -B_build -DCMAKE_C_COMPILER=gcc
        cmake --build _build
      shell: bash
      working-directory: hello_world_application
      
    - name: Build a solver application clang
      run: |
        cmake -H. -B_build -DCMAKE_C_COMPILER=clang
        cmake --build _build
      shell: bash
      working-directory: solver_application
```

создаем на gitub репозиторий lab4,связываем его с локальным репозиторием, сразу делаем пуш всего репозитория:
```bash
Команда:git remote remove origin
Команда:git remote add origin git@github.com:kuznetsovvvv/lab4.git
Команда:git add .
Команда:git commit -m "first commit"
Команда:git push -u origin main
```
---
```bash
Вывод:"first commit"
[main 8fce4da] first commit
 1 file changed, 15 insertions(+), 14 deletions(-)
 Вывод:Перечисление объектов: 258, готово.
Подсчет объектов: 100% (258/258), готово.
При сжатии изменений используется до 6 потоков
Сжатие объектов: 100% (231/231), готово.
Запись объектов: 100% (258/258), 1.10 МиБ | 13.58 МиБ/с, готово.
Всего 258 (изменений 128), повторно использовано 0 (изменений 0), повторно использовано пакетов 0
remote: Resolving deltas: 100% (128/128), done.
To github.com:kuznetsovvvv/lab4.git
 * [new branch]      main -> main
Ветка «main» отслеживает внешнюю ветку «main» из «origin».
```
Проверяем на удаленном репозитории, что сборка прошла успешно.

#2)
Также создаем в дирректории .github/workflows файл cmake2.yml для сборки на Windows и прописываем в него:
```bash
name: CMake_Build

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]


  workflow_dispatch:

jobs:
  build:
    runs-on: windows-latest
  
    
    steps:
    - name: checkout
      uses: actions/checkout@v3
    
    - name: Build a formatter library gcc
      run: |
        cmake -H. -B_build -DCMAKE_C_COMPILER=gcc
        cmake --build _build
      shell: bash
      working-directory: formatter_lib
      
    - name: Build a formatter_ex library clang
      run: |
        cmake -H. -B_build -DCMAKE_C_COMPILER=clang
        cmake --build _build
      shell: bash
      working-directory: formatter_ex_lib
      
    - name: Build a hello_world application gcc
      run: |
        cmake -H. -B_build -DCMAKE_C_COMPILER=gcc
        cmake --build _build
      shell: bash
      working-directory: hello_world_application
      
    - name: Build a solver application clang
      run: |
        cmake -H. -B_build -DCMAKE_C_COMPILER=clang
        cmake --build _build
      shell: bash
      working-directory: solver_application

```
Также делаем коммит в удаленный репозиторий и проверяем, что все собралось.

