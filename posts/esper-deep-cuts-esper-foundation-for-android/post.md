---
title: "Esper Deep Cuts: Esper Foundation for Android"
author: "Keith Szot"
date: "2025-04-23"
canonical_url: "https://www.esper.io/blog/esper-deep-cuts-esper-foundation-for-android"
---

In today's rapidly evolving landscape of enterprise and advanced consumer electronics, the reliability, security, and flexibility of dedicated Android devices are more critical than ever. Businesses across sectors — restaurants, retail, healthcare, hospitality, and custom product development — depend on these devices to perform without fail.

Esper Foundation for Android is an enterprise-grade operating system built specifically for these scenarios. It ensures seamless operation, robust security, powerful remote management, and streamlined scalability. Whether powering retail POS systems, digital signage, correctional facility tablets, or consumer fitness devices, Foundation is already in action, delivering consistent results.

## Why Foundation Matters

Executives and CTOs in these industries understand the risks associated with operational disruptions. Device downtime, exploitable vulnerabilities, and inefficient management practices lead to dissatisfied customers, regulatory exposure, and increased operational costs. Foundation addresses these challenges through a tightly integrated set of features:

**Enhanced Security:** Foundation includes secure boot, verified over-the-air (OTA) updates with the latest security patches, and comprehensive lockdown capabilities. These features work together to ensure device integrity, protect against unauthorized access, and mitigate risks from vulnerabilities — both known and emerging.

**Advanced Remote Management:** Built to integrate seamlessly with Esper's cloud-based management platform, Foundation enables full remote control of thousands of devices from a central console. This reduces the need for on-site interventions, minimizing downtime — especially vital for enterprises with multiple retail or restaurant locations. It's important to note that Foundation is designed specifically for Esper and must be managed through our platform. It is not intended for standalone use or for use with other MDM providers.

**Flexible Customization:** Foundation gives businesses the ability to tailor device behavior and workflows to their exact needs. Whether configuring a restaurant ordering system, retail kiosk, healthcare endpoint, or consumer product, Foundation makes it possible to deliver consistent, engaging, and brand-specific experiences.

**Efficient Staging and Deployment Maintenance:** With Esper Seamless Provisioning built directly into the OS, Foundation simplifies the staging process while reducing both time and cost. Once deployed, devices are self-healing. Foundation uses Foundry — a scalable OS validation and deployment pipeline tailored for enterprise — to securely deliver OS updates. This process de-risks critical deployments by preventing bricking scenarios and maintaining uninterrupted service. This is especially important for customers in healthcare and hospitality, where uptime and compliance are non-negotiable.

**Simplified Compliance:** Foundation helps reduce the administrative burden of maintaining regulatory compliance with standards like HIPAA and PCI-DSS. By design, Foundation simplifies device management workflows, reducing the risk of non-compliance and making audit processes more straightforward.

**True Android, with More:** Foundation is not a fork of Android. It is full AOSP, enhanced with features specific to dedicated device deployments. These enhancements exist alongside the standard Android API set and provide additional capabilities that extend Android's usefulness in mission-critical environments.

With the baseline established, let's dig deeper into what makes Foundation technically unique and operationally powerful.

## The Foundation of Foundation

Foundation is built on full AOSP — it is not a fork, and it maintains complete compatibility with the Android ecosystem. However, Foundation must be built specifically for the silicon and hardware platform it will run on. Each supported device family corresponds to a "branch" of our internal source code tree, and these branches may contain "leaves" — customizations specific to customer use cases.

Each of these branches and leaves is actively maintained. Every quarter, we deliver updated base builds with security patches and create standalone installable images and OTA packages for in-field updates.

Because Foundation serves vertical markets where Android version requirements are tightly coupled to supported application stacks, we support multiple Android versions simultaneously. Today, Google provides security patch coverage for Android 12 through Android 15, so our team provides backporting services for customers requiring ongoing security updates for older Android versions. This means that even if a version falls outside of Google's standard patch window, our engineers can apply applicable patches to keep your devices secure.

To visualize Foundation's architecture, consider Android as a layer cake:

- The Linux kernel forms the base  
- The vendor layer (typically maintained by the silicon vendor or OEM) sits above that  
- The Android Framework is the top layer — this is where Esper adds value  

While the kernel is largely community-maintained, and the vendor layer is developed by the hardware provider, Esper fully maintains the Android Framework on Foundation builds. In select cases — particularly for Foundation x86 — we also manage the kernel and vendor layers, which allows us to fully support and deliver OTA updates for the entire stack. In these scenarios, we coordinate closely with silicon vendors and OEMs to ensure compatibility and stability.

While we typically deliver security updates quarterly (aligned with customer expectations), our infrastructure is capable of monthly updates, trailing Google's Android Security Bulletin by 30–60 days. For high-severity vulnerabilities (Sev0), we can deliver off-cycle patches as needed, though this hasn't yet been required.

Foundation's OTA infrastructure is deeply integrated with Esper's DevOps pipeline. Through our Foundry system, we ensure each OTA is validated, packaged, and presented cleanly via the Esper Console. This enables customers to easily test updates in a lab environment and then use Esper Pipelines to orchestrate a phased rollout across fleets with fine-grained control.

Foundation supports both push and pull OTA configurations, allowing for different update strategies depending on your operational needs. Pull-based updates can be particularly useful for consumer electronics deployments. We also support A/B partitioned updates — if the hardware allows for it — to ensure continuity of service during OS updates.

As your solution evolves, Foundation is built to evolve with it. We support upgrades between Android versions using the same OTA framework. These migrations are complex and require joint planning with the customer and OEM, but we've successfully helped customers move to newer Android "dessert" releases in production environments.

## Foundation: Extending AOSP for Dedicated Use Cases

With the build structure and maintenance strategy in mind, let's explore the specific capabilities that make Foundation uniquely suited to dedicated device environments.

### Seamless Provisioning

Provisioning AOSP devices through standard methods can be tedious and operationally inefficient. Unlike GMS-based Android Enterprise, which offers various provisioning options, AOSP provisioning traditionally requires enabling Developer Options and connecting each device via USB, Ethernet, or Wi-Fi to a developer machine using ADB.

Esper Seamless Provisioning eliminates this overhead by allowing devices to auto-provision at first boot. Operators register devices using serial numbers or IMEIs — via manual input or CSV upload — and pre-assign Blueprints and tags. Upon first boot, each device connects to the Esper Cloud, is matched to its tenant and Blueprint, and is provisioned with policies, settings, and apps.

This approach transforms staging: devices can be drop-shipped and set up on-site by non-technical staff. For example, a convenience store customer used this model to install kiosks in minutes, with store managers handling installation.

For OEMs, Foundation can be flashed at the factory with no dependency on existing Blueprints. Devices can be boxed, shipped through the supply chain, and ready for configuration once received. Customers often ask for a manifest that correlates serial numbers to individual units, allowing them to pre-assign Blueprints and ensure a smooth rollout.

Foundation also builds resiliency into the provisioning process. If a device is factory reset in the field, it will re-provision using the assigned Blueprint — preventing unauthorized use and maintaining IT control.

Connectivity is often a question here. For Ethernet devices (common in Foundation deployments), network access is automatic. For Wi-Fi-only devices, credentials can be embedded into the Foundation build to allow seamless first-time provisioning.

### Foundation SDK and Esper Device SDK

Foundation includes a set of APIs through the Foundation SDK, giving enterprise developers access to configuration controls not typically exposed by AOSP:

- Application-driven control of the navigation bar, including the ability to hide or show it dynamically  
- App data backup and restore, enabling controlled downgrades without losing user data (if compatible)  
- Remote customization of the boot animation, including the ability to change it post-deployment  

In addition, the Esper Device SDK, which is embedded in Foundation, extends control to standard Android app-level code, offering features such as:

- Adjusting screen brightness, orientation, and timeout  
- Triggering reboots, locking/unlocking the device, and toggling the custom Esper Settings app  
- Fetching device-specific settings and telemetry  
- Toggling Bluetooth and Wi-Fi states, managing mobile data and Wi-Fi hotspots  
- Granular USB control, including whitelisting for a specific app or managing permissions  
- App lifecycle control (clearing data, state management, permission grants, managed configs)  
- Managing Access Point Names (APNs) on the device  

