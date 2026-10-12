cmake_minimum_required(VERSION 3.8)
project(rp_simple_controller)

# Hopefully these should make the code more portable
set(CMAKE_CXX_STANDARD 14)
add_compile_options(-Wall -Wextra -Wpedantic -Werror)

# find dependencies
find_package(ament_cmake REQUIRED)
find_package(ament_cmake_target_dependencies REQUIRED)
find_package(rclcpp REQUIRED)

# Find the other dependencies [geometry_msgs and turtlesim]
# CMake locates the required packages
find_package(geometry_msgs REQUIRED)
find_package(turtlesim REQUIRED)
find_package(turtlesim_msgs REQUIRED)

# Adding new node turtle_square
add_executable(turtle_square src/turtle_square.cpp)

# Link the ament dependencies to turtle_square using the
# ament_target_dependencies function.
# Remember to link the dependencies, you should write:
# ament_target_dependencies(target_name dependency1 dependency2 ...)
# Connects the rtarget (what we are trying to make here which is turtle_square)
# to the dependencies so that turtle_square can use them
target_link_libraries(turtle_square
  rclcpp::rclcpp
  geometry_msgs::geometry_msgs
  turtlesim_msgs::turtlesim_msgs
)

# Install the executable to the lib/${PROJECT_NAME} directory
install(
	TARGETS
	turtle_square
	DESTINATION
	lib/${PROJECT_NAME}
)

# Finaly, call ament_package to make the package.
# This should be the last line in the CMakeLists.txt file.
ament_package()
