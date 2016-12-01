if(lcm_FOUND)
  # Defines a shared library for use by KUKA iiwa world demos based on
  # System 2.0.
  add_library_with_exports(LIB_NAME drakeKukaIiwaWorld SOURCE_FILES
      iiwa_world_sim_builder.cc)
  target_link_libraries(drakeKukaIiwaWorld
      drakeKukaIiwaArmCommon
      drakeLCMSystem2
      drakeRigidBodyPlant
      drakeSystemAnalysis
      gflags)
  drake_install_libraries(drakeKukaIiwaWorld)
  drake_install_headers(
      iiwa_world_sim_builder.h)
  drake_install_pkg_config_file(drake-kuka-iiwa-world
      TARGET drakeKukaIiwaWorld
      LIBS -ldrakeKukaIiwaWorld
      REQUIRES drake-kuka-iiwa-arm-common
      VERSION 0.0.1)

  add_executable(iiwa_world_demo iiwa_world_demo.cc)
  target_link_libraries(iiwa_world_demo
      drakeKukaIiwaWorld)
  drake_add_test(
      NAME iiwa_world_demo COMMAND iiwa_world_demo -simulation_sec 1.0)
endif()