cmake_minimum_required(VERSION 3.5)

idf_component_register(
                       SRCS "src/WakeOnLan.cpp"
                       INCLUDE_DIRS "src"
                       PRIV_REQUIRES arduino-esp32
)

project(WakeOnLan)
