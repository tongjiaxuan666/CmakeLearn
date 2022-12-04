cmake_minimum_required(VERSION 3.0)
# set the project name
project(Tutorial VERSION 1.0)
# specify the C++ standard
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED True)
configure_file(TutorialConfig.h.in TutorialConfig.h)

SET(SRC_LIST tutorial.cpp)
if(USE_MYMATH)
	add_subdirectory(MathFunctions)
  	list(APPEND EXTRA_LIBS MathFunctions)
  	list(APPEND EXTRA_INCLUDES ${PROJECT_SOURCE_DIR}/MathFunctions)
endif()
# add the executable
add_executable(${PROJECT_NAME} ${SRC_LIST})
target_link_libraries(${PROJECT_NAME} PUBLIC ${EXTRA_LIBS})
target_include_directories(${PROJECT_NAME} PUBLIC
                           ${PROJECT_BINARY_DIR}
			   ${EXTRA_INCLUDES}
                           )
option(USE_MYMATH "Use tutorial provided math implementation" ON)
