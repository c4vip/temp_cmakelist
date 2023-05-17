cmake_minimum_required(VERSION 3.25)
project(temp)

set(CMAKE_CXX_STANDARD 11)

find_package(Boost REQUIRED COMPONENTS system)
find_package(spdlog REQUIRED)

# curl
find_package(CURL REQUIRED)
# set(CURL_INC_DIR /opt/homebrew/Cellar/curl/8.0.1/include)
# set(CURL_LINK_DIR /opt/homebrew/Cellar/curl/8.0.1/lib)
# include_directories(${CURL_INC_DIR})
# link_directories(${CURL_LINK_DIR})
# link_libraries(curl)

# openssl
find_package(OpenSSL REQUIRED)
# set(OPENSSL_INC_DIR /opt/homebrew/Cellar/openssl@1.1/1.1.1t/include)
# set(OPENSSL_LINK_DIR /opt/homebrew/Cellar/openssl@1.1/1.1.1t/lib)
# include_directories(${OPENSSL_INC_DIR})
# link_directories(${OPENSSL_LINK_DIR})
# link_libraries(ssl crypto)

find_package(jsoncpp REQUIRED)

# set(JSONCPP_INC_DIR /opt/homebrew/Cellar/jsoncpp/1.9.5/include)
# set(JSONCPP_LINK_DIR /opt/homebrew/Cellar/jsoncpp/1.9.5/lib)
# include_directories(${JSONCPP_INC_DIR})
# link_directories(${JSONCPP_LINK_DIR})
# link_libraries(jsoncpp)

if (Boost_FOUND)
    message("找到了boost库")
    include_directories(${Boost_INCLUDE_DIRS})
endif ()
if (spdlog_FOUND)
    message("找到了spdlog库")
    include_directories(${spdlog_INCLUDE_DRIS})
endif ()

if(CURL_FOUND)
    message("found curl lib")
   include_directories(${CURL_INCLUDE_DIR})
   message(STATUS "Curl Found: ${CURL_VERSION_STRING} ${CURL_LIBRARIES} ${CURL_LINK_LIBRARIES}!")
else(CURL_FOUND)
   message(FATAL_ERROR "Could not find the CURL library and development files.")
endif()

if(OPENSSL_FOUND)
    include_directories(${OPENSSL_INCLUDE_DIR})
    message(STATUS "OpenSSL Found!")
endif()
if(jsoncpp_FOUND)
    message("find jsonccp")
    include_directories(${JSONCPP_INCLUDE_DIR})
endif()


add_executable(temp main.cpp)

target_link_libraries(temp PRIVATE ${Boost_LIBRARIES} ${jsoncpp_LIBRARIES} ${CURL_LIBRARIES} ${spdlog_LIBRARIES} ${OpenSSL_LIBRARIES})
#target_link_libraries(sdp PRIVATE ${Boost_LIBRARIES} ${CONAN_LIBS} ${CURL_LIBRARIES} ${FMT_LIBRARIES})
#target_link_libraries(sdp PRIVATE OpenSSL::Crypto OpenSSL::SSL)

# echo 'export PATH="/opt/homebrew/opt/openssl@1.1/bin:$PATH"' >> ~/.zshrc