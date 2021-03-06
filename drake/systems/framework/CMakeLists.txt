# Source files used to build drakeSystemFramework.
set(sources
  abstract_state.cc
  basic_vector.cc
  cache.cc
  context.cc
  continuous_state.cc
  diagram.cc
  diagram_builder.cc
  diagram_context.cc
  diagram_continuous_state.cc
  discrete_state.cc
  input_port_evaluator_interface.cc
  leaf_context.cc
  leaf_system.cc
  output_port_listener_interface.cc
  parameters.cc
  state.cc
  subvector.cc
  supervector.cc
  system.cc
  system_input.cc
  system_output.cc
  system_port_descriptor.cc
  value.cc
  vector_base.cc)

# Headers that should be installed with Drake so that they
# are available elsewhere via #include.
#
# TODO(david-german-tri): Some of these headers are implementation details that
# should never be directly included outside of systems/framework. They ought to
# be private, but we can't make them private yet because they are included in
# API headers. (For example, subvector.h is used in state.h.) Once the
# System2 framework template implementations have been moved into .cc files
# using explicit instantiation, tighten this list.
set(installed_headers
  abstract_state.h
  basic_vector.h
  cache.h
  context.h
  continuous_state.h
  diagram.h
  diagram_builder.h
  diagram_context.h
  diagram_continuous_state.h
  discrete_state.h
  input_port_evaluator_interface.h
  leaf_context.h
  leaf_system.h
  output_port_listener_interface.h
  parameters.h
  state.h
  subvector.h
  supervector.h
  system.h
  systems.h
  system_input.h
  system_output.h
  system_port_descriptor.h
  value.h
  vector_base.h)

# Headers that are needed by code here but should not
# be exposed anywhere else.
set(private_headers)

add_library_with_exports(LIB_NAME drakeSystemFramework
  SOURCE_FILES ${sources} ${installed_headers} ${private_headers})
target_link_libraries(drakeSystemFramework
  drakeCommon
  drakeTrajectories
  Eigen3::Eigen)

drake_install_headers(${installed_headers})

drake_install_libraries(drakeSystemFramework)
drake_install_pkg_config_file(drake-system-framework
  TARGET drakeSystemFramework
  LIBS -ldrakeSystemFramework
  REQUIRES
    drake-common
    drake-trajectories
    eigen3)

if(BUILD_TESTING)
  add_subdirectory(test)
endif()