These SDK capabilities create deep opportunities for operational tuning and automation, critical in large-scale fleet environments.

### Secure Remote ADB and WebADB (Preview)

Foundation supports secure remote ADB, providing powerful troubleshooting capabilities with the safety of remote toggling. By default, remote ADB can be disabled to block local USB-based access and can be re-enabled through Esper Console when diagnostics are required. This makes it possible to investigate complex device issues without physical access.

In limited preview, we also offer WebADB, which brings remote debugging capabilities directly into the Esper Console through the browser — no terminal or SDK tools required. It's an especially convenient option for distributed support teams.

### Additional Advanced Capabilities

Foundation includes a growing set of capabilities designed specifically for real-world fleet operations:

- **Mesh Networking Auto-Discovery:** Foundation devices on the same LAN subnet can discover and securely communicate with each other, enabling peer-based configurations for restaurants, QSRs, or retail locations.  
- **Titanium Browser:** A secure, Chromium-based browser maintained by Esper and optimized for kiosks and other dedicated use cases, addressing the lack of viable browser options in the AOSP ecosystem.  
- **WEST Web App Support:** Esper's Web App generation tool (WEST) offers similar functionality to Google's Managed Play web app tool — except it works for AOSP — enabling customers to create and manage web apps without requiring GMS.  
- **802.1X Ethernet Authentication:** Enterprise-grade Ethernet security not natively supported in AOSP, available in Foundation for secure public deployments (stadiums, kiosks, etc.).  
- **Persistent Log Buffers:** Standard Android logcat buffers are small and cleared on reboot, making post-mortem debugging difficult. Foundation extends this buffer significantly (targeting seven days) and includes an option for persistence across reboots. You also get access to `wpa_cli` and `dmesg` logs for deep Wi-Fi and kernel-level debugging.  
- **Esper Port Manager:** Enables Linux-level peripheral access from Android apps, bridging gaps for legacy hardware — crucial for vertical deployments with specialized or non-standard hardware interfaces.  

Let's now take a closer look at the branches within Foundation that support different hardware types and deployment strategies.

## Foundation x86

The Foundation x86 branch was developed in close collaboration with Intel and is designed to run on 64-bit x86 processors. Unlike our ARM builds, which rely on vendor-provided kernel and HAL components, Esper maintains the entire Android operating system stack on Foundation x86 — including the kernel, vendor layer, and Android Framework. This full-stack ownership gives us unparalleled control and flexibility.

Foundation x86 is widely adopted in retail and restaurant environments, especially for POS systems, ordering kiosks, and digital media players powered by Intel NUCs. It installs directly on bare metal — no virtualization required — and is factory-load ready. This makes it easy to integrate with OEM validation, burn-in testing, and production workflows.

While we're often asked about minimum hardware requirements, x86 systems vary too widely to publish a strict list. That said, we've successfully run Foundation x86 on 15+ year-old hardware with as little as 2GB of RAM. Of course, this limits performance and is only suitable for low-intensity workloads. We previously maintained a 32-bit version, but most customers have since migrated to 64-bit, and we've deprecated the 32-bit branch.

Foundation x86 is highly adaptable to specialized hardware. Devices with unique configurations — such as dual displays or peripherals connected via RS-485, serial, or parallel ports — can be supported through custom engineering. We offer packaged services to develop the necessary drivers and integration layers. While it's rare, some scenarios may require cooperation with the peripheral manufacturer. We evaluate these dependencies as part of our pre-sales due diligence.

To streamline development, we provide a watermarked build of Foundation x86 to qualified prospects for early testing. We recommend performing a bare metal install on your target system to validate compatibility and performance. BIOS/UEFI drift between x86 machines can introduce inconsistencies, so hands-on testing is the best way to identify and resolve issues early.

One important consideration: apps running on Foundation x86 must include the `x86_64` Application Binary Interface (ABI). This is a simple configuration change in Android Studio, but it's essential for compatibility. While Intel's Houdini binary translator allows ARM apps to run on x86 hardware, Foundation does not include Houdini by default. It can be added with additional engineering effort (via Intel) if absolutely necessary. However, we recommend building for `x86_64` natively to avoid translation overhead.

