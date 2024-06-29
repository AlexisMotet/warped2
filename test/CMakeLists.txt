set(TESTS 
    test_AggregateEventStatistics
    test_CircularQueue
    test_CommandLineConfiguration
    test_Event
    test_IndividualEventStatistics
    test_LPState
    test_LadderQueue
    test_LogicalProcess
    test_ProfileGuidedPartitioner
    test_RandomNumberGenerator
    test_RoundRobinPartitioner
    test_STLLTSFQueue
    test_Simulation
    test_SplayTree
    test_TimeWarpAggressiveOutputManager
    test_TimeWarpAsynchronousGVTManager
    test_TimeWarpEventSet
    test_TimeWarpFileStreamManager
    test_TimeWarpPeriodicStateManager
    test_serialization
)

find_package(MPI REQUIRED)

foreach(test_name ${TESTS})
    add_executable(${test_name} ${test_name}.cpp
        $<TARGET_OBJECTS:json>
        $<TARGET_OBJECTS:GKlib> 
        $<TARGET_OBJECTS:metis> 
        $<TARGET_OBJECTS:warped2_object> 
    )
    target_link_libraries(${test_name} PRIVATE MPI::MPI_CXX)
    target_include_directories(${test_name} PRIVATE ../src ../deps/cereal-1.1.1/include ../deps/tclap-1.2.5/include ../deps)
    add_test(NAME ${test_name} COMMAND ${test_name})
endforeach()
