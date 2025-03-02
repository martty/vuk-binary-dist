cmake_minimum_required(VERSION 3.25)
project(vuk-binary-dist)

set(CMAKE_MODULE_PATH "${PROJECT_SOURCE_DIR}/cmake" ${CMAKE_MODULE_PATH})
find_package(ShaderCompile REQUIRED) # for embedding binary data

find_package(Vulkan REQUIRED COMPONENTS glslangValidator dxc)

add_custom_target(vukbdist ALL)

set(DXC_FLAGS -spirv -fspv-target-env=vulkan1.2 -fvk-use-gl-layout -Zpc -O3 -Fo)
target_shaders(vukbdist COMPILER Vulkan::dxc_exe ARGS -T cs_6_7 ${DXC_FLAGS} SHADERS src/SPD/spd.cs.hlsl)