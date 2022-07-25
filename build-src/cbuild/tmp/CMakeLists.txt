# CMSIS Build CMakeLists generated on 2022-07-25T15:41:03

cmake_minimum_required(VERSION 3.18)

# Target options

set(TARGET test.release+HW_A)
set(CPU Cortex-M3)
set(PRJ_DIR "/workspaces/cbuild-tests/prj/generated-projects/test.release+HW_A")
set(OUT_DIR "/workspaces/cbuild-tests/build-src/cbuild/test.release+HW_A")
set(INT_DIR "/workspaces/cbuild-tests/build-src/cbuild/tmp")
set(FPU NO_FPU)
set(SECURE Non-secure)
set(BYTE_ORDER Little-endian)
set(AS_FLAGS_GLOBAL "-masm=auto -D__MICROLIB")
set(CC_FLAGS_GLOBAL "-O1 -std=c99 -Wno-packed -Wno-missing-variable-declarations -Wno-missing-prototypes -Wno-missing-noreturn -Wno-sign-conversion -Wno-nonportable-include-path -Wno-reserved-id-macro -Wno-unused-macros -Wno-documentation-unknown-command -Wno-documentation -Wno-license-management -Wno-parentheses-equality -ffunction-sections -fno-rtti -funsigned-char -ffp-mode=std -fno-short-enums -fno-short-wchar -D__MICROLIB -xc -c --target=arm-arm-none-eabi")
set(LD_FLAGS_GLOBAL "--info=summarystack,stack,unused,sizes,any,common,debug,inputs,summarysizes,totals,veneers --summary_stderr --callgraph --strict --list test.map --library_type=microlib --any_sort_order=descending_size --any_placement=worst_fit --sort=Lexical --map --load_addr_map_info --xref --symbols --any_contingency --entry Reset_Handler --first __Vectors")

set(DEFINES
  STM32F10X_MD
  _RTE_
  USE_CAN
  ARM_MATH_CM3
  USE_STDPERIPH_DRIVER
)

set(INC_PATHS
  "/workspaces/cbuild-tests/prj/generated-projects/test.release+HW_A/RTE/Device/STM32F103TB"
  "/workspaces/cbuild-tests/prj/generated-projects/test.release+HW_A/RTE/_test.release_HW_A"
  "/home/dev/Keil/PACKS/ARM/CMSIS/5.9.0/CMSIS/Core/Include"
  "/home/dev/Keil/PACKS/Keil/STM32F1xx_DFP/2.4.0/Device/Include"
  "/workspaces/cbuild-tests/inc"
)

set(AS_ARM_SRC_FILES
  "/workspaces/cbuild-tests/prj/generated-projects/test.release+HW_A/RTE/Device/STM32F103TB/startup_stm32f10x_md.s"
)

set(CC_SRC_FILES
  "/workspaces/cbuild-tests/prj/generated-projects/test.release+HW_A/RTE/Device/STM32F103TB/system_stm32f10x.c"
  "/workspaces/cbuild-tests/src/main.c"
)

# Toolchain config map

include ("/home/dev/cmsis-toolbox-linux64/etc/AC6.6.18.0.cmake")

# Setup project

project(${TARGET} LANGUAGES AS_ARM C)

# Global Flags

set(CMAKE_AS_ARM_FLAGS "${AS_ARM_CPU} ${AS_ARM_BYTE_ORDER} ${AS_ARM_DEFINES} ${AS_ARM_FLAGS} ${AS_FLAGS_GLOBAL}")
set(CMAKE_C_FLAGS "${CC_CPU} ${CC_BYTE_ORDER} ${CC_DEFINES} ${CC_SECURE} ${CC_FLAGS} ${CC_FLAGS_GLOBAL} ${CC_SYS_INC_PATHS}")
set(CMAKE_C_LINK_FLAGS "${LD_CPU} ${LD_SCRIPT} ${LD_SECURE} ${LD_FLAGS_GLOBAL} ${LD_FLAGS}")

# Local Flags

foreach(SRC ${AS_ARM_SRC_FILES})
  set_source_files_properties(${SRC} PROPERTIES LANGUAGE AS_ARM)
endforeach()

# Compilation Database

set(CMAKE_EXPORT_COMPILE_COMMANDS ON)
add_custom_target(database COMMAND ${CMAKE_COMMAND} -E copy_if_different "${INT_DIR}/compile_commands.json" "${OUT_DIR}")

# Setup Target

add_executable(${TARGET} ${AS_ARM_SRC_FILES} ${CC_SRC_FILES})
set(CMAKE_EXECUTABLE_SUFFIX ${EXE_SUFFIX})
set_target_properties(${TARGET} PROPERTIES RUNTIME_OUTPUT_DIRECTORY ${OUT_DIR})
target_include_directories(${TARGET} PUBLIC ${INC_PATHS})

# Bin and Hex Conversion

add_custom_command(TARGET ${TARGET} POST_BUILD COMMAND ${CMAKE_OBJCOPY} ${ELF2HEX})
add_custom_command(TARGET ${TARGET} POST_BUILD COMMAND ${CMAKE_OBJCOPY} ${ELF2BIN})
