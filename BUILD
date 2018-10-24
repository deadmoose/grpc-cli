load("@io_bazel_rules_docker//cc:image.bzl", "cc_image")
load("@io_bazel_rules_docker//oci:oci.bzl", "container_push")

cc_image(
    name = "grpc_cli",
    binary = "@com_github_grpc_grpc//test/cpp/util:grpc_cli",
)

# TODO(deadmoose): Figure out pushing
container_push(
    name = "publish",
    format = "Docker",
    image = ":grpc_cli",
    registry = "index.docker.io",
    repository = "deadmoose/grpc-cli",
)
