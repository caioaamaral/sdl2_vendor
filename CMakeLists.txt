cmake_minimum_required(VERSION 3.16.3)
project(sdl2_vendor)

set(sdl_components)

add_subdirectory(SDL2) # SDL2::SDL2 and SDL2::SDL2main
add_subdirectory(SDL2_image) # SDL2::Image
add_subdirectory(SDL2_ttf) # SDL2::TTF

# export targets
install(EXPORT ${PROJECT_NAME}Targets
  FILE ${PROJECT_NAME}Targets.cmake
  NAMESPACE SDL2::
  DESTINATION "share/${PROJECT_NAME}/cmake"
)

# export package
include(CMakePackageConfigHelpers)

configure_package_config_file(Config.cmake.in
  ${CMAKE_CURRENT_BINARY_DIR}/${PROJECT_NAME}Config.cmake
  INSTALL_DESTINATION "share/${PROJECT_NAME}/cmake"
)

install(FILES "${CMAKE_CURRENT_BINARY_DIR}/${PROJECT_NAME}Config.cmake"
  DESTINATION "share/${PROJECT_NAME}/cmake"
)
