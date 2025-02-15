

#
# A) Package-specific configuration options
#

ASSERT_DEFINED(${PACKAGE_NAME}_ENABLE_MPI)
SET(HAVE_MPI ${${PACKAGE_NAME}_ENABLE_MPI})

ASSERT_DEFINED(${PACKAGE_NAME}_ENABLE_PETSC)
SET(HAVE_ML_PETSC ${${PACKAGE_NAME}_ENABLE_PETSC})

# BLAS and LAPACK are required in the CMake build
SET(HAVE_BLAS ON)
SET(HAVE_LAPACK ON)

TRIBITS_CONFIGURE_FILE(ml_config.h)

#
# B) Define the header and source files (and directories)
#

#
# src
#

SET(HEADERS "")
SET(SOURCES "")

INCLUDE_DIRECTORIES(${CMAKE_CURRENT_BINARY_DIR})

SET(HEADERS ${HEADERS}
  ${CMAKE_CURRENT_BINARY_DIR}/ml_config.h
  )

#
# Core files
#

INCLUDE_DIRECTORIES(${CMAKE_CURRENT_SOURCE_DIR}/Include)
INCLUDE_DIRECTORIES(${CMAKE_CURRENT_SOURCE_DIR}/Comm)
INCLUDE_DIRECTORIES(${CMAKE_CURRENT_SOURCE_DIR}/Coarsen)
INCLUDE_DIRECTORIES(${CMAKE_CURRENT_SOURCE_DIR}/FEGrid)
INCLUDE_DIRECTORIES(${CMAKE_CURRENT_SOURCE_DIR}/Main)
INCLUDE_DIRECTORIES(${CMAKE_CURRENT_SOURCE_DIR}/Smoother)
INCLUDE_DIRECTORIES(${CMAKE_CURRENT_SOURCE_DIR}/Krylov)
INCLUDE_DIRECTORIES(${CMAKE_CURRENT_SOURCE_DIR}/Operator)

APPEND_SET(HEADERS
  Include/ml_defs.h
  Comm/ml_comm.h
  Include/ml_include.h
  Include/ml_common.h
  Coarsen/ml_amg_genP.h
  Coarsen/ml_amg.h
  Coarsen/ml_agg_genP.h
  Coarsen/ml_agg_min_energy.h
  Coarsen/ml_check.h
  Coarsen/ml_aggregate.h
  Coarsen/ml_ggraph.h
  Coarsen/ml_parmetis_constants.h
  FEGrid/ml_mapper.h
  FEGrid/ml_gridagx.h
  FEGrid/ml_pde.h
  FEGrid/ml_bdrypts.h
  Coarsen/ml_agg_reitzinger.h
  Coarsen/ml_agg_METIS.h
  Coarsen/ml_agg_user.h
  Coarsen/ml_agg_VBMETIS.h
  Coarsen/ml_agg_Zoltan.h
  Coarsen/ml_agg_ParMETIS.h
  Coarsen/ml_qr_fix.h
  Coarsen/ml_qr_fix.hpp
  FEGrid/ml_gridfunc.h
  FEGrid/ml_setup.h
  FEGrid/ml_elementagx.h
  FEGrid/ml_grid.h 
  Main/ml_struct.h
  Main/ml_seg_precond.h
  Main/ml_1level.h
  Main/mli_solver.h
  Main/ml_ggb.h
  Main/ml_viz_stats.h
  Comm/ml_comminfoagx.h
  Comm/ml_comminfoop.h
  Smoother/ml_csolve.h
  Smoother/ml_mls.h
  Smoother/ml_smoother.h
  Smoother/ml_solver.h
  Smoother/ml_superlu.h
  Smoother/ml_xxt.h
  Smoother/ml_xyt.h
  Krylov/ml_bicgstabl.h
  Krylov/ml_cg.h
  Krylov/ml_gmres.h
  Krylov/ml_krylov.h
  Operator/ml_mat_formats.h
  Operator/ml_operatoragx.h
  Operator/ml_operator_blockmat.h
  Operator/ml_operator.h
  Operator/ml_op_utils.h
  Operator/ml_rap.h
  )

