# Установка компонент

## Установка Docker
### Windows 10/11
Если вы работаете на Windows 10/11, то вам необходимо поставить Docker Desktop
по [ссылке](https://docs.docker.com/desktop/setup/install/windows-install/).

### Debian
```
# Add Docker's official GPG key:
sudo apt update
sudo apt install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/debian/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc

# Add the repository to Apt sources:
sudo tee /etc/apt/sources.list.d/docker.sources <<EOF
Types: deb
URIs: https://download.docker.com/linux/debian
Suites: $(. /etc/os-release && echo "$VERSION_CODENAME")
Components: stable
Signed-By: /etc/apt/keyrings/docker.asc
EOF

sudo apt update
```
После чего:
```
sudo apt install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

### Ubuntu
Введите следующие команды в терминал:
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
запустить окружение олимпиады. Сначала соберется контейнер, это займет до
нескольких десятков минут. После этого должно открыться окно симулятора и
запустится решение.

## Linux
Для Linux откройте терминал и перейдите в директорию с распакованным архивом данной олимпиады:
```
cd /path/to/RWB-Robotics-Olympiad-2026
```
и запустите:
```
xhost +
docker compose up
```
Должно появиться много текста, а потом должно открыться окно с манипулятором.
Если окно появилось, то все работает корректно.

## Windows
Для этого, запустите файл compose.yaml из Docker Desktop.

# Решение олимпиады
Задача данной олимпиады -- сложить все объекты, едущие по конвейру в контейнер,
стоящий рядом с ним.

Решение пишется на языке `Python` с установленными пакетами:
* numpy
* scipy
* opencv
* rclpy

Манипулятор управляется при помощи отправки команд на ROS топик `/piper/ik_target`.
Раскрыть или закрыть захват можно отправив сообщение на топик
`/piper/gripper_state`, `True` -- раскрыть захват, `False` -- закрыть захват.

С топика `/conveyor/conveyor_camera/raw` можно получить изображение, пример
описан в
`wb-software-workspace/src/solution_python/solution_python/solution.py`.

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

# Способ оценки
За взятие и поднятие объектов, а также за их помещение в контейнер начисляются
баллы.
* Взятие циллиндра -- 5 очков
* Помещение циллиндра в контейнер -- 10 очков
* Взятие коробки -- 15 очков
* Помещение коробки в контейнер -- 20 очков


