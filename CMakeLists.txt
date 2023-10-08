cmake_minimum_required(VERSION 3.0)
project(SSLTest)

# Find OpenSSL
find_package(OpenSSL REQUIRED)
add_executable(server server.cpp)
add_executable(client client.cpp)
add_executable(client_bak client.cpp)

# Link OpenSSL to your project
target_link_libraries(server OpenSSL::SSL OpenSSL::Crypto)
target_link_libraries(client OpenSSL::SSL OpenSSL::Crypto)
target_link_libraries(client_bak OpenSSL::SSL OpenSSL::Crypto)
