# Build widgets opcodes
set(FLTK_SKIP_OPENGL true)
find_package(FLTK)

check_deps(USE_FLTK FLTK_FOUND)
if(USE_FLTK)
    set(widgets_SRCS FL_graph.cpp winFLTK.c widgets.cpp)
    make_plugin(widgets "${widgets_SRCS}" "${FLTK_LIBRARIES}")
    target_include_directories(widgets PRIVATE ${CSOUND_INCLUDE_DIRS})
    if(NOT MSVC)
        target_link_libraries(widgets ${FLTK_BASE_LIBRARY})
        target_link_libraries(widgets ${FLTK_FORMS_LIBRARY})
        target_link_libraries(widgets ${FLTK_IMAGES_LIBRARY})
    else()
        target_link_libraries(widgets ${FLTK_LIBRARIES})
    endif()
    target_include_directories(widgets PRIVATE ${FLTK_INCLUDE_DIR})
endif()
