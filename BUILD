load("@graknlabs_bazel_distribution//common:rules.bzl", "assemble_targz", "java_deps")

filegroup(
    name = "simulation-files",
    srcs = glob([
        "data/*.yaml",
        "schema/*.gql",
    ]),
)

java_library(
    name = "simulation",
    srcs = glob(["*.java"]),
    data = [":simulation-files"],
    resources = [
        "conf/logback.xml",
    ],
    resource_strip_prefix = "conf/",
    deps = [
        "@graknlabs_client_java//:client-java",
        "@graknlabs_graql//java:graql",
        "//dependencies/maven/artifacts/commons-cli:commons-cli",
        "//common:common",
        "//yaml_tool:yaml_tool",
        "//agents:agents",
    ],
    visibility = ["//visibility:public"],
)

java_binary(
    name = "simulation-binary",
    main_class = "grakn.simulation.Simulation",
    runtime_deps = [":simulation"],
    visibility = ["//:__pkg__"],
)

java_deps(
    name = "simulation-deps",
    target = ":simulation-binary",
    java_deps_root = "lib/",
    visibility = ["//visibility:public"],
)

assemble_targz(
    name = "assemble-linux-targz",
    output_filename = "grakn-simulation-linux",
    targets = [":simulation-deps", "//bin:assemble-bash-targz"],
    additional_files = {
        "data/data.yaml": "data/data.yaml", # TODO fix this hack
        "schema/schema.gql": "schema/schema.gql",
    },
    visibility = ["//visibility:public"],
)