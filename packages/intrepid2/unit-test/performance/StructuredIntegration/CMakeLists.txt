SET(SOURCES "")

FILE(GLOB SOURCES *.cpp)

INCLUDE_DIRECTORIES("../../../assembly-examples")

SET(LIBRARIES intrepid2)

TRIBITS_ADD_EXECUTABLE_AND_TEST(
  StructuredIntegrationPerformance
  SOURCES ${SOURCES}
  ARGS
  NUM_MPI_PROCS 1
  ADD_DIR_TO_NAME
  )
