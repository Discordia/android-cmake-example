project(androidcmakeexample)

cmake_minimum_required(VERSION 2.8)

include("$ENV{ANDROID_CMAKE_HOME}/android.apk.cmake" REQUIRED)

# compiler flags
set(CMAKE_CXX_FLAGS
  "-std=c++11 -ffor-scope -fno-exceptions -pipe -ffunction-sections -fdata-sections -ffast-math -pedantic -Werror -Wnon-virtual-dtor -Wsign-promo -fvisibility=hidden -fvisibility-inlines-hidden -Wstrict-null-sentinel -Os -funroll-all-loops -fpeel-loops -ftree-vectorize")

include_directories($ENV{ANDROID_NDK_HOME}/sources/android/native_app_glue)


# Sources
set(SOURCES 
  "src/main.cpp"
  "$ENV{ANDROID_NDK_HOME}/sources/android/native_app_glue/android_native_app_glue.c")

add_library(androidcmakeexample SHARED ${SOURCES})
  target_link_libraries(androidcmakeexample log android)
set_target_properties(androidcmakeexample PROPERTIES COMPILE_DEFINITIONS "ANDROID")
android_create_apk(androidcmakeexample "${CMAKE_BINARY_DIR}/apk" "${CMAKE_SOURCE_DIR}/libs" "${CMAKE_SOURCE_DIR}/android" "${CMAKE_SOURCE_DIR}/assets")

