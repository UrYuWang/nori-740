cmake_minimum_required (VERSION 2.8.3)
project(nori)

add_subdirectory(ext ext_build)

include_directories(
  # Nori include files
  ${CMAKE_CURRENT_SOURCE_DIR}/include
  # tinyformat string formatting library
  ${TFM_INCLUDE_DIR}
  # Eigen linear algebra library
  ${EIGEN_INCLUDE_DIR}
  # OpenEXR high dynamic range bitmap library
  ${OPENEXR_INCLUDE_DIRS}
  # Intel Thread Building Blocks
  ${TBB_INCLUDE_DIR}
  # Pseudorandom number generator
  ${PCG32_INCLUDE_DIR}
  # PugiXML parser
  ${PUGIXML_INCLUDE_DIR}
  # Helper functions for statistical hypothesis tests
  ${HYPOTHESIS_INCLUDE_DIR}
  # GLFW library for OpenGL context creation
  ${GLFW_INCLUDE_DIR}
  # GLEW library for accessing OpenGL functions
  ${GLEW_INCLUDE_DIR}
  # NanoVG drawing library
  ${NANOVG_INCLUDE_DIR}
  # NanoGUI user interface library
  ${NANOGUI_INCLUDE_DIR}
  ${NANOGUI_EXTRA_INCS}
  # Portable filesystem API
  ${FILESYSTEM_INCLUDE_DIR}
)

# The following lines build the main executable. If you add a source
# code file to Nori, be sure to include it in this list.
add_executable(nori

  # Header files
  include/nori/bbox.h
  include/nori/bitmap.h
  include/nori/block.h
  include/nori/bsdf.h
  include/nori/accel.h
  include/nori/camera.h
  include/nori/color.h
  include/nori/common.h
  include/nori/dpdf.h
  include/nori/frame.h
  include/nori/integrator.h
  include/nori/emitter.h
  include/nori/mesh.h
  include/nori/object.h
  include/nori/parser.h
  include/nori/proplist.h
  include/nori/ray.h
  include/nori/rfilter.h
  include/nori/sampler.h
  include/nori/scene.h
  include/nori/timer.h
  include/nori/transform.h
  include/nori/vector.h
  include/nori/warp.h
  include/nori/lightprobe.h
  include/nori/guider.h

  # Source code files
  src/bitmap.cpp
  src/block.cpp
  src/accel.cpp
  src/chi2test.cpp
  src/common.cpp
  src/diffuse.cpp
  src/gui.cpp
  src/independent.cpp
  src/main.cpp
  src/mesh.cpp
  src/obj.cpp
  src/object.cpp
  src/parser.cpp
  src/perspective.cpp
  src/proplist.cpp
  src/rfilter.cpp
  src/scene.cpp
  src/ttest.cpp
  src/warp.cpp
  src/microfacet.cpp
  src/mirror.cpp
  src/dielectric.cpp
  src/normals.cpp
  src/simple.cpp
  src/ao.cpp
  src/lightprobe.cpp
  src/area.cpp
  src/whitted.cpp
  src/path_simple.cpp
  src/path.cpp
  src/roughdielectric.cpp
  src/qtable.cpp
  src/path_guided.cpp
  src/path_naive.cpp
  src/path_guided_simple.cpp
  src/path_guided_mis.cpp
  src/qtable_sphere.cpp
  src/probe.cpp
)

add_definitions(${NANOGUI_EXTRA_DEFS})

# The following lines build the warping test application
add_executable(warptest
  include/nori/color.h
  include/nori/warp.h
  include/nori/vector.h
  include/nori/bitmap.h
  include/nori/lightprobe.h
  src/bitmap.cpp
  src/warp.cpp
  src/warptest.cpp
  src/microfacet.cpp
  src/object.cpp
  src/proplist.cpp
  src/common.cpp
  src/lightprobe.cpp
)

target_link_libraries(nori tbb_static pugixml IlmImf nanogui ${NANOGUI_EXTRA_LIBS})
target_link_libraries(warptest tbb_static IlmImf nanogui ${NANOGUI_EXTRA_LIBS})

# vim: set et ts=2 sw=2 ft=cmake nospell:
