load("@graknlabs_bazel_distribution//common:rules.bzl", "assemble_targz")

exports_files(["simulation"])

assemble_targz(
    name = "assemble-bash-targz",
    additional_files = {
        "//bin:simulation": 'simulation',
    },
    permissions = {
        "grakn": "0755",
    },
    visibility = ["//visibility:public"],
)