load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")

#############################################################################
#                                                                           #
#                             Python Rules                                  #
#                                                                           #
#############################################################################
http_archive(
    name = "rules_python",
    sha256 = "a3a6e99f497be089f81ec082882e40246bfd435f52f4e82f37e89449b04573f6",
    strip_prefix = "rules_python-0.10.2",
    url = "https://github.com/bazelbuild/rules_python/archive/refs/tags/0.10.2.tar.gz",
)

load("@rules_python//python:repositories.bzl", "python_register_toolchains")

python_register_toolchains(
    name = "python3_10",
    # Available versions are listed in @rules_python//python:versions.bzl.
    # We recommend using the same version your team is already standardized on.
    python_version = "3.10",
)

load("@python3_10//:defs.bzl", "interpreter")
load("@rules_python//python:pip.bzl", "pip_parse")

pip_parse(
    name = "pip_deps",
    python_interpreter_target = interpreter,
    requirements_lock = "//python:requirements.txt",
)

load("@pip_deps//:requirements.bzl", install_pip_deps = "install_deps")

install_pip_deps()

#############################################################################
#                                                                           #
#                              gRPC Rules                                   #
#                                                                           #
#############################################################################
http_archive(
    name = "com_github_grpc_grpc",
    patches = ["//patches:grpc.patch"],
    sha256 = "9717ffc52120861136e478155c2ff3a9c21740e2244de52fa966f376d7471adf",
    strip_prefix = "grpc-1.53.0",
    urls = ["https://github.com/grpc/grpc/archive/v1.53.0.tar.gz"],
)

load("@com_github_grpc_grpc//bazel:grpc_deps.bzl", "grpc_deps")

grpc_deps(
    python_headers = "@python3_10//:python_headers",
)

load("@com_github_grpc_grpc//bazel:grpc_extra_deps.bzl", "grpc_extra_deps")

grpc_extra_deps()
