workspace(name = "grpc_cli")

load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")

http_archive(
    name = "com_github_grpc_grpc",
    patches = ["patches/com_github_grpc_grpc/0001-Statically-link-grpc_cli.patch"],
    sha256 = "ceb8a753ea7e7d299197cdc7bac1d60c86e401dc8560c3c7530b39bc5fa0654f",
    strip_prefix = "grpc-1.16.0",
    urls = ["https://github.com/grpc/grpc/archive/v1.16.0.zip"],
)

http_archive(
    name = "io_bazel_rules_docker",
    sha256 = "29d109605e0d6f9c892584f07275b8c9260803bf0c6fcb7de2623b2bedc910bd",
    strip_prefix = "rules_docker-0.5.1",
    urls = ["https://github.com/bazelbuild/rules_docker/archive/v0.5.1.tar.gz"],
)

load(
    "@io_bazel_rules_docker//cc:image.bzl",
    _cc_image_repos = "repositories",
)

_cc_image_repos()

load("@com_github_grpc_grpc//bazel:grpc_deps.bzl", "grpc_deps", "grpc_test_only_deps")

grpc_deps()

grpc_test_only_deps()

new_http_archive(
    name = "cython",
    build_file = "//third_party:cython.BUILD",
    sha256 = "d68138a2381afbdd0876c3cb2a22389043fa01c4badede1228ee073032b07a27",
    strip_prefix = "cython-c2b80d87658a8525ce091cbe146cb7eaa29fed5c",
    urls = [
        "https://github.com/cython/cython/archive/c2b80d87658a8525ce091cbe146cb7eaa29fed5c.tar.gz",
    ],
)

load("@com_github_grpc_grpc//third_party/py:python_configure.bzl", "python_configure")

python_configure(name = "local_config_python")

git_repository(
    name = "io_bazel_rules_python",
    commit = "8b5d0683a7d878b28fffe464779c8a53659fc645",
    remote = "https://github.com/bazelbuild/rules_python.git",
)

load("@io_bazel_rules_python//python:pip.bzl", "pip_import", "pip_repositories")

pip_repositories()

pip_import(
    name = "grpc_python_dependencies",
    requirements = "@com_github_grpc_grpc//:requirements.bazel.txt",
)

load("@grpc_python_dependencies//:requirements.bzl", "pip_install")

pip_install()

git_repository(
    name = "org_pubref_rules_protobuf",
    remote = "https://github.com/pubref/rules_protobuf",
    tag = "v0.8.2",
)

load("@org_pubref_rules_protobuf//python:rules.bzl", "py_proto_repositories")

py_proto_repositories()