APPEND_SET(SOURCES
  Coarsen/ml_agg_uncoupled.c
  Coarsen/ml_amg.c
  Coarsen/ml_agg_coupled.c
  Coarsen/ml_amg_genP.c
  Coarsen/ml_check.c
  Coarsen/ml_agg_dd.c
  Coarsen/ml_agg_genP.c
  Coarsen/ml_agg_min_energy.cpp
  Coarsen/ml_amg_MIS.c
  Coarsen/ml_agg_MIS.c
  Coarsen/ml_agg_METIS.c
  Coarsen/ml_agg_user.c
  Coarsen/ml_agg_VBMETIS.c
  Coarsen/ml_agg_Zoltan.c
  Coarsen/ml_agg_ParMETIS.c
  Coarsen/ml_aggregate.c
  Coarsen/ml_ggraph.c
  Coarsen/ml_agg_reitzinger.c
  Coarsen/ml_qr_fix.cpp
  FEGrid/ml_gridagx.c
  FEGrid/ml_pde.c
  FEGrid/ml_bdrypts.c
  FEGrid/ml_grid.c
  FEGrid/ml_gridfunc.c
  FEGrid/ml_setup.c
  FEGrid/ml_elementagx.c
  FEGrid/ml_get_basis.c
  FEGrid/ml_mapper.c
  Main/ml_struct.c
  Main/driver.c
  Main/mli_solver.c
  Main/ml_seg_precond.c
  Main/ml_ggb.c
  Comm/ml_comm.c
  Comm/ml_comminfoagx.c
  Comm/ml_comminfoop.c
  Comm/ml_exch_row.c
  Smoother/ml_csolve.c
  Smoother/ml_smoother.c
  Smoother/ml_solver.c
  Smoother/ml_superlu.c
  Smoother/ml_xxt.c
  Smoother/ml_xyt.c
  Krylov/ml_bicgstabl.c
  Krylov/ml_cg.c
  Krylov/ml_gmres.c
  Krylov/ml_krylov.c
  Operator/ml_matmat_mult.c
  Operator/ml_operatoragx.c
  Operator/ml_operator_blockmat.c
  Operator/ml_operator.c
  Operator/ml_op_utils.c
  Operator/ml_rap.c
  Operator/ml_mat_formats.c
  Operator/ml_rap_utils.c
  )

#
# util files
#

INCLUDE_DIRECTORIES(${CMAKE_CURRENT_SOURCE_DIR}/Utils)
INCLUDE_DIRECTORIES(${CMAKE_CURRENT_SOURCE_DIR}/RefMaxwell)
INCLUDE_DIRECTORIES(${CMAKE_CURRENT_SOURCE_DIR}/MatrixFree)
INCLUDE_DIRECTORIES(${CMAKE_CURRENT_SOURCE_DIR}/MLAPI)
INCLUDE_DIRECTORIES(${CMAKE_CURRENT_SOURCE_DIR}/LevelWrap)

APPEND_SET(HEADERS
  Utils/ml_aztec_utils.h
  Utils/ml_epetra_utils.h
  Utils/ml_utils.h
  Utils/ml_memory.h
  Utils/ml_agg_info.h
  Utils/ml_aztec_lapack.h
  Utils/ml_rbm.h
  Utils/ml_read_utils.h
  Utils/ml_superlu_lapack.h
  Utils/ml_epetra_operator.h
  Utils/ml_twogrid_analysis.h
  Utils/ml_intlist.h
  Utils/ml_vec.h
  Utils/ml_lapack.h
  Utils/ml_utils.h
  Utils/ml_eigf2c.h
  Utils/ml_vampir.h
  Utils/ml_viz_opendx.h
  Utils/ml_viz_xyz.h
  Utils/ml_viz_vtk.h
  Utils/ml_amesos.h
  Utils/ml_amesos_wrap.h
  Utils/ml_ifpack.h
  Utils/ml_ifpack_wrap.h
  Utils/ml_ifpack_epetra_wrap.h
  Utils/ml_self.h
  Utils/ml_self_wrap.h
  Utils/ml_epetra_preconditioner.h
  Utils/ml_anasazi.h
  Utils/ml_epetra.h
  Utils/ml_MultiLevelOperator.h
  Utils/ml_MultiLevelPreconditioner.h
  Utils/ml_RowMatrix.h
  Utils/ml_FilterType.h
  Utils/ml_DD_prec.h
  Utils/ml_Ifpack_ML.h
  Utils/ml_Epetra_wrap_CrsGraph_as_RowMatrix.H
  Utils/ml_Preconditioner.h
  Utils/Epetra_Operator_With_MatMat.h
  Utils/Epetra_Multi_CrsMatrix.h
  Utils/ml_ValidateParameters.h
  Utils/ml_petsc.h
  RefMaxwell/ml_RefMaxwell_Utils.h
  RefMaxwell/ml_EdgeMatrixFreePreconditioner.h
  RefMaxwell/ml_FaceMatrixFreePreconditioner.h
  RefMaxwell/ml_RefMaxwell_11_Operator.h
  RefMaxwell/ml_RefMaxwell.h
  RefMaxwell/ml_GradDiv.h
  MatrixFree/ml_MatrixFreePreconditioner.h
  MatrixFree/ml_ElementByElement_SingleElement.h
  MLAPI/MLAPI.h
  MLAPI/MLAPI_Aggregation.h
  MLAPI/MLAPI_BaseObject.h
  MLAPI/MLAPI_BaseOperator.h
  MLAPI/MLAPI_CompObject.h
  MLAPI/MLAPI_Defaults.h
  MLAPI/MLAPI_Eig.h
  MLAPI/MLAPI_EpetraBaseOperator.h
  MLAPI/MLAPI_Expressions.h
  MLAPI/MLAPI_Gallery.h
  MLAPI/MLAPI_InverseOperator.h
  MLAPI/MLAPI_LoadBalanceInverseOperator.h
  MLAPI/MLAPI_Krylov.h
  MLAPI/MLAPI_MATLABStream.h
  MLAPI/MLAPI_SerialMatrix.h
  MLAPI/MLAPI_DistributedMatrix.h
  MLAPI/MLAPI_MultiLevelSA.h
  MLAPI/MLAPI_MultiLevelAdaptiveSA.h
  MLAPI/MLAPI_MultiVector.h
  MLAPI/MLAPI_MultiVector_Utils.h
  MLAPI/MLAPI_Operator_Box.h
  MLAPI/MLAPI_Operator.h
  MLAPI/MLAPI_LoadBalanceOperator.h
  MLAPI/MLAPI_Operator_Utils.h
  MLAPI/MLAPI_Space.h
  MLAPI/MLAPI_TimeObject.h
  MLAPI/MLAPI_Workspace.h
  MLAPI/MLAPI_Error.h
  MLAPI/MLAPI_SAMIS.h
  MLAPI/MLAPI_LinearCombinations.h
  MLAPI/MLAPI_BaseLinearCombination.h
  LevelWrap/ml_LevelWrap.h
  )