Although Foundation is based on AOSP, it can be used as a base for GMS builds — particularly under Google's EDLA (Enterprise Device Licensing Agreement) program. Since GMS is layered on top of AOSP, Foundation can be made EDLA-compliant through testing and validation. Note that Esper cannot certify GMS compliance directly — that's the responsibility of the EDLA licensee — but we can help run CTS and GMS test suites to prepare a Foundation build for GMS certification.

For OEMs or enterprises with highly specific hardware or performance requirements, we can create a custom "leaf" off the Foundation x86 branch. This allows for targeted customization and maintenance, including the generation of distinct OTA packages. However, these leaves require dedicated engineering resources to build, validate, and support over time.

**Evaluate Foundation x86:** If you're interested in evaluating Foundation x86 for your hardware or deployment, contact us to request a watermarked build.

## Foundation x86 Flip

Many enterprise customers — particularly in retail and restaurant sectors — are looking to migrate their existing Windows-based endpoints to Android. However, hardware replacement is expensive and disruptive. With Foundation x86 Flip, you don't need to rip and replace. Instead, you can remotely convert your Windows systems to run Foundation x86.

Here's how it works:

- A small bootstrap file is deployed to each Windows machine using your existing remote management tool.  
- The bootstrap initiates the conversion, either shrinking the Windows partition to preserve it or performing a clean install.  
- The device reboots into the Foundation installer.  
- Once installed, Seamless Provisioning completes the setup using the assigned Blueprint.  

The only requirement is associating the device's serial number with the appropriate Blueprint in advance. Once that's done, the process is fully touchless. Customers have reported a 95%+ success rate with this approach — most issues stem from BIOS drift or edge-case system configurations.

For situations where remote bootstrap isn't feasible, we've developed Firebolt, a USB-based utility that packages the entire conversion workflow. You configure Firebolt with your desired install parameters (e.g., preserve Windows or wipe clean), plug it into the target system, and let it handle the install and provisioning automatically.

## Foundation Emulator for Windows x86

In some deployment environments, everything runs on Android — except for one critical device, such as a manager's PC that must remain on Windows due to productivity tool dependencies. To bridge this gap, we developed the Foundation Emulator for Windows x86.

This emulator runs a fully managed, locked-down instance of Foundation on a Windows machine. From the perspective of Esper, it behaves just like a physical Android device:

- It's assigned a Blueprint  
- It receives policy, settings, and apps  
- It can be updated via OTA  

We even solved the challenge of LAN integration by enabling the emulator to use the Windows machine's NIC as a full network participant.

Think of it as an AOSP tablet that lives on your Windows desktop — managed, locked down, and secured by Esper.

If you have a use case that could benefit from the Foundation Emulator, reach out and we'd be happy to walk you through how it works.

## Foundation GSI for Arm

With the introduction of Project Treble in Android 8, Google introduced a modular architecture that separates the Android OS framework from the device-specific vendor implementation. This change was made to accelerate Android updates and simplify the maintenance lifecycle for device makers.

One key outcome of Project Treble is the ability to use a Generic System Image (GSI) — a complete, hardware-agnostic Android OS build that can be flashed onto any Treble-compliant device. With a GSI, you can replace the OEM-provided OS while leaving the vendor partition untouched.

Esper offers Foundation GSI for Arm as a way to deploy Foundation on Treble-compliant hardware without requiring deep customization or full re-engineering. This is especially useful for scenarios where customers want to leverage off-the-shelf Android devices (e.g., prosumer-grade tablets) but need a locked-down, enterprise-ready OS.

A common example: correctional facilities using Android tablets. Many consumer-grade tablets offer the right performance and price point, but the stock OS is too permissive and hard to control. By flashing Foundation GSI onto those devices, you get a secure, manageable experience — complete with Esper OTA support, remote management, and Blueprint-based configuration.

To install a Foundation GSI, you'll need the appropriate flashing tools provided by the silicon vendor. Some OEMs may restrict flashing, but most allow it when done properly. Caution is warranted here — flashing an incompatible GSI on a non-compliant device can result in a brick. We've seen this happen with devices that claim Treble compliance (`adb shell getprop ro.treble.enabled = true`) but fail in practice.

