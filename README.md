# Встановлення пограмного забезпечення для керування робота через ROS2 у DOCKER

## Контейнер DOCKER
Створення контеру через distrobox:  
`distrobox create -n ros2 -i ubuntu:24.04`  

Перехід до конйнеру:  
`distrobox enter ros2`  
> Вхід в перше потребудеє придумати пароль для системи у DOCKER.

## Встановлення ROS2
Оновлення пакетів ситсеми:  
`sudo apt update`  
`sudo apt upgrade`  

ROS2 потребує utf-8 кодування символив.  
Вивід поточного кодування ситмволив:  
`locale`  
Якщо не utf-8 то:  
`sudo apt update && sudo apt install locales`  
`sudo locale-gen en_US en_US.UTF-8`  
`sudo update-locale LC_ALL=en_US.UTF-8 LANG=en_US.UTF-8`  
`export LANG=en_US.UTF-8`  
Перевырити знову:  
`locale`  

Вствновленя утіліт для зручної роботи з репозиторіями:  
`sudo apt install software-properties-common`  
Додаемо репозитрій universe:  
`sudo add-apt-repository universe`  
Оновленя списку доступних пакетів:  
`sudo apt update`  
Втановлення допоміжних утилит  
`sudo apt install -y curl git lsb-release gnupg`  
Отримання останої версії пакету с джерелами ROS2 утіліт та залежностей:  
`export ROS_APT_SOURCE_VERSION=$(curl -s https://api.github.com/repos/ros-infrastructure/ros-apt-source/releases/latest | grep -F "tag_name" | awk -F'"' '{print $4}')`  
Завантаження пакету с джерелами ROS2 утіліт та залежностей:  
`curl -L -o /tmp/ros2-apt-source.deb "https://github.com/ros-infrastructure/ros-apt-source/releases/download/${ROS_APT_SOURCE_VERSION}/ros2-apt-source_${ROS_APT_SOURCE_VERSION}.$(. /etc/os-release && echo ${UBUNTU_CODENAME:-${VERSION_CODENAME}})_all.deb"`  
Втсановлення завантаженого пакету джерел ROS2:  
`sudo dpkg -i /tmp/ros2-apt-source.deb`  
Оновлення пакетів ситсеми:  
`sudo apt update`  
`sudo apt upgrade`  
Встановлення ROS2 kilted:  
`sudo apt install ros-kilted-desktop`  
Активація середовищя ROS2:  
`source /opt/ros/kilted/setup.bash`  
> Цю команду потрібно ііодити кожен раз при відкриті термінала, щоб не вводити кожного разу додйте цю команду в кінец файла `.bashrc`

Запус демонстаційної задачі ROS2, для перевірки втановлення:  
`ros2 run demo_nodes_cpp talker`  
