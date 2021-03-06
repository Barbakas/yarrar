enable_testing()

include_directories(
    "${PROJECT_SOURCE_DIR}/src" 
    "${PROJECT_SOURCE_DIR}/src/yarrar"
    "${PROJECT_SOURCE_DIR}/external/catch/"
    "${PROJECT_SOURCE_DIR}/external/opencv/build/include"
    "${PROJECT_SOURCE_DIR}/external/glfw/include"
    "${PROJECT_SOURCE_DIR}/external/glew/include"
    "${PROJECT_SOURCE_DIR}/external/json11"
    "${PROJECT_SOURCE_DIR}/external/eigen")

set(SOURCE_FILES
        TestMain.cpp
        TestMarkerTracker.cpp
        TestMarkerDetector.cpp
        TestYarrarMarkerParser.cpp
        TestUtil.cpp
        TestHistoryBuffer.cpp
        TestLockableData.cpp
        TestExtendedKalmanFilter.cpp)

add_executable(testrunner ${SOURCE_FILES})
target_link_libraries(testrunner yarrar json11 ${OpenCV_LIBS})

add_test(
    NAME TestRunner
    COMMAND ${CMAKE_BINARY_DIR}/build/bin/testrunner
    WORKING_DIRECTORY ${PROJECT_SOURCE_DIR})

if(MSVC)
    include("${PROJECT_SOURCE_DIR}/cmake/windows/CopyDLLDependencies.cmake")
    copy_dll_dependencies(testrunner)
endif()
