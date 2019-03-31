# cmake needs this line
cmake_minimum_required(VERSION 3.1)

# Enable C++11
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED TRUE)
set(CMAKE_AUTOMOC TRUE)
# Define project name
project(opencv_example_project)

# Find OpenCV, you may need to set OpenCV_DIR variable
# to the absolute path to the directory containing OpenCVConfig.cmake file
# via the command line or GUI
find_package(OpenCV REQUIRED)

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

include_directories(
    ${OpenCV_INCLUDE_DIRS}
)

link_directories(
    ${OpenCV_LIB_DIR}
)

# Declare the executable target built from your sources

set(CMAKE_INCLUDE_CURRENT_DIR ON)

set(project_sources 
./src/mainwindow.cpp 
./src/main.cpp
./src/featurewindow.cpp
./src/Canny.cpp
./src/Cartoonifier.cpp
./src/cornerfinder.cpp
./src/edgedetectwindow.cpp
./src/facerecognizer.cpp
./src/featuredetector.cpp
./src/featurewindow.cpp
./src/filters.cpp
./src/grabcut.cpp
./src/imagehandler.cpp
./src/imageholder.cpp
./src/laplace.cpp
./src/mainwindow.cpp
./src/morpher.cpp
./src/pixelate.cpp
./src/projectivetransforms.cpp
./src/rippleeffect.cpp
./src/sobel.cpp
./src/watershed.cpp
./src/watershedsegmenter.cpp)

set(project_headers 
./include/Canny.h
./include/Cartoonifier.h
./include/cornerfinder.h
./include/edgedetectwindow.h
./include/facerecognizer.h
./include/featuredetector.h
./include/featurewindow.h
./include/filters.h
./include/grabcut.h
./include/imagehandler.h
./include/imageholder.h
./include/laplace.h
./include/mainwindow.h
./include/morpher.h
./include/pixelate.h
./include/projectivetransforms.h
./include/rippleeffect.h
./include/sobel.h
./include/watershed.h
./include/watershedsegmenter.h
)

set(project_ui mainwindow.ui 
imageholder.ui
edgedetectwindow.ui
imageholder.ui
imagewidget.ui
featuredetectwindow.ui
featurewindow.ui)

# wrap the ui file to a c++ header
qt5_wrap_ui(ui_wrap ${project_ui})
qt5_wrap_cpp(moc_sources ${project_headers})
add_executable(opencv_example_project 
	${project_sources} 
	${project_headers}
	${ui_wrap} 
	${moc_sources})
target_link_libraries(opencv_example_project 
	PUBLIC
	Qt5::Core
	Qt5::Gui 
	Qt5::Widgets
  ${OpenCV_LIBS})


# need this to include the auto generated ui_mainwindow.h 
# file from the qt5_wrap_ui call below.
set(CMAKE_INCLUDE_CURRENT_DIR ON)