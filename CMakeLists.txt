cmake_minimum_required(VERSION 3.16.3)
project(sdl2_vendor)

set(sdl_targets)

add_subdirectory(SDL2) # SDL2::SDL2 and SDL2::SDL2main
add_subdirectory(SDL2_image) # SDL2::Image
add_subdirectory(SDL2_ttf) # SDL2::TTF

if(NOT sdl_targets)
  message(FATAL_ERROR "No Target found for ${PROJECT_NAME}")
else()
  install(TARGETS ${sdl_targets} EXPORT ${PROJECT_NAME}Config
    # COMPONENT SDL2::SDL2 SDL2::Image
    LIBRARY DESTINATION lib
    ARCHIVE DESTINATION lib
    RUNTIME DESTINATION bin
  )
  export(TARGETS ${sdl_targets}
    NAMESPACE SDL2::
    FILE "${CMAKE_CURRENT_BINARY_DIR}/${PROJECT_NAME}Config.cmake"
  )
  install(EXPORT ${PROJECT_NAME}Config
    DESTINATION "${CMAKE_INSTALL_PREFIX}/share/${PROJECT_NAME}/cmake"
    NAMESPACE SDL2::
  )
endif()
