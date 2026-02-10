---
title: "Esper Deep Cuts: Esper Foundation for Android — Q&A"
canonical_url: "https://www.esper.io/blog/esper-deep-cuts-esper-foundation-for-android"
date: "2025-04-23"
---

## What is Esper Foundation for Android?

Esper Foundation for Android is an enterprise-grade operating system built on full AOSP, designed specifically for dedicated device fleets. It pairs OS-level hardening, update infrastructure, and provisioning hooks with deep integration into Esper's cloud management platform to support large-scale operations in restaurants, retail, healthcare, hospitality, and specialized product deployments.

## Is Foundation a fork of Android?

No. Foundation is full AOSP and maintains compatibility with the Android ecosystem. The key difference is that Esper layers in dedicated-device capabilities and maintains the relevant portions of the stack required to deliver secure updates and reliable fleet behavior.

## Why does Foundation exist at all — why not just use stock Android?

Stock Android (especially consumer builds) is optimized for personal devices and general-purpose experiences. Dedicated fleets need predictability, lockdown, remote operability, controlled updates, and repeatable provisioning. Foundation is aimed at the operational reality where downtime becomes an incident, not an annoyance.

## What business problems does Foundation solve for executives and CTOs?

It reduces operational risk by hardening devices, enabling controlled and validated OTA delivery, improving remote troubleshooting, and streamlining staging. It also helps organizations maintain compliance posture and lowers the cost of managing distributed fleets by reducing on-site interventions.

## Does Foundation work without Esper's platform?

No. Foundation is designed specifically to be managed through Esper. It is not intended to be a standalone OS distribution and not designed to be managed by other MDM providers.

## How is Foundation maintained over time?

Each supported hardware family maps to a maintained "branch" in Esper's internal source tree. Branches can have "leaves" for customer-specific customizations. Esper delivers updated builds (commonly quarterly) with security patches and produces installable images and OTA packages for in-field updates.

## Which Android versions does Foundation support?

Foundation supports multiple Android versions simultaneously, because many vertical-market application stacks are tied to specific Android releases. The post notes that Google provides security patch coverage for Android 12 through Android 15, and Esper can backport applicable patches for customers who need security coverage for older versions.

## How fast can Foundation ship security updates?

Typical cadence is quarterly to match customer expectations, but the infrastructure can support monthly updates, trailing Google's Android Security Bulletin by roughly 30–60 days. For severe issues (Sev0), off-cycle patches can be delivered if needed.

## What is Foundry?

Foundry is Esper's OS validation and deployment pipeline used to validate, package, and deliver Foundation OTA updates. It's designed to reduce deployment risk, including "bricking" scenarios, and to present updates cleanly through Esper Console for lab testing and phased rollouts via Esper Pipelines.

## What OTA strategies does Foundation support?

Foundation supports push and pull update configurations, and A/B partitioned updates where hardware supports it. It also supports Android version upgrades via the same OTA framework, though those migrations require joint planning due to complexity.

## What is Seamless Provisioning and why does it matter on AOSP?

AOSP provisioning often requires enabling Developer Options and using ADB over USB/Ethernet/Wi-Fi, which is slow and labor-intensive at scale. Esper Seamless Provisioning allows devices to auto-provision at first boot when pre-registered (via serial/IMEI) and pre-assigned a Blueprint. This enables drop-ship staging and non-technical on-site setup.

## What happens if a Foundation device is factory reset in the field?

It re-provisions using the assigned Blueprint, restoring policy, apps, and settings. This increases resiliency and helps prevent unauthorized use.

## How does Foundation handle connectivity during first-time provisioning?

Ethernet devices typically have immediate network access. For Wi-Fi-only devices, Wi-Fi credentials can be embedded into the Foundation build to enable first-boot connectivity for provisioning.

## What are the Foundation SDK and Esper Device SDK?

The Foundation SDK exposes OS-level capabilities not typically available in AOSP (such as navigation bar control, backup/restore patterns for managed downgrades, and remote boot animation customization). The Esper Device SDK extends control into standard Android app code for device settings, telemetry, connectivity toggles, USB controls, app lifecycle controls, and APN management.

