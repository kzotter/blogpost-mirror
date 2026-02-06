<!-- post.md -->

# AI at the Edge: The Real State of Play - OEMs
## Part 2: OEMs, Lifecycles, and the CTO's Actual Problem

*Keith Szot — Feb 03, 2026*

If you are a CTO with an edge AI mandate and an installed base of devices, your first problem is not AI models, frameworks, or vendors. It's where inference runs and how much of your existing fleet you are willing, or able, to change.

Most enterprises don't operate on AI data-center timelines. Retail, hospitality, healthcare, logistics, and industrial environments plan on five-, seven-, or even ten-year device lifecycles. AI, by contrast, is moving on consumer-like timelines. Silicon generations turn over annually. Toolchains quickly evolve. Capabilities leap forward and then age out almost immediately by vertical market standards.

The mismatch of long-lived fleets colliding with fast-moving AI is the defining tension shaping OEM behavior today.

This post is not a catalog of vendors. It is a field guide to understanding how today's OEM realities, silicon availability, and inference architecture shape the decisions CTOs are actually being forced to make.

We look at OEMs through a deliberately narrow lens: how their current platforms, lifecycles, and architectural choices shape what is possible for AI at the edge. It is not an assessment of overall product quality, market leadership, or customer success for the endpoints these OEMs offer.

None of the tradeoffs described here reflect lack of OEM ambition, they reflect the responsibility of serving vertical market customers.

## The Edge AI Questions CTOs Are Asking

When organizations say "we need to do edge AI," what they usually mean is one of four things:

Can we run inference on the devices we already have?

Do we need new hardware to do this responsibly?

Should we bypass endpoints and run inference locally on-prem instead?

Or should we centralize inference in the cloud and accept the tradeoffs?

OEMs matter because they largely determine the cost, timing, and risk of every answer.

## Decide Where Inference Runs

There are three anchor locations for inference at scale.

On-device inference offers the lowest latency and strongest privacy guarantees, but it creates the hardest lifecycle problem when capabilities are rapidly changing. This path only works when hardware access, OS support, and OEM capabilities align and when teams accept tight coupling between models, runtimes, and OS updates.

On-prem edge inference introduces a local compute node in a store, restaurant, warehouse, or facility. This preserves existing endpoints while modernizing compute. For many enterprises, this has become the most pragmatic way to introduce edge AI without triggering a mass hardware refresh.

Cloud inference is the fastest way to start and the easiest to scale. Latency, bandwidth costs, data gravity, and outage tolerance become the tradeoffs.

A practical deployment strategy is to go hybrid. Time-critical or privacy-sensitive inference stays local. Heavier, bursty, or non-urgent workloads go to the cloud. The real architectural question is not where inference can run, but when does it move?

OEM constraints strongly influence how cleanly that routing can be implemented.

## Enterprise Device OEMs: The Installed Base Reality

Zebra (including Elo), Honeywell, Datalogic, Getac, MicroTouch, Toshiba Global Commerce Solutions

Enterprise device OEMs optimize for predictability, certification, and survivability. Their customers expect devices to run reliably for years, often in harsh environments, with minimal operational drama.

Zebra and Honeywell increasingly ship Android devices built on Qualcomm platforms with accessible NPUs and GPUs. These platforms do not seek pure benchmark numbers. They are tuned for sustained performance under thermal and power constraints. Vision workloads, OCR, barcode interpretation, and task-specific inference dominate.

Datalogic occupies a distinct position shaped by its deep machine-vision heritage. Many of its platforms rely on disciplined CPU and GPU pipelines rather than headline AI accelerators. For customers already running deterministic vision systems, AI arrives as augmentation for improving accuracy and flexibility without discarding proven workflows.

MicroTouch, along with vendors like Touch Dynamic and Custom America, represents a class of systems with long "dwell" times and more flexible platform strategies than many traditional rugged OEMs. MicroTouch frequently adopts Android and Linux configurations built on MediaTek Genio-class SoCs, where integrated AI accelerators are readily available and exposed. Touch Dynamic and Custom America tend to follow similar architectural patterns, pairing displays and fixed systems with configurable compute rather than tightly integrated, closed platforms.

