licenses(["notice"])  # Apache 2

# Trace driver for Datadog (https://datadoghq.com/)

load(
    "//bazel:envoy_build_system.bzl",
    "envoy_cc_extension",
    "envoy_cc_library",
    "envoy_package",
)

envoy_package()

envoy_cc_library(
    name = "datadog_tracer_lib",
    srcs = [
        "datadog_tracer_impl.cc",
    ],
    hdrs = [
        "datadog_tracer_impl.h",
    ],
    external_deps = ["dd_opentracing_cpp"],
    deps = [
        "//source/common/config:utility_lib",
        "//source/common/tracing:http_tracer_lib",
        "//source/extensions/tracers:well_known_names",
        "//source/extensions/tracers/common/ot:opentracing_driver_lib",
        "@envoy_api//envoy/config/trace/v3alpha:pkg_cc_proto",
    ],
)

envoy_cc_extension(
    name = "config",
    srcs = ["config.cc"],
    hdrs = ["config.h"],
    security_posture = "robust_to_untrusted_downstream",
    deps = [
        ":datadog_tracer_lib",
        "//source/extensions/tracers:well_known_names",
        "//source/extensions/tracers/common:factory_base_lib",
        "@envoy_api//envoy/config/trace/v3alpha:pkg_cc_proto",
    ],
)
