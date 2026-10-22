# LinuxWays Security Suite v2.7.0

**Deterministic Mobile Endpoint & Enterprise Assurance Platform for Android**

Submitted to the **PCC-26 Cyber Innovation & Startup Challenge** (NCCS, Air University, Islamabad)

![Platform](https://img.shields.io/badge/platform-Android%20(API%2036)-3DDC84)
![Status](https://img.shields.io/badge/stage-Live%20MVP-12b5a0)
![Engine](https://img.shields.io/badge/engine-deterministic%20(no%20AI)-0b1f33)
![License](https://img.shields.io/badge/license-All%20Rights%20Reserved-lightgrey)

---

## Overview

LinuxWays Security Suite is a 100% deterministic, on-device Android security auditor. It checks **12 OS hardening controls**, **100% of installed application packages** and **active network interfaces**, then calculates a reproducible **0–100 Security Score** directly on the handset.

Unlike cloud-dependent Mobile Threat Defense and antivirus tools that rely on opaque heuristics, LinuxWays gives repeatable, auditable evidence: the same device state always produces the same score and the same remediation trace. There is no AI or ML model in the decision path, no root requirement and no cloud data exfiltration.

## The Problem

- Enterprises run sensitive financial and administrative workflows on Android devices but cannot prove the devices enforce core hardening (SELinux, verified boot, encryption, clean package signing, secure network transport).
- Existing tools depend on cloud heuristics that drain battery, raise privacy concerns, create false-positive fatigue and do not verify OS hardening.
- Without verifiable device posture, Zero-Trust access decisions and compliance audits (CIS, NIST, ISO 27001) rest on assumptions.

## Key Features

| Area | What it does |
|---|---|
| **OS Controls Auditor** | 12-point check: SELinux, verified boot and bootloader lock, encryption, developer options, ADB/USB debugging, unknown-source installs, root integrity, screen lock, accessibility abuse, device admins, user CA store, security patch level |
| **Package & APK Auditor** | Enumerates 100% of installed apps; verifies V2/V3/V4 signatures, target SDK, dangerous permissions, exported components and installer provenance |
| **Network Inspector** | VPN tunnel, Private DNS (DoT/DoH), Wi-Fi cipher strength, proxy configuration and cleartext traffic flags |
| **Dual scan modes** | Standard Scan (under 2 s) and Deep Scan (under 8 s) |
| **Five workspaces** | Scanner, Apps, 12 Checks, Network, Device, with drill-down from score to package evidence |
| **Enterprise export** | Signed JSON / STIX 2.1 attestation payloads for MDM/UEM, SIEM and Zero-Trust (ZTNA) gates |

## Scoring Model

```
Security Score = S_OS (max 48) + S_Apps (max 32) + S_Network (max 20) − Σ P_Critical
```

| Score | Status |
|---|---|
| 90–100 | **Protected** (green) |
| 70–89 | **Review Needed** (amber) |
| below 70 | **Critical Action Required** (red) |

## Architecture

Five-layer modular design, with strongly typed immutable state snapshots between layers:

1. **Android OS Kernel, HAL & Framework interfaces:** PackageManager, DevicePolicyManager, Settings, Keystore, ConnectivityManager, sysfs/procfs
2. **Three-stage audit engines:** OS Controls, Package & APK, Network
3. **Deterministic scoring and policy core:** mode dispatcher, scoring engine, posture classifier
4. **Reactive five-workspace console:** the Android UI
5. **Enterprise governance and SIEM bus:** signed attestations, compliance mapper, policy webhook, fleet telemetry API

## Validation Results

Tested on reference device **RMX3933, Android API 36**:

| Metric | Baseline (State A) | Hardened (State B) |
|---|---|---|
| Security Score | 80 (Review Needed) | **97 (Protected)** |
| OS controls passed | 10 / 12 (2 warnings) | 11 / 12 (0 critical) |
| Apps audited | 75 / 75 | 65 / 65 |

## Performance Targets

- Standard Scan under 2 seconds; Deep Scan under 8 seconds
- Peak memory under 45 MB RAM
- No idle background battery drain
- 100% on-device evaluation; only signed posture attestations are exported

## Standards Alignment

CIS Google Android Benchmark · NIST SP 800-163 Rev. 1 · ISO/IEC 27001:2022

## Demo

Download the demo APK: [LinuxWays Security Suite APK](https://drive.google.com/file/d/1nxVZu5aujj99-pJ5peLo6TG2PkfxC37K/view?usp=drivesdk)

> Install by enabling installation from your browser or file manager when prompted. Android may show an "unknown source" warning for apps installed outside the Play Store.

## Getting Started

> **[Team to complete]** Fill in the details below from your project setup.

**Requirements**
- Android Studio: `[version]`
- Language / build system: `[e.g. Kotlin, Gradle]`
- minSdk / targetSdk: `[minSdk]` / `36`

**Build and run**
```bash
git clone https://github.com/<your-username>/linuxways-security-suite.git
cd linuxways-security-suite
# Open in Android Studio, sync Gradle, then Run on a device or emulator
```

## Repository Structure

> **[Team to complete]** Example layout:

```
linuxways-security-suite/
├── app/            # Android application source
├── docs/           # Technical proposal, pitch deck
├── screenshots/    # State A (score 80) and State B (score 97)
└── README.md
```

## Documentation

- Technical Architecture & Enterprise Business Proposal (see `docs/`)

## Team

| Name | Role |
|---|---|
| **Atif Ahmed** | Platform Architect (Cybersecurity & Systems Architecture) |
| **Ms. Hirra Anwar** | Assistant Professor, SEECS: Cybersecurity Research Advisory, Compliance Verification & Security Governance |
| **Muhammad Haris** | Android OS Controls Auditor (12 Checks) & Deterministic APK Inspection Engine |
| **Muhammad Majid** | Network Security Inspector, 5-Workspace Console & Device Telemetry Validation |

School of Electrical Engineering and Computer Science (SEECS), NUST, Islamabad

## License

Copyright © 2026 LinuxWays Security Suite Team. **All rights reserved.**
This repository is shared for evaluation purposes in the PCC-26 Cyber Innovation & Startup Challenge. No permission is granted to copy, modify, distribute or use the code without written consent from the authors.
