cmake_minimum_required(VERSION 2.8)
project(darknet C CXX)

set (EXECUTABLE_OUTPUT_PATH ${CMAKE_SOURCE_DIR})
set (LIBRARY_OUTPUT_PATH ${CMAKE_SOURCE_DIR})

FIND_PACKAGE(Threads)
FIND_PACKAGE(OpenCV REQUIRED)


set(LIB_SRC ${PROJECT_SOURCE_DIR}/src/gemm.c
            ${PROJECT_SOURCE_DIR}/src/utils.c
            ${PROJECT_SOURCE_DIR}/src/cuda.c
            ${PROJECT_SOURCE_DIR}/src/deconvolutional_layer.c
            ${PROJECT_SOURCE_DIR}/src/convolutional_layer.c
            ${PROJECT_SOURCE_DIR}/src/list.c
            ${PROJECT_SOURCE_DIR}/src/image.c
            ${PROJECT_SOURCE_DIR}/src/activations.c
            ${PROJECT_SOURCE_DIR}/src/im2col.c
            ${PROJECT_SOURCE_DIR}/src/col2im.c
            ${PROJECT_SOURCE_DIR}/src/blas.c
            ${PROJECT_SOURCE_DIR}/src/crop_layer.c
            ${PROJECT_SOURCE_DIR}/src/dropout_layer.c
            ${PROJECT_SOURCE_DIR}/src/maxpool_layer.c
            ${PROJECT_SOURCE_DIR}/src/softmax_layer.c
            ${PROJECT_SOURCE_DIR}/src/data.c
            ${PROJECT_SOURCE_DIR}/src/matrix.c
            ${PROJECT_SOURCE_DIR}/src/network.c
            ${PROJECT_SOURCE_DIR}/src/connected_layer.c
            ${PROJECT_SOURCE_DIR}/src/cost_layer.c
            ${PROJECT_SOURCE_DIR}/src/parser.c
            ${PROJECT_SOURCE_DIR}/src/option_list.c
            ${PROJECT_SOURCE_DIR}/src/detection_layer.c
            ${PROJECT_SOURCE_DIR}/src/route_layer.c
            ${PROJECT_SOURCE_DIR}/src/upsample_layer.c
            ${PROJECT_SOURCE_DIR}/src/box.c
            ${PROJECT_SOURCE_DIR}/src/normalization_layer.c
            ${PROJECT_SOURCE_DIR}/src/avgpool_layer.c
            ${PROJECT_SOURCE_DIR}/src/layer.c
            ${PROJECT_SOURCE_DIR}/src/local_layer.c
            ${PROJECT_SOURCE_DIR}/src/shortcut_layer.c
            ${PROJECT_SOURCE_DIR}/src/logistic_layer.c
            ${PROJECT_SOURCE_DIR}/src/activation_layer.c
            ${PROJECT_SOURCE_DIR}/src/rnn_layer.c
            ${PROJECT_SOURCE_DIR}/src/gru_layer.c
            ${PROJECT_SOURCE_DIR}/src/crnn_layer.c
            ${PROJECT_SOURCE_DIR}/src/demo.c
            ${PROJECT_SOURCE_DIR}/src/batchnorm_layer.c
            ${PROJECT_SOURCE_DIR}/src/region_layer.c
            ${PROJECT_SOURCE_DIR}/src/reorg_layer.c
            ${PROJECT_SOURCE_DIR}/src/tree.c
            ${PROJECT_SOURCE_DIR}/src/lstm_layer.c
            ${PROJECT_SOURCE_DIR}/src/l2norm_layer.c
            ${PROJECT_SOURCE_DIR}/src/yolo_layer.c
            ${PROJECT_SOURCE_DIR}/src/iseg_layer.c
            ${PROJECT_SOURCE_DIR}/src/image_opencv.cpp)

set(EXEC_SRC ${PROJECT_SOURCE_DIR}/examples/captcha.c
            ${PROJECT_SOURCE_DIR}/examples/lsd.c
            ${PROJECT_SOURCE_DIR}/examples/super.c
            ${PROJECT_SOURCE_DIR}/examples/art.c
            ${PROJECT_SOURCE_DIR}/examples/tag.c
            ${PROJECT_SOURCE_DIR}/examples/cifar.c
            ${PROJECT_SOURCE_DIR}/examples/go.c
            ${PROJECT_SOURCE_DIR}/examples/rnn.c
            ${PROJECT_SOURCE_DIR}/examples/segmenter.c
            ${PROJECT_SOURCE_DIR}/examples/regressor.c
            ${PROJECT_SOURCE_DIR}/examples/classifier.c
            ${PROJECT_SOURCE_DIR}/examples/coco.c
            ${PROJECT_SOURCE_DIR}/examples/yolo.c
            ${PROJECT_SOURCE_DIR}/examples/detector.c
            ${PROJECT_SOURCE_DIR}/examples/nightmare.c
            ${PROJECT_SOURCE_DIR}/examples/instance-segmenter.c
            ${PROJECT_SOURCE_DIR}/examples/darknet.c)

add_library(darknetlib STATIC ${LIB_SRC})

target_include_directories(darknetlib PUBLIC ${PROJECT_SOURCE_DIR}/include)
#PRIVATE ${OpenCV_INCLUDE_DIR})

target_link_libraries(darknetlib ${CMAKE_THREAD_LIBS_INIT})# ${OpenCV_LIBS})
add_executable(darknet ${EXEC_SRC})
target_link_libraries(darknet darknetlib)
