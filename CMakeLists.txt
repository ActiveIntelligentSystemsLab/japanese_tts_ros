cmake_minimum_required(VERSION 2.8.3)
project(japanese_text_to_speech)

find_package(catkin REQUIRED
  actionlib_msgs
  genmsg
)

add_action_files(DIRECTORY action FILES Speak.action)
generate_messages(DEPENDENCIES actionlib_msgs)

catkin_package(
  CATKIN_DEPENDS actionlib actionlib_msgs
)
catkin_install_python(
  PROGRAMS 
    nodes/japanese_text_to_speech
    nodes/test_client
  DESTINATION
    ${CATKIN_PACKAGE_BIN_DESTINATION}
)
