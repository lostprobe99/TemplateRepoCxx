# for each "src/x.cpp", generate target "x"
aux_source_directory(${PROJECT_SOURCE_DIR}/src sources)

foreach(main IN LISTS sources)
    message(STATUS "Found source file ${main}")
    get_filename_component(target ${main} NAME_WE)
    add_executable(${target} ${main})
    get_filename_component(fname ${main} NAME)
    target_compile_definitions(${target} PUBLIC FILENAME="${fname}")

    # target_link_libraries(${mainname} ${CONAN_LIBS})
    # if(CMAKE_CXX_COMPILER_ID MATCHES GNU)
    #     target_link_libraries(${mainname} pthread)
    # endif()
endforeach()