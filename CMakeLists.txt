cmake_minimum_required(VERSION 3.16)
project(ffplay C)

set(CMAKE_C_STANDARD 99)

include_directories(.)
# FFmpeg的安装目录，可以通过命令"brew info ffmpeg"获取
set(FFMPEG_DIR /usr/local/Cellar/ffmpeg/4.3.1)
# 头文件搜索路径
include_directories(${FFMPEG_DIR}/include/)

set(SDL_H /usr/local/Cellar/sdl2/2.0.14_1/include) # 这个SDL开发包的路径，可以通过brew info sdl2查出来
include_directories(${SDL_H}) # 添加SDL头文件搜索路径

set(SDL_LIB /usr/local/Cellar/sdl2/2.0.14_1/lib/libSDL2-2.0.0.dylib)
link_libraries(${SDL_LIB}) # 增加SDL链接库目录
# 动态链接库或静态链接库的搜索路径
link_directories(${FFMPEG_DIR}/lib/)

add_executable(ffplay
        cmdutils.c
        cmdutils.h
        config.h
        ffplay.c
        )
target_link_libraries(ffplay
        swscale swresample avcodec avutil avdevice avfilter avformat
        )
