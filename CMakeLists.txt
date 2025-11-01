cmake_minimum_required(VERSION 3.15)

project(Genie)


add_subdirectory(vendor/glfw)
add_subdirectory(vendor/glad)

add_executable(${PROJECT_NAME}
    src/main.cpp
)

find_package(OpenGL REQUIRED)
target_link_libraries(${PROJECT_NAME}
    PRIVATE
    glad
    glfw
    OpenGL::GL
)

target_include_directories(${PROJECT_NAME}
    PRIVATE
    vendor/glad/include
    vendor/glfw/include
)