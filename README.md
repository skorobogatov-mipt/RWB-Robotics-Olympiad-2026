# Установка компонент
## Установка WSL
Если вы пишете данную олимпиаду на Windows 10 или Windows 11, вам необходимо
установить Windows Subsytem Linux по 
[данной инструкции](https://learn.microsoft.com/ru-ru/windows/wsl/install).
Рекоммендуется установить версию с Ubuntu 22.04.

## Установка Docker
Если вы установили WSL или уже пользуетесь Ubuntu или Debian, то при помощи `apt` установите Docker. 
Откройте терминал, если вы на Linux(я думаю, что с этим и без подсказок справитесь) или WSL, если вы на Windows:
```
wsl ~
```

После этого, установите Docker:
```
# Add Docker's official GPG key:
sudo apt update
sudo apt install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc

# Add the repository to Apt sources:
sudo tee /etc/apt/sources.list.d/docker.sources <<EOF
Types: deb
URIs: https://download.docker.com/linux/ubuntu
Suites: $(. /etc/os-release && echo "${UBUNTU_CODENAME:-$VERSION_CODENAME}")
Components: stable
Signed-By: /etc/apt/keyrings/docker.asc
EOF

sudo apt update
```
После чего:
```
sudo apt install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```


## Данный репозиторий
Данный репозиторий можно скачать как .zip архив со [страницы на
гитхабе](https://github.com/skorobogatov-mipt/Wildberries-Robotics-Olympiad-2026)
или при помощи `git clone`.

# Запуск окружений
После того, как вы скачали данный репозиторий и установили Docker, можно
запустить окружение олимпиады.
Для этого, откройте папку в которой лежит данная олимпиада в терминале WSL или
вашей системы(если вы пользуетесь Linux).

После этого, запустите в терминале команду:
```
docker compose up
```
Должно появиться много текста, а потом должно открыться окно с манипулятором.
Если окно появилось, то все работает корректно.

# Решение олимпиады
Задача данной олимпиады -- сложить все объекты, едущие по конвейру в контейнер,
стоящий рядом с ним.

Манипулятор управляется при помощи отправки команд на ROS топик `/piper/ik_target`.
Раскрыть или закрыть захват можно отправив сообщение на топик
`/piper/gripper_state`, `True` -- раскрыть захват, `False` -- закрыть захват.

Пример решения и использования топиков лежит в файле
`wb-software-workspace/src/solution_python/solution_python/solution.py`

Ваше решение должно находиться в этом файле. 

Если вы чувствуете себя продвинутым и умеете писать ROS-пакеты, то можете
писать дополнительные файлы в этом пакете, но решение целиком должно находиться
в папке `solution_python`.

# Отправка решения
Для сдачи решения, заархивируйте папку
`wb-software-workspace/src/solution_python` в .zip файл и приложите его в форме
по [ссылке](https://forms.wb.ru/f/2751184e-9c34-46b0-86ad-299a9e0d923b).

Обратите внимание, что любые файлы вне этой папки частью решения не считаются.


