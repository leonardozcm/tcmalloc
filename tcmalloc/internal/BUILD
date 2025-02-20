# Copyright 2019 The TCMalloc Authors
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#     https://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.
#
# Internal libraries used for the implementation and testing of TCMalloc.

load("//tcmalloc:copts.bzl", "TCMALLOC_DEFAULT_COPTS")
load("//tcmalloc:variants.bzl", "create_tcmalloc_benchmark")

package(default_visibility = ["//visibility:private"])

licenses(["notice"])  # Apache 2.0

cc_library(
    name = "atomic_danger",
    hdrs = ["atomic_danger.h"],
    copts = TCMALLOC_DEFAULT_COPTS,
    visibility = ["//visibility:private"],
    deps = [":config"],
)

cc_library(
    name = "atomic_stats_counter",
    hdrs = ["atomic_stats_counter.h"],
    copts = TCMALLOC_DEFAULT_COPTS,
    visibility = [
        "//tcmalloc:__subpackages__",
    ],
    deps = [
        ":config",
        "@com_google_absl//absl/base:core_headers",
    ],
)

cc_library(
    name = "clock",
    hdrs = ["clock.h"],
    copts = TCMALLOC_DEFAULT_COPTS,
    visibility = [
        "//tcmalloc:__subpackages__",
    ],
    deps = [
        ":config",
        "@com_google_absl//absl/base",
        "@com_google_absl//absl/functional:function_ref",
        "@com_google_absl//absl/time",
    ],
)

cc_library(
    name = "config",
    hdrs = ["config.h"],
    copts = TCMALLOC_DEFAULT_COPTS,
    visibility = ["//tcmalloc:__subpackages__"],
    deps = [
        "@com_google_absl//absl/base:config",
    ],
)

cc_library(
    name = "declarations",
    hdrs = ["declarations.h"],
    visibility = [
        "//tcmalloc:__subpackages__",
    ],
)

cc_library(
    name = "environment",
    srcs = ["environment.cc"],
    hdrs = ["environment.h"],
    copts = TCMALLOC_DEFAULT_COPTS,
    visibility = [
        "//tcmalloc:__subpackages__",
    ],
    deps = [":config"],
)

cc_test(
    name = "environment_test",
    srcs = ["environment_test.cc"],
    copts = TCMALLOC_DEFAULT_COPTS,
    deps = [
        ":environment",
        "@com_github_google_benchmark//:benchmark",
        "@com_google_googletest//:gtest_main",
    ],
)

cc_library(
    name = "lifetime_predictions",
    hdrs = ["lifetime_predictions.h"],
    copts = TCMALLOC_DEFAULT_COPTS,
    visibility = [
        "//tcmalloc:__subpackages__",
    ],
    deps = [
        ":linked_list",
        "@com_google_absl//absl/algorithm:container",
        "@com_google_absl//absl/base",
        "@com_google_absl//absl/base:core_headers",
        "@com_google_absl//absl/base:malloc_internal",
        "@com_google_absl//absl/debugging:stacktrace",
        "@com_google_absl//absl/hash",
        "@com_google_absl//absl/time",
    ],
)

cc_test(
    name = "lifetime_predictions_test",
    srcs = ["lifetime_predictions_test.cc"],
    copts = TCMALLOC_DEFAULT_COPTS,
    deps = [
        ":lifetime_predictions",
        ":logging",
        "//tcmalloc/testing:testutil",
        "@com_github_google_benchmark//:benchmark",
        "@com_google_absl//absl/base:core_headers",
        "@com_google_absl//absl/flags:flag",
        "@com_google_googletest//:gtest_main",
    ],
)

cc_library(
    name = "lifetime_tracker",
    hdrs = ["lifetime_tracker.h"],
    visibility = [
        "//tcmalloc:__subpackages__",
    ],
    deps = [
        ":clock",
        ":lifetime_predictions",
        ":linked_list",
        "@com_google_absl//absl/algorithm:container",
        "@com_google_absl//absl/base",
        "@com_google_absl//absl/base:core_headers",
        "@com_google_absl//absl/base:malloc_internal",
        "@com_google_absl//absl/debugging:stacktrace",
        "@com_google_absl//absl/hash",
        "@com_google_absl//absl/memory",
        "@com_google_absl//absl/time",
    ],
)