To help mitigate risk, Google offers a Dynamic System Update (DSU) mechanism. DSU lets you boot a GSI on supported Android 10+ devices without overwriting the original OS. It's a non-destructive test mode that enables quick evaluation. If the Foundation GSI works via DSU, you're in good shape to proceed with a full install.

DSU requires sufficient free storage space, and once testing is complete, you can remove the GSI by disabling it in Developer Options or via ADB. The device will then revert to its original OS with no data loss.

If you're unsure whether your hardware is compatible, Google provides Reference GSIs for Android 9–15. These can be used as a quick test: if the reference GSI boots successfully, Foundation GSI likely will too. If it doesn't, that's our problem to solve — not yours.

Foundation GSI brings the power of Esper to a wider range of Arm devices without requiring a bespoke build. It's a great fit for customers looking to scale with cost-effective hardware while still enforcing policy, security, and update control.

We provide a watermarked version of Foundation GSI for testing. Contact us to learn more.

## Foundation for Amlogic – Khadas VIM3 Line

Amlogic chipsets are commonly found in Android TV sticks and other low-cost digital media devices. However, these devices typically come with consumer-oriented firmware built for 10-foot UI experiences — not the best fit for enterprise use cases like digital signage or menu boards.

That said, the price point is compelling. Through collaboration with early customers, we identified the Khadas VIM3 line as a suitable platform for Foundation. VIM3 boards are powered by Amlogic and offer sufficient performance, availability, and build quality for dedicated deployments.

Esper has worked directly with Khadas to bring up Foundation on the VIM3. While these devices require some light preparation — such as optional enclosures or heatsinks — they remain far more cost-effective than NUCs or other premium media players.

The key advantage? You're not relying on questionable firmware that could introduce security risks into your network. Instead, you get Foundation — complete with OTA update infrastructure, remote management, Blueprint provisioning, and tight control.

While newer Arm-based digital signage hardware is emerging with better out-of-box support, VIM3 remains a proven option. Several of our customers have deployed it in the field for digital menu boards and signage at scale.

If you're looking for a cost-effective way to power AOSP-based digital media solutions, VIM3 with Foundation is worth exploring.

## Foundation Bespoke for Arm

Some OEMs are building highly specialized devices for enterprise or consumer markets — devices with no standard screen, unique input methods, and purpose-built hardware configurations. In these cases, the stock Android OS provided by the silicon vendor often falls short. It lacks the customization, polish, and control required to create a seamless product experience and manage it at scale.

That's where Foundation Bespoke for Arm comes in.

If the OEM has access to the Android vendor layer, Esper can deliver a fully customized build of Foundation. This includes not just OS-level enhancements, but also full branding and UI control. The device can be tailored end to end — from boot animation and first-boot experience to home screen layout, system dialogs, and update flows.

On top of this, all Esper device management capabilities are baked in, giving the OEM or enterprise full control over policies, software updates, provisioning, and troubleshooting.

Because Foundation Bespoke is built from the ground up, it's the most engineering-intensive branch in the Foundation family. It requires a dedicated bring-up effort and ongoing maintenance investment, and has the least leverage from existing Foundation codebases. However, for customers deploying at scale with a custom hardware design, the upfront cost is often outweighed by the long-term value of control, manageability, and brand fidelity.

We've brought Foundation Bespoke to life on a wide range of platforms, including MediaTek, Qualcomm, Synaptics, and even Rockchip. The custom nature of this engagement means we won't have a prebuilt Foundation image ready to test on your hardware. That said, we can provide a watermarked build from another Foundation branch to help evaluate Esper's management experience and overall platform approach.

If you're building something unique and need an Android OS that goes beyond the basics — with an MDM built for scale — reach out to us through our contact form. We'd love to hear more about your use case.

## How to Try Foundation

If any of these Foundation branches sparked your interest — whether you're deploying at scale, upgrading from Windows, or developing a custom product — let's talk.

Contact us and share your target hardware, use case, and any specific requirements. We'll work with you to determine the right branch, discuss engineering needs, and (where applicable) get a watermarked build in your hands for evaluation.

Some of these discussions may require an NDA, and we're happy to accommodate that.

**Foundation on.**