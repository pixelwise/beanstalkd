project(my_vulkan)
cmake_minimum_required(VERSION 3.10)
execute_process(
    COMMAND ${CMAKE_CURRENT_SOURCE_DIR}/verc.sh
    OUTPUT_FILE ${CMAKE_CURRENT_BINARY_DIR}/vers.c
    WORKING_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}
)
set(
    SOURCES
    ${CMAKE_CURRENT_BINARY_DIR}/vers.c
    conn.c
    file.c
    heap.c
    job.c
    ms.c
    net.c
    primes.c
    prot.c
    serv.c
    time.c
    tube.c
    util.c
    walg.c
    main.c
)
set(
    LIBRARIES
)
IF(APPLE)
    set(SOURCES ${SOURCES} darwin.c)
ELSE(APPLE)
    set(SOURCES ${SOURCES} linux.c)
    set(LIBRARIES ${LIBRARIES} rt)
ENDIF(APPLE)
add_executable(
    beanstalkd
    ${SOURCES}
)
target_link_libraries(
    beanstalkd
    ${LIBRARIES}
)
