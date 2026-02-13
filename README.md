This repo simply illustrates an issue I'm having with Bazel 9.0.0 and the `toolchains_llvm_bootstrapped` repo building `mimick`. This library builds correctly with `toolchains_llvm`. Install `bazelisk` and run:

```bash
git clone --recurse-submodules https://github.com/asymingt/bazel_toolchain_issue.git
cd bazel_toolchain_issue
bazel build @mimick//...
```