APPEND_SET(SOURCES
  Utils/ml_rbm.c
  Utils/ml_aztec_utils.c
  Utils/ml_read_utils.c
  Utils/ml_twogrid_analysis.c
  Utils/ml_epetra_utils.cpp
  Utils/ml_utils.c
  Utils/ml_intlist.c
  Utils/ml_vec.c
  Utils/ml_memory.c
  Utils/ml_eigf2c.c
  Utils/ml_agg_info.c
  Utils/ml_viz_opendx.c
  Utils/ml_viz_xyz.c
  Utils/ml_viz_vtk.c
  Utils/ml_amesos.c
  Utils/ml_amesos_wrap.cpp
  Utils/ml_ifpack.c
  Utils/ml_ifpack_wrap.cpp
  Utils/ml_ifpack_epetra_wrap.cpp
  Utils/ml_self.c
  Utils/ml_self_wrap.cpp
  Utils/ml_MultiLevelPreconditioner.cpp
  Utils/ml_MultiLevelPreconditioner_Filtering.cpp
  Utils/ml_MultiLevelPreconditioner_NullSpace.cpp
  Utils/ml_MultiLevelPreconditioner_Defaults.cpp
  Utils/ml_MultiLevelPreconditioner_Smoothers.cpp
  Utils/ml_MultiLevelPreconditioner_Viz.cpp
  Utils/ml_MultiLevelPreconditioner_Adapt.cpp
  Utils/ml_MultiLevelPreconditioner_Analyze.cpp
  Utils/ml_MultiLevelPreconditioner_Test.cpp
  Utils/ml_MultiLevelPreconditioner_Aux.cpp
  Utils/ml_MultiLevelPreconditioner_XML.cpp
  Utils/ml_anasazi.cpp
  Utils/ml_MultiLevelOperator.cpp
  Utils/ml_RowMatrix.cpp
  Utils/ml_DD_prec.cpp
  Utils/Epetra_Multi_CrsMatrix.cpp
  Utils/ml_ValidateParameters.cpp
  RefMaxwell/ml_RefMaxwell_Utils.cpp
  RefMaxwell/ml_FaceMatrixFreePreconditioner.cpp
  RefMaxwell/ml_EdgeMatrixFreePreconditioner.cpp
  RefMaxwell/ml_RefMaxwell_11_Operator.cpp
  RefMaxwell/ml_RefMaxwell.cpp
  RefMaxwell/ml_GradDiv.cpp
  MatrixFree/ml_MatrixFreePreconditioner.cpp
  MLAPI/MLAPI_Defaults.cpp
  MLAPI/MLAPI_Gallery.cpp
  MLAPI/MLAPI_InverseOperator.cpp
  MLAPI/MLAPI_LoadBalanceInverseOperator.cpp
  MLAPI/MLAPI_Operator_Utils.cpp
  MLAPI/MLAPI_Eig.cpp
  MLAPI/MLAPI_Krylov.cpp
  MLAPI/MLAPI_Workspace.cpp
  MLAPI/MLAPI_Expressions.cpp
  MLAPI/MLAPI_MultiVector_Utils.cpp
  MLAPI/MLAPI_BaseObject.cpp
  MLAPI/MLAPI_Aggregation.cpp
  MLAPI/MLAPI_Error.cpp
  MLAPI/MLAPI_DistributedMatrix.cpp
  MLAPI/MLAPI_SAMIS.cpp
  MLAPI/MLAPI_LinearCombinations.cpp
  LevelWrap/ml_LevelWrap.cpp
  )

#
# C) Define the targets for package's library(s)
#

TRIBITS_ADD_LIBRARY(
  ml
  HEADERS ${HEADERS}
  SOURCES ${SOURCES}
  )

if (WIN32)
	target_link_libraries (ml PUBLIC ws2_32)
endif ()
