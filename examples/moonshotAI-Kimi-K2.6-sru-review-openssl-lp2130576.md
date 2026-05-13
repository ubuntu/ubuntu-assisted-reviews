## SRU Review Report

| | |
|---|---|
| **Package** | openssl |
| **Tag** | queue/noble/unapproved/42ff75462 |
| **Reviewer** | opencode |
| **Date** | 2026-05-13 |

---

### Summary

**NEEDS-INFO**

---

### Checks

| # | Check | Result |
|---|-------|--------|
| 1 | Bug references in changelog | PASS |
| 2 | Bugs publicly accessible | PASS |
| 3 | Bug references in source.changes | N/A |
| 4 | Minimal change | PASS |
| 5 | No unrelated changes | PASS |
| 6 | DEP-3 patch format | PASS |
| 7 | Correct versioning | PASS |
| 8 | No co-dependent SRU | PASS |
| 9 | Fix in later releases | PASS |
| 10 | Fix in devel release | PASS |
| 11 | New upstream / uscan | N/A |
| 12 | Package-specific procedure | PASS |
| 13 | NEW packages in control | PASS |
| 14 | Maintainer has ubuntu.com email | PASS |
| 15 | No translation changes | PASS |
| 16 | Correct release tasks | PASS |
| 17 | SRU template filled | NEEDS-INFO |
| 18 | Kernel GA & HWE in plan | N/A |
| 19 | Test plan covers usage | FAIL |
| 20 | Good user story in plan | FAIL |
| 21 | Phasing errors addressed | PASS |

---

### Details

- **Check 17 — SRU template filled:** The primary bug **LP: #2130576** was moved to **Incomplete** status on Noble by a reviewer on 2026-05-06, who asked the uploader to confirm how the performance improvement is being validated. Another reviewer followed up on 2026-05-08 stating they are still waiting for a reply. The template exists but the open question means it is not yet considered complete by the SRU team.

- **Check 19 — Test plan covers usage:** The test plan for **LP: #2130576** only instructs reviewers to run `nm` to check for symbol presence on arm64/ppc64el/riscv64. This verifies build behavior but does **not** cover normal usage or confirm the stated user impact (performance improvement for TLS handshakes and ECDSA/ECDHE operations).

- **Check 20 — Good user story in plan:** The test plan for **LP: #2130576** does not tell a coherent user story. It is a low-level technical check (symbol existence) rather than describing how a user or administrator would observe the improvement in real-world TLS performance.

---

### Recommendation

**NEEDS-INFO**

The uploader must reply on **LP: #2130576** to the reviewer's question about how the performance improvement is being confirmed. The test plan should be updated to include a performance regression test or benchmark (e.g., TLS handshake throughput before and after the fix on affected architectures) that demonstrates the stated user impact is actually addressed. Once the test plan is acceptable and the bug status moves out of **Incomplete**, this upload can be re-reviewed for approval.

The code changes themselves are minimal and correct: enabling `ec_nistp_64_gcc_128` on arm64/ppc64el/riscv64, fixing doc symlinks to `libssl3t64`, and adding the ppc64 regex patch with proper DEP-3 headers. The equivalent fixes are already present in Plucky, Questing, and Resolute. No other blocking issues were identified.
