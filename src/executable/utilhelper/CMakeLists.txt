include_directories(
  ${CMAKE_CURRENT_SOURCE_DIR}/RES
  ${UTIL_BOOTLOADER_INCLUDE_DIRS}
)

configure_file(RES/repair.rc ${RC_DIR}/repair.rc @ONLY)
file(GLOB Sources
  code/*.cpp
  ${RC_DIR}/repair.rc
)

add_definitions(
  -Dgamecore_LOG
  -DDONTUSE_PCH
  -DDESURA_EXE
  -DDESURA_CLIENT
)
				
add_executable(utilhelper WIN32 ${Sources})
target_link_libraries(utilhelper
  mdump_s
  util_s
  util_bootloader_s
  Comctl32
)

install_executable(utilhelper)
SetStaticRuntime(utilhelper)
