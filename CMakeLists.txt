cmake_minimum_required(VERSION 4.0)

project(Genie)


add_subdirectory(vendor/glfw)
add_subdirectory(vendor/glad)
add_subdirectory(vendor/imgui)
add_subdirectory(vendor/glm)

# set(SRC
#     "src/*.h"
#     "src/*.cpp"
# )

# add_executable(${PROJECT_NAME} SRC)

set(ASSETS_SOURCE_DIR "${CMAKE_CURRENT_SOURCE_DIR}/assets")

set(ASSETS_DESTINATION_DIR "${CMAKE_BINARY_DIR}")

# add_custom_command(Genie PRE_BUILD COMMAND ${CMAKE_COMMAND} -E copy_directory "${ASSETS_SOURCE_DIR}" "${ASSETS_DESTINATION_DIR}")
# COMMENT "Copying assets to build directory..."

add_executable(${PROJECT_NAME} src/main.cpp src/shader.h)

add_custom_command(
    TARGET Genie
    POST_BUILD
    COMMAND ${CMAKE_COMMAND} -E copy_directory
        "${ASSETS_SOURCE_DIR}"
        #"${ASSETS_DESTINATION_DIR}/${CMAKE_CONFIGURATION_TYPE}/assets"
        "${ASSETS_DESTINATION_DIR}/Debug/assets"
    COMMENT "Copying assets to build directory..."
)

find_package(OpenGL REQUIRED)
target_link_libraries(${PROJECT_NAME}
    PRIVATE
    glad
    glfw
    imgui
    glm
    OpenGL::GL
)

target_include_directories(${PROJECT_NAME}
    PRIVATE
    vendor/glad/include
    vendor/glfw/include
    vendor/imgui
    vendor/glm
)