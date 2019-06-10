# CMakeList.txt: SSH2Example에 대한 CMake 프로젝트, 여기에 소스를 포함하고
# 프로젝트 특정 논리를 정의합니다.
#
cmake_minimum_required (VERSION 3.8)

include(CheckFunctionExists)
include(CheckSymbolExists)
include(CheckFunctionExistsMayNeedLibrary)
include(CheckIncludeFiles)
include(CheckTypeSize)
include(CheckSymbolExists)
include(CheckNonblockingSocketSupport)
include(SocketLibraries)

check_include_files(inttypes.h HAVE_INTTYPES_H)
check_include_files(unistd.h HAVE_UNISTD_H)
check_include_files(sys/param.h HAVE_SYS_PARAM_H)
check_include_files(sys/socket.h HAVE_SYS_SOCKET_H)
check_include_files(arpa/inet.h HAVE_ARPA_INET_H)
check_include_files(windows.h HAVE_WINDOWS_H)
check_include_files(winsock2.h HAVE_WINSOCK2_H)
check_include_files(netinet/in.h HAVE_NETINET_IN_H)

append_needed_socket_libraries(LIBRARIES)



# TODO: 필요한 경우 테스트를 추가하고 대상을 설치합니다.

## Platform checks
check_include_files(inttypes.h HAVE_INTTYPES_H)
check_include_files(unistd.h HAVE_UNISTD_H)
check_include_files(stdlib.h HAVE_STDLIB_H)
check_include_files(sys/select.h HAVE_SYS_SELECT_H)
check_include_files(sys/socket.h HAVE_SYS_SOCKET_H)
check_include_files(sys/time.h HAVE_SYS_TIME_H)
check_include_files(arpa/inet.h HAVE_ARPA_INET_H)
check_include_files(netinet/in.h HAVE_NETINET_IN_H)
check_include_files(winsock2.h HAVE_WINSOCK2_H)

check_symbol_exists(strcasecmp strings.h HAVE_STRCASECMP)
check_symbol_exists(_stricmp string.h HAVE__STRICMP)
check_symbol_exists(snprintf stdio.h HAVE_SNPRINTF)
check_symbol_exists(_snprintf stdio.h HAVE__SNPRINTF)

check_symbol_exists(__func__ "" HAVE___FUNC__)
check_symbol_exists(__FUNCTION__ "" HAVE___FUNCTION__)

configure_file(
  ${CMAKE_CURRENT_SOURCE_DIR}/config_example_cmake.h.in
  ${CMAKE_CURRENT_SOURCE_DIR}/config_example.h)


find_package(Libssh2 CONFIG REQUIRED)

# 이 프로젝트의 실행 파일에 소스를 추가합니다.
add_executable (SSH2Example "SSH2Example.cpp" "SSH2Example.h" "config_example.h" )
target_link_libraries(SSH2Example   Libssh2::libssh2 ${LIBRARIES} )