package(default_visibility = ["//visibility:public"])

licenses(["notice"])  # Apache 2.0

cc_library(
    name = "preprocessor",
    srcs = ["preprocessor.cc"],
    hdrs = ["preprocessor.h"],
    deps = [
        "//tensorflow/lite/delegates/gpu/common:status",
        "@com_google_absl//absl/strings",
    ],
)

cc_test(
    name = "preprocessor_test",
    srcs = ["preprocessor_test.cc"],
    tags = [
        "local",
    ],
    deps = [
        ":preprocessor",
        "@com_google_googletest//:gtest_main",
    ],
)

cc_library(
    name = "parameter_accessor",
    srcs = ["parameter_accessor.cc"],
    hdrs = ["parameter_accessor.h"],
    deps = [
        ":preprocessor",
        "//tensorflow/lite/delegates/gpu/common:types",
        "//tensorflow/lite/delegates/gpu/gl:uniform_parameter",
        "@com_google_absl//absl/strings",
        "@com_google_absl//absl/strings:str_format",
        "@com_google_absl//absl/types:variant",
    ],
)

cc_test(
    name = "parameter_accessor_test",
    srcs = ["parameter_accessor_test.cc"],
    tags = [
        "local",
    ],
    deps = [
        ":parameter_accessor",
        "//tensorflow/lite/delegates/gpu/common:types",
        "@com_google_googletest//:gtest_main",
    ],
)

cc_library(
    name = "object_accessor",
    srcs = ["object_accessor.cc"],
    hdrs = ["object_accessor.h"],
    deps = [
        ":parameter_accessor",
        ":preprocessor",
        "//tensorflow/lite/delegates/gpu/common:data_type",
        "//tensorflow/lite/delegates/gpu/common:types",
        "//tensorflow/lite/delegates/gpu/gl:object",
        "@com_google_absl//absl/strings",
        "@com_google_absl//absl/strings:str_format",
        "@com_google_absl//absl/types:variant",
    ],
)

cc_test(
    name = "object_accessor_test",
    srcs = ["object_accessor_test.cc"],
    tags = [
        "local",
    ],
    deps = [
        ":object_accessor",
        ":parameter_accessor",
        "//tensorflow/lite/delegates/gpu/common:types",
        "@com_google_absl//absl/types:variant",
        "@com_google_googletest//:gtest_main",
    ],
)

cc_library(
    name = "shader_code",
    hdrs = ["shader_code.h"],
    deps = [
        "//tensorflow/lite/delegates/gpu/common:model",
        "//tensorflow/lite/delegates/gpu/common:types",
        "//tensorflow/lite/delegates/gpu/gl:object",
        "//tensorflow/lite/delegates/gpu/gl:uniform_parameter",
    ],
)

cc_library(
    name = "shader_codegen",
    srcs = ["shader_codegen.cc"],
    hdrs = ["shader_codegen.h"],
    deps = [
        ":compiled_node",
        ":object_accessor",
        ":parameter_accessor",
        ":preprocessor",
        ":shader_code",
        "//tensorflow/lite/delegates/gpu/common:model",
        "//tensorflow/lite/delegates/gpu/common:status",
        "//tensorflow/lite/delegates/gpu/gl:compiler_options",
        "//tensorflow/lite/delegates/gpu/gl:gpu_info",
        "//tensorflow/lite/delegates/gpu/gl:object",
        "@com_google_absl//absl/strings",
    ],
)

cc_library(
    name = "compiled_node",
    srcs = ["compiled_node.cc"],
    hdrs = ["compiled_node.h"],
    deps = [
        ":rename",
        "//tensorflow/lite/delegates/gpu/common:model",
        "//tensorflow/lite/delegates/gpu/common:status",
        "//tensorflow/lite/delegates/gpu/gl:node_shader",
        "//tensorflow/lite/delegates/gpu/gl:object",
        "@com_google_absl//absl/strings",
    ],
)

cc_library(
    name = "fuse_inplace",
    srcs = ["fuse_inplace.cc"],
    hdrs = ["fuse_inplace.h"],
    deps = [
        ":compiled_node",
        ":preprocessor",
        "//tensorflow/lite/delegates/gpu/common:model",
        "//tensorflow/lite/delegates/gpu/common:model_transformer",
        "//tensorflow/lite/delegates/gpu/common:types",
        "//tensorflow/lite/delegates/gpu/gl:node_shader",
        "@com_google_absl//absl/strings",
        "@com_google_absl//absl/types:any",
    ],
)

cc_library(
    name = "fuse_inline",
    srcs = ["fuse_inline.cc"],
    hdrs = ["fuse_inline.h"],
    deps = [
        ":compiled_node",
        ":shader_code",
        "//tensorflow/lite/delegates/gpu/common:model",
        "//tensorflow/lite/delegates/gpu/common:model_transformer",
        "//tensorflow/lite/delegates/gpu/common:status",
        "//tensorflow/lite/delegates/gpu/common:types",
        "//tensorflow/lite/delegates/gpu/gl:node_shader",
        "@com_google_absl//absl/strings",
        "@com_google_absl//absl/types:any",
    ],
)

cc_library(
    name = "rename",
    srcs = ["rename.cc"],
    hdrs = ["rename.h"],
    deps = [
        ":object_accessor",
        ":parameter_accessor",
        ":preprocessor",
        "//tensorflow/lite/delegates/gpu/common:status",
        "//tensorflow/lite/delegates/gpu/gl:node_shader",
        "//tensorflow/lite/delegates/gpu/gl:object",
        "//tensorflow/lite/delegates/gpu/gl:uniform_parameter",
        "@com_google_absl//absl/strings",
    ],
)

cc_library(
    name = "fuse_auto_input",
    srcs = ["fuse_auto_input.cc"],
    hdrs = ["fuse_auto_input.h"],
    deps = [
        ":compiled_node",
        "//tensorflow/lite/delegates/gpu/common:model",
        "//tensorflow/lite/delegates/gpu/common:model_transformer",
        "//tensorflow/lite/delegates/gpu/common:operations",
        "//tensorflow/lite/delegates/gpu/common:types",
        "@com_google_absl//absl/strings",
        "@com_google_absl//absl/types:any",
        "@com_google_absl//absl/types:variant",
    ],
)
