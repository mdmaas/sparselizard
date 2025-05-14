custom_add_executable_from_dir(hphi-2d ${CMAKE_CURRENT_SOURCE_DIR})
target_link_libraries(hphi-2d sparselizard)
custom_symlink_file(hphi-2d ${CMAKE_CURRENT_SOURCE_DIR} ${CMAKE_CURRENT_BINARY_DIR} "*.msh;*.geo;*.txt;*.csv;*.nas;*.slz")