cc_test(
    name = "lifetime_tracker_test",
    srcs = ["lifetime_tracker_test.cc"],
    copts = TCMALLOC_DEFAULT_COPTS,
    deps = [
        ":lifetime_predictions",
        ":lifetime_tracker",
        ":logging",
        "@com_github_google_benchmark//:benchmark",
        "@com_google_absl//absl/base:core_headers",
        "@com_google_absl//absl/flags:flag",
        "@com_google_absl//absl/time",
        "@com_google_googletest//:gtest_main",
    ],
)

cc_library(
    name = "linked_list",
    hdrs = ["linked_list.h"],
    copts = TCMALLOC_DEFAULT_COPTS,
    visibility = [
        "//tcmalloc:__subpackages__",
    ],
    deps = [
        ":logging",
        "@com_google_absl//absl/base:core_headers",
    ],
)

create_tcmalloc_benchmark(
    name = "linked_list_benchmark",
    srcs = ["linked_list_benchmark.cc"],
    copts = TCMALLOC_DEFAULT_COPTS,
    malloc = "//tcmalloc",
    deps = [
        ":linked_list",
        ":logging",
        ":mock_span",
        "@com_github_google_benchmark//:benchmark",
        "@com_google_absl//absl/random",
    ],
)

cc_test(
    name = "linked_list_test",
    size = "small",
    srcs = ["linked_list_test.cc"],
    copts = TCMALLOC_DEFAULT_COPTS,
    linkstatic = 1,
    deps = [
        ":linked_list",
        ":mock_span",
        "@com_github_google_benchmark//:benchmark",
        "@com_google_absl//absl/container:flat_hash_set",
        "@com_google_absl//absl/container:node_hash_set",
        "@com_google_absl//absl/random",
        "@com_google_googletest//:gtest_main",
    ],
)

cc_library(
    name = "linux_syscall_support",
    hdrs = ["linux_syscall_support.h"],
    copts = TCMALLOC_DEFAULT_COPTS,
)

cc_library(
    name = "logging",
    srcs = ["logging.cc"],
    hdrs = ["logging.h"],
    copts = TCMALLOC_DEFAULT_COPTS,
    visibility = [
        "//tcmalloc:__pkg__",
        "//tcmalloc:__subpackages__",
    ],
    deps = [
        ":config",
        ":parameter_accessors",
        "//tcmalloc:malloc_extension",
        "@com_google_absl//absl/base",
        "@com_google_absl//absl/base:core_headers",
        "@com_google_absl//absl/debugging:stacktrace",
        "@com_google_absl//absl/strings",
        "@com_google_absl//absl/strings:str_format",
    ],
)

cc_test(
    name = "logging_test",
    srcs = ["logging_test.cc"],
    copts = TCMALLOC_DEFAULT_COPTS,
    data = [
    ],
    deps = [
        ":logging",
        "@com_github_google_benchmark//:benchmark",
        "@com_google_absl//absl/base:core_headers",
        "@com_google_absl//absl/flags:flag",
        "@com_google_googletest//:gtest_main",
    ],
)

cc_binary(
    name = "logging_test_helper",
    testonly = 1,
    srcs = ["logging_test_helper.cc"],
    copts = TCMALLOC_DEFAULT_COPTS,
    malloc = "//tcmalloc",
)

cc_library(
    name = "memory_stats",
    srcs = ["memory_stats.cc"],
    hdrs = ["memory_stats.h"],
    copts = TCMALLOC_DEFAULT_COPTS,
    visibility = [
        "//tcmalloc:__subpackages__",
    ],
    deps = [
        ":config",
        ":logging",
        ":util",
        "@com_google_absl//absl/strings",
    ],
)

cc_test(
    name = "memory_stats_test",
    srcs = ["memory_stats_test.cc"],
    copts = TCMALLOC_DEFAULT_COPTS,
    deps = [
        ":memory_stats",
        "@com_github_google_benchmark//:benchmark",
        "@com_google_absl//absl/base:core_headers",
        "@com_google_googletest//:gtest_main",
    ],
)

cc_library(
    name = "mincore",
    srcs = ["mincore.cc"],
    hdrs = ["mincore.h"],
    copts = TCMALLOC_DEFAULT_COPTS,
    linkstatic = 1,
    visibility = ["//tcmalloc:__subpackages__"],
    deps = [":config"],
)

create_tcmalloc_benchmark(
    name = "mincore_benchmark",
    srcs = ["mincore_benchmark.cc"],
    copts = TCMALLOC_DEFAULT_COPTS,
    deps = [
        ":logging",
        ":mincore",
        "@com_github_google_benchmark//:benchmark",
        "@com_google_absl//absl/memory",
    ],
)

