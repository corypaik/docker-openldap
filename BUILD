load(
    "//third_party/rules_docker/container:container.bzl",
    "container_image",
    "container_layer",
    "container_push",
)
load("//third_party/rules_pkg/pkg:tar.bzl", "pkg_tar")

pkg_tar(
    name = "service_tar",
    srcs = glob(["image/service/**"]),
    package_dir = "/container",
    strip_prefix = "image",
)

pkg_tar(
    name = "environment_tar",
    srcs = glob(["image/environment/**"]),
    package_dir = "/container",
    strip_prefix = "image",
)

container_image(
    name = "openldap_image",
    base = "@openldap_base//image",
    tars = [":service_tar", ":environment_tar"],
    visibility = ["//docker:__pkg__"],
)

container_push(
    name = "push",
    format = "OCI",
    registry = "ghcr.io",
    repository = "corypaik/openldap",
    image = ":openldap_image",
    visibility = ["//docker:__pkg__"],
)
