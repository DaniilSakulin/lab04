Лабораторная работа №4 по ТиМП

Работу выполнил: Сакулин Даниил

1.Создаем переменные для удобства:

```
$ export GITHUB_USERNAME=DaniilSakulin
$ export GITHUB_TOKEN=bcdb004356ff6ee85f8bb134c93cb2f8d982ca43
```

2. Устанавливаем Travis:

```
$ sudo gem install travis
Successfully installed travis-1.9.1
Parsing documentation for travis-1.9.1
Done installing documentation for travis after 1 seconds
1 gem installed
```

3. Копируем предыдущую лабораторную работу:

```
$ git clone https://github.com/${GITHUB_USERNAME}/lab03-1 projects/lab04
Cloning into 'projects/lab04'...
remote: Enumerating objects: 29, done.
remote: Counting objects: 100% (29/29), done.
remote: Compressing objects: 100% (24/24), done.
remote: Total 29 (delta 8), reused 22 (delta 3), pack-reused 0
Unpacking objects: 100% (29/29), 3.80 KiB | 16.00 KiB/s, done.
```

```
$ cd projects/lab04
$ git remote remove origin
$ git remote add origin https://github.com/${GITHUB_USERNAME}/lab04
```

4. Настраиваем конфигурационный файл Travis:

```
$ cat > .travis.yml <<EOF Устанавливаем язык, в данном случае с++

language: cpp
EOF
$ cat >> .travis.yml <<EOF Добавляем скрипты

script:

команда для генерации файлов проекта

- cmake -H. -B_build -DCMAKE_INSTALL_PREFIX=_install 

команда для сборки

- cmake --build _build 

команда для запуска цели инсталляции

- cmake --build _build --target install
EOF

$ cat >> .travis.yml <<EOF указание дополнительных пакетов, которые необходимо поставить

addons:
  apt:
    sources:
      - george-edison55-precise-backports
    packages:
      - cmake
      - cmake-data
EOF
```

5. Проверяем правильность travis.yml:

```
$ travis login --github-token ${GITHUB_TOKEN} заходим в травис
Successfully logged in as DaniilSakulin!
```

```
$ travis lint проверяем
 Hooray, .travis.yml looks valid :)
 ```
 
6. Коммитим и пушим изменения:

```
$ git add .travis.yml $ git add README.md $ git commit -m "added Travis CI"
 [master 53b0b7b] added Travis CI
 1 file changed, 12 insertions(+)
 create mode 100644 .travis.yml
$ git push origin master
Enumerating objects: 32, done.
Counting objects: 100% (32/32), done.
Delta compression using up to 4 threads
Compressing objects: 100% (30/30), done.
Writing objects: 100% (32/32), 4.18 KiB | 428.00 KiB/s, done.
Total 32 (delta 9), reused 0 (delta 0)
remote: Resolving deltas: 100% (9/9), done.
To https://github.com/DaniilSakulin/lab04
 * [new branch]      master -> master
 ```
 
7.Использование других команд Travis:

```
$ travis accounts Показывает учетные записи
DaniilSakulin (DaniilSakulin): subscribed, 6 repositories
BMSTU-IU8-25 (Bmstu-iu8-25): subscribed, 12 repositories
```
```
$ travis sync Синхронизирует информацию
 synchronizing: . done
 ```
 ```
$ travis repos показывает список репозиториев
BMSTU-IU8-25/BMSTU-IU8-25.github.io
BMSTU-IU8-25/algorithmic-languages-2-lab-1
BMSTU-IU8-25/algorithmic-languages-2-lab-3
BMSTU-IU8-25/algorithmic-languages-2-lab-4
BMSTU-IU8-25/algorithmic-languages-2-lab-5
BMSTU-IU8-25/algorithmic-languages-2-project-2
BMSTU-IU8-25/algorithmic-languages-lab-4
BMSTU-IU8-25/algorithmic-languages-lab-5
BMSTU-IU8-25/algorithmic-languages-lab-6
BMSTU-IU8-25/algorithmic-languages-project-1
BMSTU-IU8-25/algorithmic-languages-project-2
BMSTU-IU8-25/simple-protection-2-task-sollution
DaniilSakulin/Daniil-
DaniilSakulin/lab02
DaniilSakulin/lab01
DaniilSakulin/lab03-1
DaniilSakulin/lab05
DaniilSakulin/lab04
```
```
$ travis enable включает репозиторий
detected repository as DaniilSakulin/lab04, is this correct? |yes| yes
DaniilSakulin/lab04: enabled :)
```
```
$ travis whatsup показывает проекты, сборки, состояние
BMSTU-IU8-25/algorithmic-languages-lab-5 passed: #23
```
```
$ travis branches показывает состояние веток
 master:  #1    passed     added Travis CI
 ```
 ```
$ travis history показывает историю
 #1 passed:       master added Travis CI
 
Homework

Создаем .travis.yml:

```
$ cat > .travis.yml <<EOF `Устанавливаем язык, в данном случае с++`
language: cpp
EOF
```
```
$ cat > .travis.yml <<EOF `Устанавливаем компилятор, в данном случае gcс`
compiler:
- gcc
EOF
```
```
$ cat > .travis.yml <<EOF `Устанавливаем ОС,в которой будет компиляция, в данном случае linux`
os:
- linux
EOF 
```
```
$ cat > .travis.yml <<EOF `загружаем и устанавливаем нужный софт`
addons:
apt:
sources:
- ubuntu-toolchain-r-test
- llvm-toolchain-precise-3.6
packages:
- g++-7
- clang-3.6
EOF  
```
```
$ cat > .travis.yml <<EOF `Скрипт`
script:
- cmake CMakeLists.txt
- cmake --build .
EOF  
```
Аналогично для appveyor.yml:
```
$ cat > .appveyor.yml <<EOF
```
```
image: Visual Studio 2015
init:
- git config --global core.autocrlf input
clone_folder: c:\projects\my-prj
platform:
- x64
configuration:
- Debug
environment:
matrix:
- TOOLCHAIN: msvc15
build_script:
- cmake CMakeLists.txt
- cmake --build .
EOF
```
