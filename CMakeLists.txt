cmake_minimum_required(VERSION 3.1)

# Enable C++11
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED TRUE)

project(testproject)

# Find includes in corresponding build directories
set(CMAKE_INCLUDE_CURRENT_DIR ON)
# Instruct CMake to run moc automatically when needed.
set(CMAKE_AUTOMOC ON)

find_package(OpenCV REQUIRED)

include_directories(${OpenCV_INCLUDE_DIRS})
find_package(Qt5 COMPONENTS REQUIRED Quick Qml Core Gui Widgets)

# If the package has been found, several variables will
# be set, you can find the full list with descriptions
# in the OpenCVConfig.cmake file.
# Print some message showing some of them
message(STATUS "OpenCV library status:")
message(STATUS "    config: ${OpenCV_DIR}")
message(STATUS "    version: ${OpenCV_VERSION}")
message(STATUS "    libraries: ${OpenCV_LIBS}")
message(STATUS "    include path: ${OpenCV_INCLUDE_DIRS}")

set(SOURCES
  main.cpp
  mainwindow.cpp
)

set(FORMS
  mainwindow.ui
)
qt5_wrap_ui(FORM_H ${FORMS})

# Tell CMake to create the helloworld executable
add_executable(helloworld ${SOURCES} ${FORM_H})

# Use the Widgets module from Qt 5.
target_link_libraries(helloworld Qt5::Widgets)

