# Description: IntelliJ protobuf plugin - Go language support integration tests.
#

licenses(["notice"])  # Apache 2.0

package(default_visibility = ["//visibility:private"])

load(
    "//build_support/build_defs:build_defs.bzl",
    "stamped_plugin_xml",
    "optional_plugin_xml",
    "intellij_plugin",
)
load(
    "//build_support/testing:test_defs.bzl",
    "intellij_integration_test_suite",
)
load(
    "//golang/src/itest/resources:defs.bzl",
    "resources_import_prefix",
    "resources_package_name",
)

stamped_plugin_xml(
    name = "stamped_plugin_xml",
    plugin_id = "idea.plugin.protoeditor.golang",
    plugin_name = "Protocol Buffer Editor w/ Go Support",
)

intellij_plugin(
    name = "plugin_for_tests",
    optional_plugin_xmls = [
        ":optional_xml",
    ],
    plugin_xml = ":stamped_plugin_xml",
    deps = [
        "//core:plugin_library",
        "//golang:plugin_library",
    ],
)

optional_plugin_xml(
    name = "optional_xml",
    module = "org.jetbrains.plugins.go",
    plugin_xml = "//golang/src/itest/resources:META-INF/golang_optional.xml",
)

intellij_integration_test_suite(
    name = "integration_tests",
    srcs = glob(["java/**/*.java"]),
    data = ["//golang/src/itest/resources"],
    jvm_flags = [
        "-Dtest.resources.package.name=" + resources_package_name(),
        "-Dtest.resources.import.prefix=" + resources_import_prefix(),
        "-Dtest.resources.location=" + package_name() + "/resources/",
    ],
    required_plugins = "idea.plugin.protoeditor.golang,org.jetbrains.plugins.go",
    test_package_root = "idea.plugin.protoeditor",
    visibility = ["//visibility:public"],
    runtime_deps = [
        ":plugin_for_tests",
    ],
    deps = [
        "//build_support:test_plugin_api",
        "//build_support:test_plugin_go_support",
        "//build_support:test_libs",
        "//testlib:gencodeutils",
        "//testlib:test_utils",
    ],
)
