file(GLOB SOURCE *.c *.cpp)
add_library(krnl386 SHARED ${SOURCE} krnl386.exe16.obj ${CMAKE_CURRENT_BINARY_DIR}/krnl386.def)
include_directories(../wine)
add_definitions(-DMZ_SUPPORTED -DENABLEREDIRECTSYSTEMDIR -D_X86_ -D__WINESRC__ -D__i386__  -DHAVE_STRNCASECMP -DHAVE__STRNICMP -D_WINTERNL_ -DNtCurrentTeb=NtCurrentTeb__  -DDECLSPEC_HIDDEN= -Dstrncasecmp=_strnicmp)
spec_build(krnl386.exe16 KERNEL ARG --heap 65520)
target_link_libraries(krnl386 libwine winecrt0 lz32.lib ntdll.lib ddraw.lib dsound.lib)
set_target_properties(krnl386 PROPERTIES SUFFIX ".exe16")
