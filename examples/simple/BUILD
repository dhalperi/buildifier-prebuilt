load("@buildifier_prebuilt//:rules.bzl", "buildifier")

buildifier(
    name = "buildifier.check",
    exclude_patterns = [
        "./.git/*",
    ],
    lint_mode = "warn",
    lint_warnings = [
        # This demonstrates how one can enable all warnings and then disable
        # select categories.
        "all",
        "-cc-native",
    ],
    mode = "diff",
)

sh_binary(
    name = "hello_world",
    srcs = ["hello_world.sh"],
)

sh_test(
    name = "hello_world_test",
    srcs = ["hello_world_test.sh"],
    data = [
        ":hello_world",
    ],
    deps = [
        "@bazel_tools//tools/bash/runfiles",
    ],
)
