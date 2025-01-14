# how to set up Qt on WSL

## step 1:
### install WSL (single PowerShell command)
run this and go through the install process
```PowerShell
  wsl --install
```

reasonable defaults - more info at [https://learn.microsoft.com/en-us/windows/wsl/install]

## step 2:
### restart your computer

## step 3:
### test if visual apps are working:
(should spawn a pair of eyes on your screen)
```bash
xeyes
```

## step 4
### install Qt:
this is an excerpt from my terminal history, after that qt was working

not quite sure what happened here
```bash
sudo apt install qt5-default
sudo apt update
sudo apt install qt5-default
sudo apt-mark manual qtbase5-dev qtchooser qt5-qmake qtbase5-dev-tools
sudo apt install qtbase5-dev qtchooser qt5-qmake qtbase5-dev-tools
```

## step 5
### try running a simple Qt App:
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
    m_view->setFixedSize(600, 600);
    view->show();
    return a.exec();
}
```
