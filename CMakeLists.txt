cmake_minimum_required(VERSION 3.5)
project(idrs_tokent VERSION 1.0.0)
find_package(eosio.cdt)

add_contract(idrs-token idrs-token ${CMAKE_CURRENT_SOURCE_DIR}/src/idrs-token.cpp)

target_include_directories(idrs-token.wasm
   PUBLIC
   ${CMAKE_CURRENT_SOURCE_DIR}/include)

set_target_properties(idrs-token.wasm
   PROPERTIES
   RUNTIME_OUTPUT_DIRECTORY "${CMAKE_CURRENT_BINARY_DIR}")

configure_file( ${CMAKE_CURRENT_SOURCE_DIR}/ricardian/idrs-token.contracts.md.in ${CMAKE_CURRENT_BINARY_DIR}/ricardian/idrs-token.contracts.md @ONLY )

target_compile_options( idrs-token.wasm PUBLIC -R${CMAKE_CURRENT_SOURCE_DIR}/ricardian -R${CMAKE_CURRENT_BINARY_DIR}/ricardian )