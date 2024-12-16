cmake_minimum_required(VERSION 2.8.3)
project(vins_estimator)

set(CMAKE_BUILD_TYPE "Release")
set(CMAKE_CXX_FLAGS "-std=c++14")
#-DEIGEN_USE_MKL_ALL")
set(CMAKE_CXX_FLAGS_RELEASE "-O3 -Wall -g -pthread -fopenmp")

include_directories(${CMAKE_SOURCE_DIR}/./include)
#add_library( lib_camera_model STATIC IMPORTED )
#set_target_properties(lib_camera_model PROPERTIES IMPORTED_LOCATION  ${CMAKE_SOURCE_DIR}/./build/libcamera_model.a)

find_package(OpenCV 4 REQUIRED)

include_directories(
					/usr/local/include/
					${OpenCV_INCLUDE_DIRS}
					)


find_package(Ceres REQUIRED)

include_directories(${CERES_INCLUDE_DIRS})



#message("CERES_INCLUDE_DIR:" ${CERES_INCLUDE_DIR}  " CERES_LIBS: "  ${CERES_LIBRARIES} )
#set(CMAKE_MODULE_PATH ${PROJECT_SOURCE_DIR}/cmake)
#message("CMAKE MOUDLE PATH:", ${CMAKE_MODULE_PATH})
#find_package(Eigen3  REQUIRED)
include_directories(
# ${EIGEN3_INCLUDE_DIR}
		/usr/include/eigen3
)

	
find_package(Boost REQUIRED COMPONENTS filesystem program_options system)

find_package(Pangolin REQUIRED)
include_directories(${Pangolin_INCLUDE_DIRS})

include_directories(${Boost_INCLUDE_DIRS})
add_executable(vins_estimator
    src/estimator_node.cpp
    src/parameters.cpp
    src/estimator.cpp
    src/feature_manager.cpp
    src/factor/pose_local_parameterization.cpp
    src/factor/projection_factor.cpp
    src/factor/marginalization_factor.cpp
    src/utility/utility.cpp
    src/utility/visualization.cpp
#    src/utility/CameraPoseVisualization.cpp
    src/initial/solve_5pts.cpp
    src/initial/initial_aligment.cpp
    src/initial/initial_sfm.cpp
    src/initial/initial_ex_rotation.cpp
    src/loop-closure/ThirdParty/DBoW/BowVector.cpp
    src/loop-closure/ThirdParty/DBoW/FBrief.cpp
    src/loop-closure/ThirdParty/DBoW/FeatureVector.cpp
    src/loop-closure/ThirdParty/DBoW/QueryResults.cpp
    src/loop-closure/ThirdParty/DBoW/ScoringObject.cpp
    src/loop-closure/ThirdParty/DUtils/Random.cpp
    src/loop-closure/ThirdParty/DUtils/Timestamp.cpp
    src/loop-closure/ThirdParty/DVision/BRIEF.cpp
    src/loop-closure/ThirdParty/VocabularyBinary.cpp
    src/loop-closure/loop_closure.cpp
    src/loop-closure/keyframe.cpp
    src/loop-closure/keyframe_database.cpp
    src/feature_tracker/feature_tracker.cpp 
  #  src/feature_tracker/feature_tracker_parameters.cpp
    src/camera_models/Camera.cc
    src/camera_models/CameraFactory.cc
    src/camera_models/CostFunctionFactory.cc
    src/camera_models/PinholeCamera.cc
    src/camera_models/CataCamera.cc
    src/camera_models/EquidistantCamera.cc
    src/camera_models/ScaramuzzaCamera.cc
    src/camera_models/gpl.cc
    )


target_link_libraries(vins_estimator #lib_camera_model 
					#opencv_calib3d opencv_core opencv_features2d opencv_flann opencv_highgui opencv_imgcodecs opencv_imgproc opencv_ml opencv_objdetect opencv_photo opencv_shape opencv_stitching opencv_superres opencv_video opencv_videoio opencv_videostab opencv_viz   
					${Pangolin_LIBRARIES}
					${CERES_LIBRARIES}
          ${OpenCV_LIBS}
#					suitesparse cxsparse cholmod atlas lapack_atlas
#					glog
#					ceres
		) 