cc_test(
    name = "mincore_test",
    srcs = ["mincore_test.cc"],
    copts = TCMALLOC_DEFAULT_COPTS,
    linkstatic = 1,
    deps = [
        ":logging",
        ":mincore",
        "@com_github_google_benchmark//:benchmark",
        "@com_google_googletest//:gtest_main",
    ],
)

cc_library(
    name = "mock_span",
    testonly = 1,
    hdrs = ["mock_span.h"],
    copts = TCMALLOC_DEFAULT_COPTS,
    deps = [
        ":linked_list",
    ],
)

cc_library(
    name = "cache_topology",
    srcs = ["cache_topology.cc"],
    hdrs = ["cache_topology.h"],
    copts = TCMALLOC_DEFAULT_COPTS,
    visibility = [
        "//tcmalloc:__subpackages__",
    ],
    deps = [
        ":config",
        ":logging",
        ":util",
        "@com_google_absl//absl/base",
        "@com_google_absl//absl/base:core_headers",
        "@com_google_absl//absl/functional:function_ref",
        "@com_google_absl//absl/strings",
    ],
)

cc_test(
    name = "cache_topology_test",
    srcs = ["cache_topology_test.cc"],
    copts = TCMALLOC_DEFAULT_COPTS,
    linkstatic = 1,
    deps = [
        ":cache_topology",
        "@com_github_google_benchmark//:benchmark",
        "@com_google_absl//absl/random",
        "@com_google_absl//absl/types:span",
        "@com_google_googletest//:gtest_main",
    ],
)

cc_library(
    name = "numa",
    srcs = ["numa.cc"],
    hdrs = ["numa.h"],
    copts = TCMALLOC_DEFAULT_COPTS,
    visibility = [
        "//tcmalloc:__subpackages__",
    ],
    deps = [
        ":config",
        ":environment",
        ":logging",
        ":percpu",
        ":util",
        "@com_google_absl//absl/base",
        "@com_google_absl//absl/base:core_headers",
        "@com_google_absl//absl/functional:function_ref",
        "@com_google_absl//absl/strings",
    ],
)

cc_test(
    name = "numa_test",
    srcs = ["numa_test.cc"],
    copts = TCMALLOC_DEFAULT_COPTS,
    linkstatic = 1,
    deps = [
        ":logging",
        ":numa",
        "//tcmalloc:want_numa_aware",
        "@com_github_google_benchmark//:benchmark",
        "@com_google_absl//absl/random",
        "@com_google_absl//absl/strings",
        "@com_google_absl//absl/types:span",
        "@com_google_googletest//:gtest_main",
    ],
)

cc_library(
    name = "optimization",
    hdrs = ["optimization.h"],
    copts = TCMALLOC_DEFAULT_COPTS,
    visibility = [
        "//tcmalloc:__subpackages__",
    ],
    deps = [
        ":logging",
    ],
)

cc_library(
    name = "parameter_accessors",
    hdrs = ["parameter_accessors.h"],
    copts = TCMALLOC_DEFAULT_COPTS,
    visibility = ["//tcmalloc:__subpackages__"],
    deps = [
        "@com_google_absl//absl/base:core_headers",
        "@com_google_absl//absl/time",
    ],
)

cc_library(
    name = "percpu",
    srcs = [
        "percpu.cc",
        "percpu_rseq_asm.S",
        "percpu_rseq_unsupported.cc",
    ],
    hdrs = ["percpu.h"],
    copts = TCMALLOC_DEFAULT_COPTS,
    textual_hdrs = [
        "percpu_rseq_aarch64.S",
        "percpu_rseq_ppc.S",
        "percpu_rseq_x86_64.S",
    ],
    visibility = [
        "//tcmalloc:__subpackages__",
    ],
    deps = [
        ":atomic_danger",
        ":config",
        ":linux_syscall_support",
        ":logging",
        ":optimization",
        ":util",
        "@com_google_absl//absl/base",
        "@com_google_absl//absl/base:core_headers",
        "@com_google_absl//absl/base:dynamic_annotations",
    ],
)

cc_library(
    name = "percpu_tcmalloc",
    hdrs = ["percpu_tcmalloc.h"],
    copts = TCMALLOC_DEFAULT_COPTS,
    visibility = [
        "//tcmalloc:__subpackages__",
    ],
    deps = [
        ":mincore",
        ":percpu",
        "@com_google_absl//absl/base",
        "@com_google_absl//absl/base:dynamic_annotations",
    ],
)

