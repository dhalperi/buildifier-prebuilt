load(
    "@contrib_rules_bazel_integration_test//bazel_integration_test:defs.bzl",
    "bazel_integration_tests",
    "default_test_runner",
    "integration_test_utils",
)
load("//:bazel_versions.bzl", "SUPPORTED_BAZEL_VERSIONS")

# Add test for buildozer

default_test_runner(
    name = "default_test_runner",
    bazel_cmds = [
        "info",
        "run //:buildifier.check",
        "test //...",
    ],
)

sh_binary(
    name = "simple_test_runner",
    testonly = True,
    srcs = ["simple_test_runner.sh"],
    data = [
        "@contrib_rules_bazel_integration_test//tools:create_scratch_dir",
    ],
    deps = [
        "@bazel_tools//tools/bash/runfiles",
        "@cgrindel_bazel_starlib//shlib/lib:assertions",
    ],
)

bazel_integration_tests(
    name = "simple_test",
    bazel_versions = SUPPORTED_BAZEL_VERSIONS,
    test_runner = ":simple_test_runner",
    workspace_files = integration_test_utils.glob_workspace_files("simple") + [
        "//:local_repository_files",
    ],
    workspace_path = "simple",
)

bazel_integration_tests(
    name = "specify_assets_test",
    bazel_versions = SUPPORTED_BAZEL_VERSIONS,
    test_runner = ":default_test_runner",
    workspace_files = integration_test_utils.glob_workspace_files("specify_assets") + [
        "//:local_repository_files",
    ],
    workspace_path = "specify_assets",
)

test_suite(
    name = "integration_tests",
    # If you don't apply the test tags to the test suite, the test suite will
    # be found when `bazel test //...` is executed.
    tags = integration_test_utils.DEFAULT_INTEGRATION_TEST_TAGS,
    tests = integration_test_utils.bazel_integration_test_names(
        "simple_test",
        SUPPORTED_BAZEL_VERSIONS,
    ) + integration_test_utils.bazel_integration_test_names(
        "specify_assets_test",
        SUPPORTED_BAZEL_VERSIONS,
    ),
    visibility = ["//:__subpackages__"],
)