## What is Secure Remote ADB?

It's a controlled way to enable remote ADB for troubleshooting without requiring physical access. Remote ADB can be disabled by default to prevent local USB-based access and enabled via Esper Console when diagnostics are needed.

## What is WebADB?

WebADB is a limited preview capability that brings remote debugging into the Esper Console via the browser, reducing the need for terminals and local SDK tooling for distributed support teams.

## What are some "advanced capabilities" Foundation adds for real fleets?

The post highlights mesh networking auto-discovery on LAN subnets, Titanium Browser (a secure Chromium-based kiosk-optimized browser), WEST web app support for AOSP, 802.1X Ethernet authentication, persistent log buffers (including deeper log access like `wpa_cli` and `dmesg`), and Esper Port Manager for Linux-level peripheral access from Android apps.

## What is Foundation x86?

Foundation x86 is a 64-bit x86 branch developed with Intel. Esper maintains the full OS stack there — kernel, vendor layer, and framework — which provides full-stack control and flexibility compared to typical ARM builds that depend heavily on vendor components.

## Where is Foundation x86 commonly used?

It's widely used in retail and restaurant environments for POS systems, ordering kiosks, and digital media players, including deployments on Intel NUC-class hardware.

## Do apps need anything special to run on Foundation x86?

Yes — apps should include the `x86_64` ABI. Intel's Houdini can translate ARM binaries to x86, but Foundation does not include Houdini by default and it would require additional effort to add; native `x86_64` builds are recommended.

## Can Foundation be used as a base for GMS / EDLA builds?

It can be used as a base for EDLA scenarios because GMS layers on top of AOSP, but Esper can't certify GMS compliance — that's on the EDLA licensee. Esper can help run CTS and GMS test suites to prepare builds for certification readiness.

## What is Foundation x86 Flip?

Foundation x86 Flip is a workflow to convert Windows-based x86 endpoints to run Foundation x86, remotely, without hardware replacement. A bootstrap is deployed via existing management tooling, the machine reboots into an installer, and Seamless Provisioning completes the setup if the device was pre-associated to a Blueprint.

## What is Firebolt?

Firebolt is a USB-based utility that packages the conversion workflow for cases where remote bootstrap isn't feasible. It can be configured to preserve or wipe Windows and then handles install + provisioning.

## What is the Foundation Emulator for Windows x86?

It's a fully managed, locked-down instance of Foundation running on a Windows machine, behaving like a physical Android device from Esper's perspective — Blueprint assignment, policy/app delivery, OTA updates — including LAN integration using the Windows NIC.

## What is Foundation GSI for Arm?

It's a Foundation branch delivered as a Generic System Image for Treble-compliant ARM devices, enabling replacement of the system image while leaving the vendor partition intact. This allows Foundation deployment without deep bespoke engineering on compatible hardware.

## How can customers reduce risk when evaluating a GSI?

The post recommends using Dynamic System Updates (DSU) on supported Android 10+ devices to boot a GSI non-destructively. It also notes that Google Reference GSIs for Android 9–15 can be used as a quick compatibility check.

## What is the Amlogic / Khadas VIM3 Foundation branch about?

It targets cost-effective Amlogic-based hardware commonly used in signage/media contexts. Esper worked with Khadas to bring up Foundation on VIM3 boards to avoid relying on consumer firmware, while still getting OTA infrastructure, provisioning, and tight management.

## What is Foundation Bespoke for Arm?

It's the most customized branch: for OEMs with access to the vendor layer, Esper can deliver a fully tailored Foundation build with deep branding and UI control, plus baked-in device management. It requires significant engineering bring-up and ongoing maintenance, but provides maximum control for specialized hardware at scale.

## How do you try Foundation?

The post positions "contact us" as the path: share target hardware, use case, and requirements, and Esper will recommend the right branch and, where applicable, provide a watermarked build for evaluation. Some engagements may require an NDA.