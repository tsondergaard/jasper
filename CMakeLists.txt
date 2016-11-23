cmake_minimum_required(VERSION 3.2.0)

# FIXME: Find OpenGL (HAVE_OPENGL)
# FIXME: Find libjpeg (HAVE_LIBJPEG)

if(CMAKE_C_COMPILER MATCHES cl)
    if(NOT BUILD_SHARED_LIBS)
        string(REPLACE "/Zi" "/Z7" CMAKE_C_FLAGS_DEBUG "${CMAKE_C_FLAGS_DEBUG}")
        string(REPLACE "/Zi" "/Z7" CMAKE_C_FLAGS_RELWITHDEBINFO "${CMAKE_C_FLAGS_RELWITHDEBINFO}")
        string(REPLACE "/Zi" "/Z7" CMAKE_CXX_FLAGS_DEBUG "${CMAKE_CXX_FLAGS_DEBUG}")
        string(REPLACE "/Zi" "/Z7" CMAKE_CXX_FLAGS_RELWITHDEBINFO "${CMAKE_CXX_FLAGS_RELWITHDEBINFO}")
    endif()
endif()

add_subdirectory(src/libjasper)
add_subdirectory(src/appl)
