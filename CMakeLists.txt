cmake_minimum_required(VERSION 3.12)
project(cpuburner VERSION 0.0.0)

find_package(daq-cmake REQUIRED)

daq_setup_environment()

find_package(appfwk REQUIRED)
#find_package(opmonlib REQUIRED)
find_package(Boost COMPONENTS unit_test_framework REQUIRED)
find_package(ers REQUIRED)
find_package(okssystem REQUIRED)
find_package(genconfig REQUIRED)
find_package(oksdbinterfaces REQUIRED)
find_package(coredal REQUIRED)

daq_generate_dal(cpuburner.schema.xml
  NAMESPACE dunedaq::cpuburner::dal DEP_PKGS coredal)

daq_codegen(cpuburner.jsonnet TEMPLATES Structs.hpp.j2 Nljs.hpp.j2)
daq_codegen(cpuburnerinfo.jsonnet DEP_PKGS opmonlib TEMPLATES opmonlib/InfoStructs.hpp.j2 opmonlib/InfoNljs.hpp.j2)

daq_add_plugin(CPUBurner duneDAQModule 
  LINK_LIBRARIES appfwk::appfwk cpuburner_oks)

daq_install()

