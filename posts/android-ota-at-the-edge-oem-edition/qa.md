# Android OTA at the Edge – OEM Q&A

**Who is this for?**  
OEM product leaders, engineering managers, and CTOs shipping Android into vertical markets.

**What is the core argument?**  
Once Android devices become infrastructure, OTA becomes a governance problem, not a feature.

**Why does GMS create tension for vertical markets?**  
Because Google operates a parallel update authority optimized for global security velocity, not fleet uptime predictability.

**Why does the factory image matter so much?**  
Partition layout, slot strategy, flash sizing, and Verified Boot decisions determine what updates are possible years later.

**What is the risk with BSP-provided OTA clients?**  
They may exist without clear ownership, telemetry, or signing governance, creating security and operational risk.

**Why is AOSP attractive despite higher responsibility?**  
It consolidates update authority and removes parallel control planes, improving predictability for long-lived fleets.

**What role does Esper Foundation play?**  
It provides a disciplined OS foundation that enables controlled OTA, backporting, and lifecycle governance without OEMs building everything themselves.

**What differentiates successful OEMs in vertical markets?**  
They own the build, the keys, the OTA system, and the lifecycle instead of assembling inherited pieces.