Getac, by contrast, spans Qualcomm-based Android devices and Intel-based Windows systems, allowing AI capability to enter through multiple paths, either via Qualcomm NPUs on Android or CPU- and GPU-based inference on Windows.

OEMs like Aava Mobile sit in an interesting middle ground. Android-first, but enterprise-disciplined, they tend to adopt Qualcomm platforms that expose AI acceleration without forcing consumer-driven refresh cycles. For teams that want more control than mainstream consumer Android allows without drifting into bespoke hardware this class of OEM offers a pragmatic path forward.

Toshiba's retail platforms, carrying forward the lineage of IBM's store systems, emphasize long-term availability and operational predictability. AI is introduced carefully here, often via CPU inference or adjacent compute rather than specialized accelerators.

Across this category, the pattern is consistent: AI capability is arriving, but it is shaped by the realities of long-lived fleets.

## The Low-Risk On-Ramps to Edge AI

### Kiosks and Drive-Through  
GRUBBR, Frank Mayer, Olea, Posiflex, Acrelec

Kiosks and drive-through systems are not the most glamorous edge AI endpoints, but they are among the most forgiving. They are fixed in place, power-rich, thermally stable, and modular by design.

This modularity is the quiet reason so much edge AI experimentation shows up here first. Compute can be introduced, upgraded, or removed without destabilizing the enclosure, the UI, or the surrounding workflow. Dropping in an x86 box, a NUC, or even a GPU-equipped sidecar is operationally tractable.

AI adoption in kiosks is often driven less by the use case than by the ease of implementation. The same dynamic applies to drive-through systems, where cameras, microphones, and local compute can be combined with relatively low risk.

### Kitchen Display Systems and Back-of-House Operations  
KitchenArmor, Epson

The highest economic impact of AI in hospitality doesn't have to appear in the customer experience. It can be behind the scenes.

Kitchen throughput, prep timing, ingredient usage, labor allocation, and anomaly detection are where AI delivers durable value. Kitchen display systems sit at the center of these workflows.

Notably, most KDS platforms today do not ship with native, general-purpose AI acceleration by design. These systems are built to be reliable execution surfaces, not experimental compute nodes.

In practice, the intelligence does not live in the display, it integrates with it. Most successful deployments rely on remote inference (CPU-based, edge-node-based, or cloud-driven) to serve KDS platforms reliably without compromising uptime or predictability. PerfectCo is one example of an ISV delivering AI-like capabilities using existing hardware designs.

### Digital Signage and Ambient Intelligence  
Instore Screens and Advanced Signage Platforms

Digital signage has quietly become one of the most AI-active edge categories. Audience analytics, dwell measurement, and content adaptation are inherently local problems. Latency and privacy matter.

Vendors like Instore Screens (available through Lenovo) are shipping compact signage controllers, such as FlexBox, with integrated NPUs, designed to run inference locally while fitting cleanly into enterprise procurement and lifecycle models. These systems illustrate how AI can be introduced without turning displays into complex endpoints.

In many ways, signage shows the end state other edge categories are still moving toward: intelligence placed close to the interaction surface, compute treated as modular infrastructure, and endpoints kept simple enough to survive long lifecycles.

## Platformized Retail Systems: Stability Over Silicon

Toast, Square, Clover

These platforms are deliberately conservative at the endpoint not because they lack ambition, but because their business models reward stability. They operate large, tightly managed estates where recurring revenue comes from software, services, and transactions, not hardware refresh.

Thus their velocity comes from product decisions, not device churn. Intelligence is pushed upward into tightly controlled cloud services, where it can be updated continuously and monetized predictably. Endpoints remain stable so operations remain predictable.

This is not a limitation, it's a design choice. For many operators, AI arriving as a service rather than as a hardware capability is the correct trade.

## Enterprise Vertical Infrastructure: Trust and Time

Global Payments (Xenial), NCR Voyix, PAR, Diebold Nixdorf, Oracle MICROS

These vendors operate at a different layer of the stack. They run the operational and transactional backbone of retail, hospitality, and financial self-service environments, often at national or global scale. In these systems, customers punish instability far more than they reward novelty.

The hardware platforms in this category are intentionally conservative. Xenial's GC26, for example, is built on long-life Intel x86 architectures optimized for predictability, availability, and certification. While these systems do not chase the latest AI accelerators, they provide stable, well-understood compute environments that can reliably host CPU-based inference, orchestration logic, and integration points for adjacent edge or cloud intelligence.

