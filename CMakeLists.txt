cmake_minimum_required(VERSION 3.10)
project(OpenGLProject)

set(CMAKE_CXX_STANDARD 17)

# Không cần thiết cài đặt DEPENDENCIES_PATH và CMAKE_MODULE_PATH nếu không dùng FindGLAD.cmake
# set(DEPENDENCIES_PATH ${CMAKE_CURRENT_SOURCE_DIR}/libs)
# set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} ${CMAKE_CURRENT_SOURCE_DIR}/cmake)

add_subdirectory(libs/glfw)

# === GLAD ===
# Thêm Glad như một thư viện tĩnh từ các file nguồn của nó
# glad.c nằm trong libs/glad/src/
add_library(glad STATIC libs/glad/src/glad.c)

# Thiết lập các thư mục include cho Glad
# glad.h nằm trong libs/glad/include/
target_include_directories(glad PUBLIC libs/glad/include) # Dùng PUBLIC để các mục tiêu khác cũng có thể thấy Glad headers

# =============

add_executable(OpenGLApp code/main.cpp)

target_link_libraries(OpenGLApp PRIVATE 
    glfw 
    glad # Liên kết với thư viện glad đã tạo ở trên
)

target_include_directories(OpenGLApp PRIVATE
    libs/glfw/include
    # Không cần ${GLAD_INCLUDE_PATH} nữa vì chúng ta đã tự thêm Glad
    libs/glm
)