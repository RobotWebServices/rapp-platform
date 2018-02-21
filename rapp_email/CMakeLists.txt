cmake_minimum_required(VERSION 2.8.3)
project(rapp_email)

find_package(catkin REQUIRED COMPONENTS
  rospy
  rapp_utilities
  rapp_platform_ros_communications
)

catkin_package(
  LIBRARIES
  CATKIN_DEPENDS
  rospy
  rapp_utilities
  rapp_platform_ros_communications
)

include_directories(
  ${catkin_INCLUDE_DIRS}
)

catkin_python_setup()

install(TARGETS ${PROJECT_NAME}
  ARCHIVE DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
  LIBRARY DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
  RUNTIME DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
)

install(DIRECTORY cfg launch src/rapp_email
  DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION}
)

if (CATKIN_ENABLE_TESTING)
  find_package(rostest REQUIRED)
  add_rostest(tests/email_receiver_unit_tests.launch)
  add_rostest(tests/email_sender_unit_tests.launch)
endif()
