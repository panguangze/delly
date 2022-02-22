cmake_minimum_required(VERSION 3.16)
project(delly)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_BUILD_TYPE RELEASE)

set(CMAKE_EXPORT_COMPILECOMMANDS ON)
set(CMAKE_CXX_FLAGS_DEBUG "$ENV{CXX_FLAGS} -O0 -Wall -ggdb -fkeep-inline-functions")
set(CMAKE_CXX_FLAGS_RELEASE "$ENV{CXXFLAGS} -O3 ")
set(Boost_USE_STATIC_LIBS OFF)
set(Boost_USE_MULTITHREADED ON)
set(Boost_USE_STATIC_RUNTIME OFF)
aux_source_directory(./src DELLY_SRC)
include_directories(/mnt/d/linux/conda/envs/delly/include)
link_directories(/mnt/d/linux/conda/envs/delly/lib)
#aux_source_directory(./vcflib VCF_LIB)
#add_library(bio SHARED IMPORTED)
#add_library(bfi SHARED IMPORTED)
#add_library(bda SHARED IMPORTED)
#add_library(bsy SHARED IMPORTED)
#add_library(bpr SHARED IMPORTED)
#
#set_target_properties(bio PROPERTIES
#        IMPORTED_LOCATION "/mnt/d/linux/conda/envs/delly/lib/libboost_iostreams.so"
#        INTERFACE_INCLUDE_DIRECTORIES  "/mnt/d/linux/conda/envs/delly/include/boost")
#set_target_properties(bfi PROPERTIES
#        IMPORTED_LOCATION "/mnt/d/linux/conda/envs/delly/lib/libboost_filesystem.so"
#        INTERFACE_INCLUDE_DIRECTORIES  "/mnt/d/linux/conda/envs/delly/include/boost")
#set_target_properties(bpr PROPERTIES
#        IMPORTED_LOCATION "/mnt/d/linux/conda/envs/delly/lib/libboost_program_options.so"
#        INTERFACE_INCLUDE_DIRECTORIES  "/mnt/d/linux/conda/envs/delly/include/boost")
#set_target_properties(bda PROPERTIES
#        IMPORTED_LOCATION "/mnt/d/linux/conda/envs/delly/lib/libboost_date_time .so"
#        INTERFACE_INCLUDE_DIRECTORIES  "/mnt/d/linux/conda/envs/delly/include/boost")
#set_target_properties(bsy PROPERTIES
#        IMPORTED_LOCATION "/mnt/d/linux/conda/envs/delly/lib/libboost_system.so"
#        INTERFACE_INCLUDE_DIRECTORIES  "/mnt/d/linux/conda/envs/delly/include/boost")
add_executable(delly delly.cpp ${DELLY_SRC})

target_link_libraries(delly boost_iostreams boost_filesystem boost_program_options boost_date_time boost_system hts)
install(TARGETS delly DESTINATION bin)