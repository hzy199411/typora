# AOSP master build issue 202106
* issue:
```bash
FAILED: out/target/common/obj/APPS/qcrilmsgtunnel_intermediates/enforce_uses_libraries.status
/bin/bash -c "(rm -f out/target/common/obj/APPS/qcrilmsgtunnel_intermediates/enforce_uses_libraries.status ) && (build/soong/scripts/manifest_check.py    --enforce-uses-libraries        --enforce-uses-libraries-status out/target/common/obj/APPS/qcrilmsgtunnel_intermediates/enforce_uses_libraries.status           --aapt out/host/linux-x86/bin/aapt                                      vendor/qcom/flame/proprietary/qcrilmsgtunnel.apk )"
error: mismatch in the <uses-library> tags between the build system and the manifest:
        - required libraries in build system: []
                         vs. in the manifest: [qti-telephony-hidl-wrapper, qti-telephony-utils]
        - optional libraries in build system: []
                         vs. in the manifest: []
        - tags in the manifest (vendor/qcom/flame/proprietary/qcrilmsgtunnel.apk):
                uses-library:'qti-telephony-hidl-wrapper'               uses-library:'qti-telephony-utils'
note: the following options are available:
        - to temporarily disable the check on command line, rebuild with RELAX_USES_LIBRARY_CHECK=true (this will set compiler filter "verify" and disable AOT-compilation in dexpreopt)
        - to temporarily disable the check for the whole product, set PRODUCT_BROKEN_VERIFY_USES_LIBRARIES := true in the product makefiles
        - to fix the check, make build system properties coherent with the manifest
        - see build/make/Changes.md for details

01:38:11 ninja failed with: exit status 1
```

* workaround:
```bash
$ RELAX_USES_LIBRARY_CHECK=true make
```