cc_test(
    name = "percpu_tcmalloc_test",
    timeout = "long",
    srcs = ["percpu_tcmalloc_test.cc"],
    copts = TCMALLOC_DEFAULT_COPTS,
    linkstatic = 1,
    malloc = "//tcmalloc:tcmalloc_deprecated_perthread",
    deps = [
        ":config",
        ":logging",
        ":percpu_tcmalloc",
        ":util",
        "//tcmalloc:malloc_extension",
        "//tcmalloc/testing:testutil",
        "@com_github_google_benchmark//:benchmark",
        "@com_google_absl//absl/base",
        "@com_google_absl//absl/container:fixed_array",
        "@com_google_absl//absl/container:flat_hash_set",
        "@com_google_absl//absl/debugging:symbolize",
        "@com_google_absl//absl/random",
        "@com_google_absl//absl/random:seed_sequences",
        "@com_google_absl//absl/strings",
        "@com_google_absl//absl/synchronization",
        "@com_google_absl//absl/time",
        "@com_google_absl//absl/types:span",
        "@com_google_googletest//:gtest_main",
    ],
)

cc_library(
    name = "proc_maps",
    srcs = ["proc_maps.cc"],
    hdrs = ["proc_maps.h"],
    copts = TCMALLOC_DEFAULT_COPTS,
    visibility = [
        "//tcmalloc:__subpackages__",
    ],
    deps = [
        ":config",
        ":logging",
        ":util",
        "@com_google_absl//absl/base:core_headers",
        "@com_google_absl//absl/strings:str_format",
    ],
)

cc_library(
    name = "range_tracker",
    hdrs = ["range_tracker.h"],
    copts = TCMALLOC_DEFAULT_COPTS,
    visibility = [
        "//tcmalloc:__subpackages__",
    ],
    deps = [
        ":logging",
        ":optimization",
        "@com_google_absl//absl/numeric:bits",
    ],
)

create_tcmalloc_benchmark(
    name = "range_tracker_benchmark",
    srcs = ["range_tracker_benchmark.cc"],
    copts = TCMALLOC_DEFAULT_COPTS,
    malloc = "//tcmalloc",
    deps = [
        ":range_tracker",
        "@com_github_google_benchmark//:benchmark",
        "@com_google_absl//absl/base:core_headers",
        "@com_google_absl//absl/container:fixed_array",
        "@com_google_absl//absl/random",
        "@com_google_absl//absl/random:distributions",
    ],
)

cc_test(
    name = "range_tracker_test",
    srcs = ["range_tracker_test.cc"],
    copts = TCMALLOC_DEFAULT_COPTS,
    linkstatic = 1,
    deps = [
        ":range_tracker",
        "@com_github_google_benchmark//:benchmark",
        "@com_google_absl//absl/base:core_headers",
        "@com_google_absl//absl/container:fixed_array",
        "@com_google_absl//absl/random",
        "@com_google_absl//absl/random:distributions",
        "@com_google_googletest//:gtest_main",
    ],
)

# An empty rule to force libc malloc instead of TCMalloc.
cc_library(
    name = "system_malloc",
    copts = TCMALLOC_DEFAULT_COPTS,
    linkstatic = 1,
    visibility = [
        "//tcmalloc:__subpackages__",
    ],
)

cc_library(
    name = "timeseries_tracker",
    hdrs = ["timeseries_tracker.h"],
    copts = TCMALLOC_DEFAULT_COPTS,
    visibility = [
        "//tcmalloc:__subpackages__",
    ],
    deps = [
        ":clock",
        ":logging",
        "@com_google_absl//absl/base",
        "@com_google_absl//absl/functional:function_ref",
        "@com_google_absl//absl/numeric:bits",
        "@com_google_absl//absl/numeric:int128",
        "@com_google_absl//absl/time",
    ],
)

cc_test(
    name = "timeseries_tracker_test",
    srcs = ["timeseries_tracker_test.cc"],
    copts = TCMALLOC_DEFAULT_COPTS,
    deps = [
        ":timeseries_tracker",
        "@com_github_google_benchmark//:benchmark",
        "@com_google_googletest//:gtest_main",
    ],
)

cc_library(
    name = "util",
    srcs = ["util.cc"],
    hdrs = ["util.h"],
    copts = TCMALLOC_DEFAULT_COPTS,
    visibility = [
        "//tcmalloc:__subpackages__",
    ],
    deps = [
        ":config",
        ":logging",
        "@com_google_absl//absl/base",
        "@com_google_absl//absl/base:core_headers",
        "@com_google_absl//absl/time",
        "@com_google_absl//absl/types:span",
    ],
)
