# 

cmake_minimum_required (VERSION 2.6.0)

set(KEYWORD "espeakExample")

# Start a project.
project(${KEYWORD})

#set(CMAKE_BUILD_TYPE Debug)#RelWithDebInfo)
FIND_PACKAGE(YARP REQUIRED)
FIND_PACKAGE(ROBOTICSLAB_SPEECH REQUIRED)

# Search for source code.
file(GLOB folder_source *.cpp *.cc *.c)
file(GLOB folder_header *.h *.hpp)
source_group("Source Files" FILES ${folder_source})
source_group("Header Files" FILES ${folder_header})

# Automatically add include directories if needed.
foreach(header_file ${folder_header})
  get_filename_component(p ${header_file} PATH)
  include_directories(${p})
endforeach(header_file ${folder_header})

include_directories(${YARP_INCLUDE_DIRS} ${ROBOTICSLAB_SPEECH_INCLUDE_DIRS})

link_directories(${ROBOTICSLAB_SPEECH_LINK_DIRS})

# Set up our main executable.
if (folder_source)
  add_executable(${KEYWORD} ${folder_source} ${folder_header} ${ROBOTICSLAB_SPEECH_IDL_FILES})
  target_link_libraries(${KEYWORD} ${YARP_LIBRARIES} ${ROBOTICSLAB_SPEECH_LIBRARIES})
  install(TARGETS ${KEYWORD} DESTINATION bin )
else (folder_source)
  message(FATAL_ERROR "No source code files found. Please add something")
endif (folder_source)


