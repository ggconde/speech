# Copyright: 2017 UC3M
# Author: Juan G Victores & Raul de santos Rico
# CopyPolicy: Released under the terms of the GNU GPL v2.0.
# 

find_package(YARP REQUIRED)
list(APPEND CMAKE_MODULE_PATH ${YARP_MODULE_PATH})
include(YarpInstallationHelpers)
yarp_configure_external_installation(roboticslab-speech)

yarp_install(FILES ymanager.ini DESTINATION ${ROBOTICSLAB-SPEECH_DATA_INSTALL_DIR})  # Cleaner than ${ROBOTICSLAB-SPEECH_ROBOTS_INSTALL_DIR}/../ or similar.

### Go through single applications

add_subdirectory(speechRecognition)
