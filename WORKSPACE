workspace(
    name = "angular_cli",
    managed_directories = {"@npm": ["node_modules"]},
)

load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")

http_archive(
    name = "build_bazel_rules_nodejs",
    sha256 = "f7037c8e295fdc921f714962aee7c496110052511e2b14076bd8e2d46bc9819c",
    urls = ["https://github.com/bazelbuild/rules_nodejs/releases/download/4.4.5/rules_nodejs-4.4.5.tar.gz"],
)

# Check the bazel version and download npm dependencies
load("@build_bazel_rules_nodejs//:index.bzl", "check_bazel_version", "check_rules_nodejs_version", "node_repositories", "yarn_install")

# Bazel version must be at least the following version because:
#   - 0.26.0 managed_directories feature added which is required for nodejs rules 0.30.0
#   - 0.27.0 has a fix for managed_directories after `rm -rf node_modules`
check_bazel_version(
    message = """
You no longer need to install Bazel on your machine.
Angular has a dependency on the @bazel/bazelisk package which supplies it.
Try running `yarn bazel` instead.
    (If you did run that, check that you've got a fresh `yarn install`)
""",
    minimum_bazel_version = "4.0.0",
)

check_rules_nodejs_version(minimum_version_string = "2.0.0")

# Setup the Node.js toolchain
node_repositories(
    node_version = "14.17.1",
    package_json = ["//:package.json"],
)

yarn_install(
    name = "npm",
    package_json = "//:package.json",
    yarn_lock = "//:yarn.lock",
)
