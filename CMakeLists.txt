cmake_minimum_required(VERSION 3.14)
project(dynamixel_sdk LANGUAGES CXX)

if(NOT CMAKE_CXX_STANDARD)
  set(CMAKE_CXX_STANDARD 17)
endif()

if(CMAKE_COMPILER_IS_GNUXX OR CMAKE_CXX_COMPILER_ID MATCHES "Clang")
  add_compile_options(-Wall -Wextra -Wpedantic)
endif()

include_directories(
  ${CMAKE_CURRENT_SOURCE_DIR}/include/dynamixel_sdk
)

add_library(${PROJECT_NAME} SHARED
  ${CMAKE_CURRENT_SOURCE_DIR}/src/dynamixel_sdk/group_bulk_read.cpp
  ${CMAKE_CURRENT_SOURCE_DIR}/src/dynamixel_sdk/group_sync_read.cpp
  ${CMAKE_CURRENT_SOURCE_DIR}/src/dynamixel_sdk/packet_handler.cpp
  ${CMAKE_CURRENT_SOURCE_DIR}/src/dynamixel_sdk/port_handler.cpp
  ${CMAKE_CURRENT_SOURCE_DIR}/src/dynamixel_sdk/port_handler_mac.cpp
  ${CMAKE_CURRENT_SOURCE_DIR}/src/dynamixel_sdk/protocol1_packet_handler.cpp
  ${CMAKE_CURRENT_SOURCE_DIR}/src/dynamixel_sdk/group_bulk_write.cpp
  ${CMAKE_CURRENT_SOURCE_DIR}/src/dynamixel_sdk/group_sync_write.cpp
  ${CMAKE_CURRENT_SOURCE_DIR}/src/dynamixel_sdk/port_handler_arduino.cpp
  ${CMAKE_CURRENT_SOURCE_DIR}/src/dynamixel_sdk/port_handler_linux.cpp
  ${CMAKE_CURRENT_SOURCE_DIR}/src/dynamixel_sdk/port_handler_windows.cpp
  ${CMAKE_CURRENT_SOURCE_DIR}/src/dynamixel_sdk/protocol2_packet_handler.cpp
)

target_include_directories(${PROJECT_NAME} PUBLIC
  $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>
  $<INSTALL_INTERFACE:include>
)

install(
  TARGETS ${PROJECT_NAME}
  EXPORT "export_${PROJECT_NAME}"
  ARCHIVE DESTINATION lib
  LIBRARY DESTINATION lib
  RUNTIME DESTINATION lib
  INCLUDES
)

install(
  DIRECTORY
    include/${PROJECT_NAME}/
  DESTINATION
    include/${PROJECT_NAME}
)