AI adoption here is deliberate by necessity. These vendors tend to introduce intelligence at the system and workflow level first spanning demand forecasting, optimization, fraud detection, labor and inventory analytics often with inference running nearby rather than embedded directly in the endpoint.

When AI arrives in this layer, it tends to be durable rather than flashy. CTOs should expect progress on timelines that respect trust, compliance, and operational risk and platforms that are designed to support AI as a long-lived capability, not a transient feature.

## Edge Compute as a Pressure Valve

### HP and Lenovo: Two Paths to Enterprise Edge AI

HP and Lenovo both make visible a pattern many enterprises are converging on but they arrive there from different starting points.

Lenovo operates across a remarkably broad hardware spectrum. On one side of the business, it ships large volumes of PC-like endpoints into retail and hospitality environments: Windows POS systems, NUC-like form factors, and a wide range of tablets, including devices used directly in vertical workflows. On the other side, Lenovo has invested heavily in edge infrastructure through its ThinkEdge portfolio, including compact systems capable of hosting discrete GPUs.

This breadth gives enterprises optionality. Modest AI capability can exist at the endpoint through integrated NPUs in Intel Core Ultra or Qualcomm-based designs while heavier inference workloads are pulled inward to edge nodes that can be upgraded independently. Lenovo's approach assumes heterogeneity and embraces architectural flexibility.

HP's path is more focused. HP does not meaningfully participate in vertical tablets, but it has deep roots in fixed-location retail hardware and is actively energizing its edge business around AI-driven solutions. Recent organizational changes reflect a push to treat AI not as a device feature, but as part of a broader retail and edge offering.

In practice, this means HP often concentrates intelligence adjacent to endpoints rather than distributing it widely. Compact edge systems and accelerator-equipped platforms become the natural home for generative and multimodal workloads, while POS and other endpoints remain stable and predictable.

Both approaches converge on the same operational truth: distributing GPUs across thousands of endpoints rarely scales. Architecturally, x86 expandability is powerful. Operationally, enterprises prefer concentrating complexity where compute can be cooled, serviced, upgraded, and governed without destabilizing the fleet.

## Payment Terminals: Compliance Defines the Boundary

Verifone, PAX, Ingenico, Castles, BBPOS

Payment terminals operate under some of the strictest regulatory regimes in the enterprise landscape. While many now run Android-based operating systems, any AI execution on the terminal itself remains tightly constrained by certification, security, and compliance requirements.

Dedicated AI accelerators, if present at all, are rarely exposed. CPU-based processing dominates, typically sandboxed and vendor-controlled. Vision, biometrics, and fraud-related capabilities tend to be fixed-function rather than general-purpose.

As a result, intelligence around payments increasingly lives outside the terminal in adjacent services responsible for identity, risk assessment, policy enforcement, and orchestration. The terminal's role narrows toward secure execution, while decision-making logic moves upward in the stack.

CTOs should assume payment terminals will primarily consume AI services rather than host them, a shift that is already reshaping how value and responsibility are distributed across the payments ecosystem.

## Emerging Android-First OEMs: Speed With Responsibility

iMin, Bluebird, SUNMI, Newland, Chainway, Urovo

This class of OEMs adopts MediaTek and Qualcomm silicon aggressively and tends to expose NPUs earlier than traditional enterprise hardware vendors. From a pure capability standpoint, many are ahead of the installed base when it comes to on-device AI potential.

Within this group, there are meaningful differences. Vendors like iMin stand out for taking a more integrated, product-driven approach pairing MediaTek platforms with thoughtful industrial design and a tighter hardware–software story. The result feels less like a collection of SKUs and more like a deliberate ecosystem, which makes emerging AI capabilities easier to reason about and experiment with.

Others in the category optimize for speed and scale, moving quickly to new silicon and form factors, often with impressive hardware at aggressive price points. The tradeoff across the class is lifecycle ownership. Faster refresh cycles and shorter guarantees shift more responsibility onto the customer.

These platforms excel at pilots, innovation-forward deployments, and localized rollouts. Scaling them into long-lived, globally managed fleets is possible but it requires discipline and strong fleet controls.

