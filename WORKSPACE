workspace(name = "buildifier_prebuilt")

load(":deps.bzl", "buildifier_prebuilt_deps")

buildifier_prebuilt_deps()

load("@bazel_skylib//:workspace.bzl", "bazel_skylib_workspace")

bazel_skylib_workspace()

load(":defs.bzl", "buildifier_prebuilt_register_toolchains")

buildifier_prebuilt_register_toolchains()

# MARK: - Test and Release Dependencies

load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")

http_archive(
    name = "cgrindel_bazel_starlib",
    sha256 = "75ede4943a0000661cab0a4495bd10ddfc45bc73df83677eb75f49202ea09a34",
    strip_prefix = "bazel-starlib-0.5.0",
    urls = [
        "http://github.com/cgrindel/bazel-starlib/archive/v0.5.0.tar.gz",
    ],
)

load("@cgrindel_bazel_starlib//:deps.bzl", "bazel_starlib_dependencies")

bazel_starlib_dependencies()

http_archive(
    name = "contrib_rules_bazel_integration_test",
    sha256 = "ab9bbf776b5874f8a02f639fec2fbb3e3eefa4403cf861ae00d7c7e4d757f9ff",
    strip_prefix = "rules_bazel_integration_test-0.6.2",
    urls = [
        "http://github.com/bazel-contrib/rules_bazel_integration_test/archive/v0.6.2.tar.gz",
    ],
)

load("@contrib_rules_bazel_integration_test//bazel_integration_test:deps.bzl", "bazel_integration_test_rules_dependencies")

bazel_integration_test_rules_dependencies()

load("@contrib_rules_bazel_integration_test//bazel_integration_test:defs.bzl", "bazel_binaries")
load("//:bazel_versions.bzl", "SUPPORTED_BAZEL_VERSIONS")

bazel_binaries(versions = SUPPORTED_BAZEL_VERSIONS)
