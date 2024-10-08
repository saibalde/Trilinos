TRIBITS_INCLUDE_DIRECTORIES(${${PACKAGE_NAME}_SOURCE_DIR}/adapters/mpi/src/function)
TRIBITS_INCLUDE_DIRECTORIES(${${PACKAGE_NAME}_SOURCE_DIR}/adapters/mpi/src/vector)

TRIBITS_ADD_EXECUTABLE_AND_TEST(
  example_01
  SOURCES example_01.cpp
  ARGS PrintItAll
  NUM_MPI_PROCS 1
  PASS_REGULAR_EXPRESSION "TEST PASSED"
  ADD_DIR_TO_NAME
)

TRIBITS_COPY_FILES_TO_BINARY_DIR(
  PinTParabolicControlDataCopy
  SOURCE_FILES
    input_ex01.xml
    input_rol.xml
  SOURCE_DIR "${CMAKE_CURRENT_SOURCE_DIR}"
  DEST_DIR "${CMAKE_CURRENT_BINARY_DIR}"
)

IF( TPL_ENABLE_MPI )

  TRIBITS_ADD_EXECUTABLE_AND_TEST(
      PinTConstraint_FD_Test
      SOURCES PinTConstraint_FD_Test.cpp
      ARGS PrintItAll
      NUM_MPI_PROCS 2
      PASS_REGULAR_EXPRESSION "TEST PASSED"
      ADD_DIR_TO_NAME
      )

  TRIBITS_ADD_EXECUTABLE_AND_TEST(
      AugmentedSystem_test
      SOURCES AugmentedSystem.cpp
      ARGS PrintItAll
      COMM mpi
      NUM_MPI_PROCS 2
      PASS_REGULAR_EXPRESSION "TEST PASSED"
      ADD_DIR_TO_NAME
      )

ENDIF()
