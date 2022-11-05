cmake_minimum_required(VERSION 3.5)
project(japanese_text_to_speech)

#find_package(catkin REQUIRED
#  actionlib_msgs
#  genmsg
#)
#
#add_action_files(DIRECTORY action FILES Speak.action)
#generate_messages(DEPENDENCIES actionlib_msgs)
#
#catkin_package(
#  CATKIN_DEPENDS actionlib actionlib_msgs
#)
#catkin_install_python(
#  PROGRAMS
#    nodes/japanese_text_to_speech
#    nodes/test_client
#  DESTINATION
#    ${CATKIN_PACKAGE_BIN_DESTINATION}
#)

# Default to C99
if(NOT CMAKE_C_STANDARD)
  set(CMAKE_C_STANDARD 99)
endif()

# Default to C++14
if(NOT CMAKE_CXX_STANDARD)
  set(CMAKE_CXX_STANDARD 14)
endif()

if(CMAKE_COMPILER_IS_GNUCXX OR CMAKE_CXX_COMPILER_ID MATCHES "Clang")
  add_compile_options(-Wall -Wextra -Wpedantic)
endif()

# find dependencies
find_package(ament_cmake REQUIRED)
find_package(ament_cmake_python REQUIRED)
find_package(builtin_interfaces REQUIRED)
find_package(rosidl_default_generators REQUIRED)

#ament_python_install_package(nodes)

### ここにメッセージやサービスのファイルを記述 ###
rosidl_generate_interfaces(${PROJECT_NAME}
  "action/Speak.action"
  DEPENDENCIES builtin_interfaces
)

# Install Python executables
install(PROGRAMS
  nodes/japanese_text_to_speech
  nodes/test_client
  DESTINATION lib/${PROJECT_NAME}
  )

if(BUILD_TESTING)
  find_package(ament_lint_auto REQUIRED)
  ament_lint_auto_find_test_dependencies()
endif()

ament_export_dependencies(rosidl_default_runtime)
ament_package()
