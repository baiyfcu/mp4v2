project(mp4v2)
set(CMAKE_VERBOSE_MAKEFILE on)

set(mp4v2_DIR ${CMAKE_CURRENT_SOURCE_DIR})
file(GLOB mp4v2src ${mp4v2_DIR}/src/*.cpp)
file(GLOB mp4v2src_bmff ${mp4v2_DIR}/src/bmff/*.cpp)
file(GLOB mp4v2src_itmf ${mp4v2_DIR}/src/itmf/*.cpp)
file(GLOB mp4v2src_qtff ${mp4v2_DIR}/src/qtff/*.cpp)
file(GLOB mp4v2util ${mp4v2_DIR}/util/*.cpp)
file(GLOB mp4v2libutil "${mp4v2_DIR}/libutil/*.cpp")
file(GLOB mp4v2libplatform "${mp4v2_DIR}/libplatform/*.cpp")
file(GLOB mp4v2libplatform_time "${mp4v2_DIR}/libplatform/time/*.cpp")
file(GLOB mp4v2libplatform_number "${mp4v2_DIR}/libplatform/number/*.cpp")
file(GLOB mp4v2libplatform_io "${mp4v2_DIR}/libplatform/io/*.cpp")
file(GLOB mp4v2libplatform_process "${mp4v2_DIR}/libplatform/process/*.cpp")
file(GLOB mp4v2libplatform_prog "${mp4v2_DIR}/libplatform/prog/*.cpp")
file(GLOB mp4v2libplatform_sys "${mp4v2_DIR}/libplatform/sys/*.cpp")



include_directories(${mp4v2_DIR}
                    ${mp4v2_DIR}/include)
					
#-------------------------------------------------------------------------------------------------------------------		
if(USE_ALLMT_)
set(CMAKE_CXX_FLAGS_DEBUG "/D_DEBUG /MTd /Zi /Ob0 /Od /RTC1")
set(CMAKE_CXX_FLAGS_RELEASE "/MT /O2 /Ob2 /D NDEBUG")
set(CMAKE_CXX_FLAGS_MINSIZEREL "/MT /O1 /Ob1 /D NDEBUG")
set(CMAKE_CXX_FLAGS_RELWITHDEBINFO "/MT /Zi /O2 /Ob1 /D NDEBUG")
endif()

# 给解决方案中工程增加宏定义
ADD_DEFINITIONS(-DMP4V2_USE_STATIC_LIB)

add_library( # Sets the name of the library.
             mp4v2
             # Sets the library as a shared library.
             STATIC
             # Provides a relative path to your source file(s).
             # Associated headers in the same location as their source
             # file are automatically included.
             ${mp4v2src};
             ${mp4v2src_bmff};
             ${mp4v2src_itmf};
             ${mp4v2src_qtff};
             ${mp4v2util};
             ${mp4v2libplatform};
             ${mp4v2libplatform_time};
             ${mp4v2libplatform_number};
             ${mp4v2libplatform_io};
             ${mp4v2libplatform_prog};
             ${mp4v2libplatform_sys};
             ${mp4v2libutil};
             )
			 
set_target_properties(mp4v2 PROPERTIES OUTPUT_NAME "mp4v2")