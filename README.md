# how to set up Qt on WSL

## step 1:
install WSL (single PowerShell command)

run this and go through the install process
```PowerShell
  wsl --install
```

reasonable defaults - more info at [https://learn.microsoft.com/en-us/windows/wsl/install]

## step 2:
restart your computer

## step 3:
### open your newly installed WSL:
open powershell -> the tab island on top -> the dropdown -> select Ubuntu
![wsl ubuntu terminal location](https://github.com/user-attachments/assets/9bcf08f6-a2ed-4f5f-b5db-bb08fb4662d8)

### configure username and password for ubuntu
yeah do that

## step 3.5 (optional)
### test if visual apps are working:
(should spawn a pair of eyes on your screen)
(I'm not sure if this comes preinstalled now, might need to install x11apps)
```bash
apt-get install x11-apps
xeyes
```

## step 4
install a c++ compiler & cmake
```bash
sudo apt install g++
sudo apt install cmake
```

## step 5
install Qt:
this is an excerpt from my terminal history, after that qt was working

not quite sure what happened here
```bash
sudo apt install qt5-default
sudo apt update
sudo apt install qt5-default
sudo apt-mark manual qtbase5-dev qtchooser qt5-qmake qtbase5-dev-tools
sudo apt install qtbase5-dev qtchooser qt5-qmake qtbase5-dev-tools
```

## step 6
try running a simple Qt App:

CMakeLists.txt
```cmake
cmake_minimum_required(VERSION 3.22)
project(Pacman)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_AUTOMOC ON)
set(CMAKE_AUTORCC ON)
set(CMAKE_AUTOUIC ON)

# Set the path to your Qt5 installation
set(CMAKE_PREFIX_PATH "usr/lib/x86_64-linux-gnu/cmake/Qt5/Qt5Config.cmake")

find_package(Qt5 COMPONENTS
        Core
        REQUIRED)

find_package(Qt5 COMPONENTS Widgets REQUIRED)

add_executable(Pacman main.cpp)

target_link_libraries(Pacman
        Qt5::Core
        Qt5::Widgets
)
```

main.cpp
```c++
// main.cpp
#include <QApplication>
#include <QGraphicsView>
#include <QGraphicsScene>

int main(int argc, char *argv[]) {
    QApplication a(argc, argv);
    QGraphicsScene *scene = new QGraphicsScene();
    scene->setBackgroundBrush(Qt::magenta);
    QGraphicsView* view = new QGraphicsView(scene);
    view->setFixedSize(600, 600);
    view->show();
    return a.exec();
}
```

compile & run
```bash
cmake .
make
./Pacman
```

