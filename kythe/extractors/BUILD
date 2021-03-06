package(default_visibility = ["//visibility:public"])

load(":extractors.bzl", "extractor_action")

# Clone of default Java proto toolchain with "annotate_code" enabled for
# cross-language metadata file generation.
#
# --proto_toolchain_for_java=@io_kythe//kythe/extractors:java_proto_toolchain
proto_lang_toolchain(
    name = "java_proto_toolchain",
    command_line = "--java_out=annotate_code:$(OUT)",
    runtime = "@com_google_protobuf//:protobuf_java",
)

extractor_action(
    name = "extract_kzip_cxx",
    args = [
        "$(EXTRA_ACTION_FILE)",
        "$(output $(ACTION_ID).cxx.kzip)",
        "$(location //external:vnames_config)",
    ],
    data = ["//external:vnames_config"],
    extractor = "@io_kythe//kythe/cxx/extractor:cxx_extractor_bazel",
    mnemonics = ["CppCompile"],
    output = "$(ACTION_ID).cxx.kzip",
)

extractor_action(
    name = "extract_kzip_java",
    args = [
        "$(EXTRA_ACTION_FILE)",
        "$(output $(ACTION_ID).java.kzip)",
        "$(location //external:vnames_config)",
    ],
    data = ["//external:vnames_config"],
    extractor = "@io_kythe//kythe/java/com/google/devtools/kythe/extractors/java/bazel:java_extractor",
    mnemonics = ["Javac"],
    output = "$(ACTION_ID).java.kzip",
)

extractor_action(
    name = "extract_kzip_go",
    args = [
        "-corpus kythe.io",
        "$(EXTRA_ACTION_FILE)",
        "$(output $(ACTION_ID).go.kzip)",
        "$(location //external:vnames_config)",
    ],
    data = ["//external:vnames_config"],
    extractor = "@io_kythe//kythe/go/extractors/cmd/bazel:bazel_go_extractor",
    mnemonics = ["GoCompile"],
    output = "$(ACTION_ID).go.kzip",
)

extractor_action(
    name = "extract_kzip_jvm",
    args = [
        "$(EXTRA_ACTION_FILE)",
        "$(output $(ACTION_ID).jvm.kzip)",
        "$(location //external:vnames_config)",
    ],
    data = ["//external:vnames_config"],
    extractor = "@io_kythe//kythe/java/com/google/devtools/kythe/extractors/jvm/bazel:bazel_jvm_extractor",
    mnemonics = ["JavaIjar"],
    output = "$(ACTION_ID).jvm.kzip",
)

extractor_action(
    name = "extract_kzip_objc",
    args = [
        "$(EXTRA_ACTION_FILE)",
        "$(output $(ACTION_ID).objc.kzip)",
        "$(location //external:vnames_config)",
        "$(location //third_party/bazel:get_devdir)",
        "$(location //third_party/bazel:get_sdkroot)",
    ],
    data = [
        "//external:vnames_config",
        "//third_party/bazel:get_devdir",
        "//third_party/bazel:get_sdkroot",
    ],
    extractor = "@io_kythe//kythe/cxx/extractor:objc_extractor_bazel",
    mnemonics = ["ObjcCompile"],
    output = "$(ACTION_ID).objc.kzip",
)

extractor_action(
    name = "extract_typescript_kzip",
    args = [
        "--extra_action=$(EXTRA_ACTION_FILE)",
        "--include='\\.(js|json|tsx?|d\\.ts)$$'",
        "--language=typescript",
        "--output=$(output $(ACTION_ID).typescript.kzip)",
        "--rules=$(location //external:vnames_config)",
        "--scoped=true",
        "--source='\\.ts$$'",
    ],
    data = ["//external:vnames_config"],
    extractor = "@io_kythe//kythe/go/extractors/cmd/bazel:extract_kzip",
    mnemonics = ["TypeScriptCompile"],
    output = "$(ACTION_ID).typescript.kzip",
)

extractor_action(
    name = "extract_kzip_protobuf",
    args = [
        "--extra_action=$(EXTRA_ACTION_FILE)",
        "--language=protobuf",
        "--rules=$(location //external:vnames_config)",
        "--output=$(output $(ACTION_ID).protobuf.kzip)",
    ],
    data = ["//external:vnames_config"],
    extractor = "@io_kythe_lang_proto//kythe/go/extractors/proto:extract_proto_kzip",
    mnemonics = ["GenProtoDescriptorSet"],
    output = "$(ACTION_ID).protobuf.kzip",
)
