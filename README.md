repo for reproduce bazel rules_go bug
=====================================

Consider "vendor/" directory with https://github.com/stretchr/testify project
It has own "vendor/" directory
```
vendor/github.com/stretchr/testify/vendor
```

```
➜ bazel run :gazelle
INFO: Found 1 target...
Target //:gazelle up-to-date:
  bazel-bin/gazelle_script.bash
  bazel-bin/gazelle
INFO: Elapsed time: 0.110s, Critical Path: 0.00s

INFO: Running command line: bazel-bin/gazelle

➜ bazel build //vendor/github.com/stretchr/testify/...
ERROR: /Users/oleg/pp/bazel_vendor_inside_vendor/vendor/github.com/stretchr/testify/mock/BUILD.bazel:3:1: no such package 'vendor/github.com/stretchr/objx': BUILD file not found on package path and referenced by '//vendor/github.com/stretchr/testify/mock:go_default_library'.
ERROR: Analysis of target '//vendor/github.com/stretchr/testify/http:go_default_library' failed; build aborted: no such package 'vendor/github.com/stretchr/objx': BUILD file not found on package path.
INFO: Elapsed time: 0.107s
```

As you can see, gazelle ignores "vendor" inside "vendor/github.com/stretchr/testify"
