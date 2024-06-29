cmake_minimum_required(VERSION 3.23)
enable_testing()
project(warped2 VERSION 5.0.0 DESCRIPTION "warped2" LANGUAGES C CXX)
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)
set(CMAKE_CXX_STANDARD 17)

add_library(json OBJECT)
target_sources(json PRIVATE
    deps/json/jsoncpp.cpp
)
target_include_directories(json PRIVATE deps/json)

add_library(GKlib OBJECT)
target_sources(GKlib PRIVATE
    deps/metis/GKlib/b64.c
    deps/metis/GKlib/blas.c
    deps/metis/GKlib/csr.c
    deps/metis/GKlib/error.c
    deps/metis/GKlib/evaluate.c
    deps/metis/GKlib/fkvkselect.c
    deps/metis/GKlib/fs.c
    deps/metis/GKlib/getopt.c
    deps/metis/GKlib/gkregex.c
    deps/metis/GKlib/graph.c
    deps/metis/GKlib/htable.c
    deps/metis/GKlib/io.c
    deps/metis/GKlib/itemsets.c
    deps/metis/GKlib/mcore.c
    deps/metis/GKlib/memory.c
    deps/metis/GKlib/omp.c
    deps/metis/GKlib/pdb.c
    deps/metis/GKlib/pqueue.c
    deps/metis/GKlib/random.c
    deps/metis/GKlib/rw.c
    deps/metis/GKlib/seq.c
    deps/metis/GKlib/sort.c
    deps/metis/GKlib/string.c
    deps/metis/GKlib/timers.c
    deps/metis/GKlib/tokenizer.c
    deps/metis/GKlib/util.c
)
target_include_directories(GKlib PRIVATE deps/metis/GKlib)

add_library(metis OBJECT)
target_sources(metis PRIVATE
    deps/metis/libmetis/auxapi.c
    deps/metis/libmetis/balance.c
    deps/metis/libmetis/bucketsort.c
    deps/metis/libmetis/checkgraph.c
    deps/metis/libmetis/coarsen.c
    deps/metis/libmetis/compress.c
    deps/metis/libmetis/contig.c
    deps/metis/libmetis/debug.c
    deps/metis/libmetis/defs.h
    deps/metis/libmetis/fm.c
    deps/metis/libmetis/fortran.c
    deps/metis/libmetis/frename.c
    deps/metis/libmetis/gklib.c
    deps/metis/libmetis/gklib_defs.h
    deps/metis/libmetis/gklib_rename.h
    deps/metis/libmetis/graph.c
    deps/metis/libmetis/initpart.c
    deps/metis/libmetis/kmetis.c
    deps/metis/libmetis/kwayfm.c
    deps/metis/libmetis/kwayrefine.c
    deps/metis/libmetis/macros.h
    deps/metis/libmetis/mcutil.c
    deps/metis/libmetis/mesh.c
    deps/metis/libmetis/meshpart.c
    deps/metis/libmetis/metislib.h
    deps/metis/libmetis/minconn.c
    deps/metis/libmetis/mincover.c
    deps/metis/libmetis/mmd.c
    deps/metis/libmetis/ometis.c
    deps/metis/libmetis/options.c
    deps/metis/libmetis/parmetis.c
    deps/metis/libmetis/pmetis.c
    deps/metis/libmetis/proto.h
    deps/metis/libmetis/refine.c
    deps/metis/libmetis/rename.h
    deps/metis/libmetis/separator.c
    deps/metis/libmetis/sfm.c
    deps/metis/libmetis/srefine.c
    deps/metis/libmetis/stat.c
    deps/metis/libmetis/stdheaders.h
    deps/metis/libmetis/struct.h
    deps/metis/libmetis/timing.c
    deps/metis/libmetis/util.c
    deps/metis/libmetis/wspace.c
)

target_include_directories(metis PRIVATE deps/metis/libmetis deps/metis/include deps/metis/GKlib)

add_library(warped2_object OBJECT)
target_sources(warped2_object PRIVATE
    src/AggregateEventStatistics.cpp
    src/CommandLineConfiguration.cpp
    src/Configuration.cpp
    src/EventStatistics.cpp
    src/FileStream.cpp
    src/IndividualEventStatistics.cpp
    src/LadderQueue.cpp
    src/LogicalProcess.cpp
    src/ProfileGuidedPartitioner.cpp
    src/RoundRobinPartitioner.cpp
    src/STLLTSFQueue.cpp
    src/SequentialEventDispatcher.cpp
    src/SplayTree.cpp
    src/Simulation.cpp
    src/TimeWarpAggressiveOutputManager.cpp
    src/TimeWarpAsynchronousGVTManager.cpp
    src/TimeWarpCommunicationManager.cpp
    src/TimeWarpEventDispatcher.cpp
    src/TimeWarpEventSet.cpp
    src/TimeWarpFileStream.cpp
    src/TimeWarpFileStreamManager.cpp
    src/TimeWarpGVTManager.cpp
    src/TimeWarpMPICommunicationManager.cpp
    src/TimeWarpOutputManager.cpp
    src/TimeWarpPeriodicStateManager.cpp
    src/TimeWarpStateManager.cpp
    src/TimeWarpStatistics.cpp
    # src/TimeWarpSynchronousGVTManager.cpp
    src/TimeWarpTerminationManager.cpp
)
target_include_directories(warped2_object PRIVATE deps deps/cereal-1.1.1/include deps/tclap-1.2.5/include)

add_subdirectory(test)