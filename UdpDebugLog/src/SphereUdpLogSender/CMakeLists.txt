#  Copyright (c) Microsoft Corporation. All rights reserved.
#  Licensed under the MIT License.

cmake_minimum_required(VERSION 3.10)

project(SphereUdpLogSender C)

azsphere_configure_tools(TOOLS_REVISION "21.01")
azsphere_configure_api(TARGET_API_SET "8")

add_executable(${PROJECT_NAME} 
	main.c 
	udplog.c
	)

target_link_libraries(${PROJECT_NAME} applibs gcc_s c)

# comment out the add_compile_definitions to use the standard Log_Debug
add_compile_definitions(USE_SOCKET_LOG)

# Referencing the HardwareDefinitions directly from the SDK, so to not carry them over
azsphere_target_hardware_definition(${PROJECT_NAME} TARGET_DIRECTORY "${AZURE_SPHERE_SDK_PATH}/HardwareDefinitions" TARGET_DEFINITION "mt3620.json")

azsphere_target_add_image_package(${PROJECT_NAME})
