This repo simply illustrates an issue I'm having with Bazel 9.0.0 and the `toolchains_llvm_bootstrapped` repo building `mimick`. This library builds correctly with `toolchains_llvm`. Install `bazelisk` and run:

```bash
git clone --recurse-submodules https://github.com/asymingt/bazel_toolchain_issue.git
cd bazel_toolchain_issue
bazel test @mimick//...
```

Look at [MODULE.bazel](MODULE.bazel) and you will see OPTION 1 (toolchains_llvm_boostrapped) and OPTION 2 (toolchains_llvm). You can comment out one and then use the other to switch between working and not working.

```
###########################
# OPTION 1: DOES NOT WORK
toolchain = use_extension("@toolchains_llvm_bootstrapped//extensions:toolchain.bzl", "toolchain")
toolchain.exec(
    arch = "x86_64",
    os = "linux",
)
toolchain.target(
    arch = "x86_64",
    os = "linux",
)
use_repo(toolchain, "llvm_toolchains")

register_toolchains("@llvm_toolchains//:all")
############################

############################
# OPTION 2 : WORKS
# llvm = use_extension("@toolchains_llvm//toolchain/extensions:llvm.bzl", "llvm")
# llvm.toolchain(llvm_version = "20.1.7")
# use_repo(llvm, "llvm_toolchain")
#
# register_toolchains("@llvm_toolchain//:all")
############################
```