#
# Copyright(c) 2019 Intel Corporation
# SPDX - License - Identifier: BSD - 2 - Clause - Patent
#

# ASM_SSSE3 Directory CMakeLists.txt

# Include Encoder Subdirectories
include_directories(${PROJECT_SOURCE_DIR}/Source/API/
    ${PROJECT_SOURCE_DIR}/Source/Lib/Common/Codec/
    ${PROJECT_SOURCE_DIR}/Source/Lib/Common/C_DEFAULT/
    ${PROJECT_SOURCE_DIR}/Source/Lib/Common/ASM_SSE2/
    ${PROJECT_SOURCE_DIR}/Source/Lib/Common/ASM_SSSE3/
    ${PROJECT_SOURCE_DIR}/Source/Lib/Common/ASM_SSE4_1/
    ${PROJECT_SOURCE_DIR}/Source/Lib/Common/ASM_AVX2/
    ${PROJECT_SOURCE_DIR}/Source/Lib/Common/ASM_AVX512/)

set(flags_to_test -mssse3)

if(CMAKE_C_COMPILER_ID STREQUAL "Intel" AND NOT WIN32)
    list(APPEND flags_to_test -static-intel -w)
endif()

test_apply_compiler_flags(${flags_to_test})

file(GLOB all_files
    "*.h"
    "*.asm"
    "*.c")

file(GLOB asm_includes "../ASM_SSE2/x86_abi_support.asm")

#list(REMOVE_ITEM all_files ${asm_includes})

add_library(COMMON_ASM_SSSE3 OBJECT ${all_files})
