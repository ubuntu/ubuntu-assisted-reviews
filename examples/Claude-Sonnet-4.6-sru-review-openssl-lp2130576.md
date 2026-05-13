=== SRU Review Report ===
Package:      openssl
Tag:          queue/noble/unapproved/c01fc7dc1
Reviewer:     ubuntu-sru
Date:         2026-05-13

--- Summary ---
NEEDS-INFO

--- Checks ---
1. Bug references in changelog:      [PASS]
2. Bugs publicly accessible:         [PASS]
3. Bug references in source.changes: [N/A]
4. Minimal change:                   [PASS]
5. No unrelated changes:             [PASS]
6. DEP-3 patch format:               [PASS]
7. Correct versioning:               [PASS]
8. No co-dependent SRU:              [PASS]
9. Fix in later releases:            [PASS]
10. Fix in devel release:            [PASS]
11. New upstream / uscan:            [N/A]
12. Package-specific procedure:      [N/A]
13. NEW packages in control:         [PASS]
14. Maintainer has ubuntu.com email: [PASS]
15. No translation changes:          [PASS]
16. Correct release tasks:           [FAIL]
17. SRU template filled:             [FAIL]
18. Kernel GA & HWE in plan:         [N/A]
19. Test plan covers usage:          [FAIL]
20. Good user story in plan:         [FAIL]
21. Phasing errors addressed:        [N/A]

--- Details ---

Check 3 — source.changes not inspected:
The .changes file is not available via git. Bug numbers in the changelog match what is
visible in Launchpad, so this is treated as N/A rather than a failure.

Check 16 — Correct release tasks: FAIL (LP: #2130576)
The Noble (and Jammy) tasks for LP: #2130576 remain in Incomplete state. For an SRU
upload to be approved, all targeted release tasks must be at least In Progress with a
complete and accepted SRU template. The uploader has not yet responded to a reviewer's
request for regression testing evidence; until the task is advanced to In Progress the
SRU template is not considered accepted for noble.

LP: #2107167 (Noble: In Progress) and LP: #2137464 (Noble: In Progress, Questing: Fix
Released) are correctly filed.

Check 17 — SRU template filled: FAIL (LP: #2130576)
A reviewer queried whether symbol-presence checking alone
("nm … | grep EC_GFp_nistp224_method") is sufficient to confirm the stated performance
impact on arm64, ppc64el, and riscv64. The uploader has not responded with regression
testing results covering actual performance or broader functional testing. Until this
information is provided and the Noble task is advanced to In Progress, the template is
not complete.

The templates for LP: #2107167 and LP: #2137464 were filled on 2026-05-06 and are
accepted.

Check 19 — Test plan covers usage: FAIL
LP: #2130576: The test plan only verifies symbol presence (nm). A reviewer has already
flagged this as insufficient. The plan should include evidence of a successful package
build on at least one of the newly-enabled architectures (arm64, ppc64el, riscv64) and
a functional test exercising the optimised code path (e.g., openssl speed or a TLS
handshake confirming the nistp symbols are actually used at runtime).

LP: #2137464: The test plan explicitly defers testing to LP: #2130576 ("better to test
this change as part of [bug #2130576]"). Since that testing is itself incomplete, this
creates a dependency that must be resolved together.

LP: #2107167: The plan only demonstrates the broken pre-fix state. It should include a
post-fix verification step confirming the symlinks resolve correctly after installing the
updated package (e.g., "readlink -f /usr/share/doc/openssl/copyright" returns a valid
path).

Check 20 — Good user story in plan: FAIL
The test plans across all three bugs do not form a coherent user story that exercises
normal openssl usage end-to-end. There is no install-and-verify scenario a user or
administrator could follow to confirm the package works correctly after applying the SRU.

Informational — symlink fix hardcodes library package name:
The upload writes "ln -sf ../libssl3t64/$$f …" directly, whereas questing and resolute
use the "$(library_package)" variable (which also resolves to libssl3t64). Functionally
equivalent for noble; noted for awareness only, not a blocking concern.

Informational — changelog.gz still in symlink loop:
The upload retains changelog.gz in the "for f in …" loop. Questing and resolute dropped
it with a comment noting that pkgbinarymangler removes the real file, breaking the
symlink. If pkgbinarymangler behaves the same way on noble builders, this could leave the
changelog.gz symlink dangling. The uploader should confirm whether this is intentional or
whether LP: #2107167 should also drop changelog.gz from the loop.

--- Recommendation ---
NEEDS-INFO

The code changes themselves are minimal and correct: enabling ec_nistp_64_gcc_128 on
arm64/ppc64el/riscv64, fixing doc symlinks to point to libssl3t64, and adding the ppc64
regex patch with proper DEP-3 headers. The equivalent fixes are present in all later
supported releases and in the devel release.

Three blocking items must be addressed before this upload can be approved:

1. LP: #2130576 — regression testing required.
   The uploader must respond to the open reviewer question and provide testing that goes
   beyond symbol-presence checking: a successful package build on an affected architecture
   and a functional test showing the optimised ECC code path is exercised (e.g., openssl
   speed nistp384 before and after, or a TLS handshake confirming the optimised
   implementation is loaded). Once provided, the Noble task must be updated to In Progress.

2. LP: #2137464 — test plan must become self-contained.
   Once item 1 is resolved, update LP: #2137464 with an explicit reference to the
   completed test results rather than an open-ended cross-reference to an incomplete bug.

3. LP: #2107167 — extend test plan to include post-fix verification.
   Add a step that installs the updated package in a noble environment and confirms
   /usr/share/doc/openssl/copyright and /usr/share/doc/libssl-dev/copyright resolve
   correctly via their symlinks. Also clarify whether changelog.gz should be dropped from
   the symlink loop as questing and resolute have done.