link_libraries(libjasper)

if (HAVE_OPENGL)
  add_executable(jiv jiv.c)
endif()

add_executable(jasper jasper.c)
add_executable(imgcmp imgcmp.c)
add_executable(imginfo imginfo.c)
# FIXME: add_executable(dummy dummy.c)

if (UNIX)
  add_executable(tmrdemo tmrdemo.c) # Needs sleep()
  add_executable(dummy2 dummy2.c) # Needs getopt() and maybe more
endif()

install(TARGETS jasper RUNTIME DESTINATION bin)