## CPU-Only Inference: How to Know If You Already Have Enough

A surprising amount of useful edge AI does not require NPUs or GPUs.

Modern CPUs can handle quantized (lower precision) vision models, OCR, anomaly detection, recommendation systems, and task-specific language models. For many enterprises, the real question is not whether CPUs can do AI, but what kinds of AI they tolerate.

Hardware refreshed within the last two to three years is often more capable than teams expect. In practice, compute limits are frequently encountered later than memory limits. Adequate RAM, storage throughput, and IO bandwidth often matter as much as raw CPU performance.

For CTOs looking to evaluate this quickly, the simplest test is not a benchmark, it is a workload probe. Take one representative use case. Run it locally. Observe latency, concurrency, and failure behavior under realistic load. If inference remains predictable and does not starve the rest of the system, you likely have more headroom than you assumed.

Teams evaluating CPU-only inference should focus less on theoretical peak performance and more on workload characteristics: model size, quantization level, latency tolerance, and how many requests must be served simultaneously. Many vertical use cases fit comfortably within these constraints when expectations are grounded in operational reality.

CPU inference is not a fallback. It is often how AI ships on enterprise timelines quietly, incrementally, and without forcing premature hardware decisions.

## Refresh, Pattern, and the Shape of a Sustainable Strategy

Hardware refresh is not the enemy of edge AI. It is often the enabler.

Newer platforms bring better thermals, improved acceleration, and longer runway. OEMs have invested heavily in making AI-capable hardware available across categories, and those advances matter. The opportunity lies in refreshing intentionally. Not all at once (unless you've had a capital budget windfall or Finance wants to take advantage of accelerated depreciation opportunities), not everywhere, but in ways that compound value over time.

Across successful deployments, a consistent pattern emerges. Endpoints remain modest. Inference is treated as a service. Local edge compute absorbs change.

Phased refresh, targeted upgrades, and aligning new hardware with inference placement allow enterprises to introduce AI without unnecessary disruption. Edge compute acts as a bridge between generations, enabling new capabilities to arrive before every endpoint is replaced.

When inference can be discovered, routed, and upgraded independently of endpoints, AI becomes something enterprises can actually operate and not a one-time upgrade, but an evolving capability that survives hardware cycles.

## What This Means Going Forward

OEMs are not blocking AI at the edge. They are shaping it under real constraints.

Consumer silicon will always move first. Vertical silicon will follow. Long-life enterprise SKUs will lag both. That sequence is structural, not accidental.

CTOs succeed by designing architectures that survive that reality and by refreshing hardware in ways that compound advantage rather than reset it. Compounding, in this context, means each generation of hardware expands what is possible without forcing wholesale replatforming. It means inference placement, fleet management, and operational controls remain stable even as silicon capabilities improve underneath them.

When refresh cycles add capacity without invalidating prior decisions, AI becomes an evolving capability instead of a recurring disruption.

Throughout this post, OEMs were discussed only in terms of how their platforms enable or constrain AI at the edge. In many other dimensions, these same vendors differentiate in ways that matter deeply to customers. This lens was intentionally narrow, because AI capability is now intersecting with hardware lifecycles in ways that cut across otherwise strong product strategies.

The next layer down, the silicon vendors, is where these dynamics originate. That's where we turn next!

## A Note on Timing

One last thought, and it's less about technology than timing.

Most edge AI conversations happen too late. They start after hardware has already been selected, budgets allocated, and refresh cycles locked in. At that point, teams are no longer designing systems, they're negotiating constraints.

The most productive conversations happen earlier when fleets are still in motion, when inference placement is still flexible, and when the difference between a three-year decision and a seven-year one is negotiable.

At Esper, we spend a lot of time in that early window, often before there's an RFP or a hardware refresh is officially on the calendar. The work is less about selling software and more about helping teams reason clearly about what they already have, what they're likely to need next, and where AI actually belongs in their architecture.

If this post surfaced questions about your current fleet, your next refresh, or how AI fits into decisions you haven't made yet, I'm always happy to talk. These conversations are most useful early before decisions harden and options narrow.

You can reach me directly, or connect with us at Esper. Either way, the earlier the conversation starts, the more room there is to get it right.