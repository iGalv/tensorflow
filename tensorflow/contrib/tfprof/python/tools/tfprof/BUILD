licenses(["notice"])  # Apache 2.0

package(default_visibility = ["//visibility:public"])

load("//tensorflow:tensorflow.bzl", "tf_py_test")
load("//tensorflow:tensorflow.bzl", "tf_py_wrap_cc")

py_library(
    name = "model_analyzer",
    srcs = ["model_analyzer.py"],
    srcs_version = "PY2AND3",
    deps = [
        ":pywrap_tensorflow_print_model_analysis_lib",
        ":tfprof_logger",
        "//tensorflow/tools/tfprof:protos_all_py",
    ],
)

py_test(
    name = "model_analyzer_test",
    srcs = ["model_analyzer_test.py"],
    srcs_version = "PY2AND3",
    deps = [
        ":model_analyzer",
        "//tensorflow:tensorflow_py",
    ],
)

py_library(
    name = "tfprof_logger",
    srcs = ["tfprof_logger.py"],
    srcs_version = "PY2AND3",
    deps = [
        "//tensorflow/python:framework_for_generated_wrappers",
        "//tensorflow/tools/tfprof:protos_all_py",
        "@six_archive//:six",
    ],
)

tf_py_test(
    name = "tfprof_logger_test",
    srcs = ["tfprof_logger_test.py"],
    additional_deps = [
        ":tfprof_logger",
        "//tensorflow:tensorflow_py",
        "//tensorflow/tools/tfprof:protos_all_py",
    ],
)

tf_py_wrap_cc(
    name = "pywrap_tensorflow_print_model_analysis_lib",
    srcs = ["pywrap_tensorflow_print_model_analysis.i"],
    swig_includes = [
        "//tensorflow/python:lib/core/strings.i",
        "//tensorflow/python:platform/base.i",
    ],
    deps = [
        "//tensorflow/core:framework_headers_lib",
        "//tensorflow/tools/tfprof/internal:print_model_analysis_hdr",
        "//util/python:python_headers",
    ],
)

py_test(
    name = "print_model_analysis_test",
    srcs = ["print_model_analysis_test.py"],
    srcs_version = "PY2AND3",
    deps = [
        ":pywrap_tensorflow_print_model_analysis_lib",
        "//tensorflow:tensorflow_py",
        "//tensorflow/python:framework_test_lib",
        "//tensorflow/python:platform_test",
        "//tensorflow/tools/tfprof:protos_all_py",
    ],
)

# -----------------------------------------------------------------------------
# Google-internal targets.  These must be at the end for syncrepo.

filegroup(
    name = "all_files",
    srcs = glob(
        ["**/*"],
        exclude = [
            "**/METADATA",
            "**/OWNERS",
        ],
    ),
    visibility = ["//tensorflow:__subpackages__"],
)
