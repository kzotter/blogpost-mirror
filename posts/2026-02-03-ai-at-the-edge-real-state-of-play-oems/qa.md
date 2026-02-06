<!-- qa.md -->

# Q&A Companion — AI at the Edge: The Real State of Play (OEMs)
## Part 2: OEMs, Lifecycles, and the CTO's Actual Problem

### What problem is this post actually solving?
It reframes "edge AI" away from model worship and toward operational reality: where inference runs, what your current fleet can tolerate, and how OEM lifecycle constraints quietly decide what's feasible long before a data scientist gets involved.

### Why are OEMs so central to edge AI decisions?
Because OEMs control the shape of the box you're stuck with for five to ten years: silicon availability, OS support, exposed accelerators, certification posture, long-life SKUs, and what kinds of updates are safe to ship at scale. They don't just sell devices. They sell the boundaries of your future architecture.

### What are the four "edge AI" questions CTOs are really asking?
They boil down to: can we run inference on what we already deployed, do we need new hardware to be responsible, should we shift inference to an on-prem edge node to avoid refreshing endpoints, or should we centralize in the cloud and accept latency, bandwidth, and outage tradeoffs.

### What are the three anchor locations for inference?
On-device, on-prem edge (a local compute node per site or facility), and cloud. The post's punchline is that hybrid is normal: keep time-critical and privacy-sensitive work local, push heavy and non-urgent workloads outward. The real question is when inference moves, not whether it can.

### Why is on-device inference "the hardest lifecycle problem"?
Because it creates tight coupling: models, runtimes, drivers, OS versions, and OEM firmware have to stay aligned while silicon capabilities churn annually. In a long-lived fleet, that coupling becomes a tax you pay every time the industry leaps forward.

### What makes on-prem edge inference so pragmatic?
It's a pressure valve. You modernize compute without destabilizing endpoints. You get a place to run newer models, swap accelerators, and upgrade independently while letting the fleet keep doing its boring, profitable job.

### Why is cloud inference still attractive?
It's the fastest to start and easiest to scale organizationally, but you trade for it with latency, bandwidth costs, data gravity, and outage tolerance. You also inherit whatever "oops" moments happen when connectivity or cloud dependencies go sideways.

### What characterizes the classic enterprise device OEMs?
Predictability, certification, survivability, and long-term availability. Zebra and Honeywell increasingly lean on Qualcomm Android platforms that expose NPUs/GPUs, tuned for sustained performance rather than benchmark heroics. Datalogic brings machine-vision heritage and often succeeds with disciplined CPU/GPU pipelines rather than chasing accelerators.

### Why do kiosks and drive-through systems show up as early edge AI labs?
Because they're fixed, power-rich, thermally stable, and modular. That modularity means you can drop in compute sidecars (x86 boxes, NUCs, GPU-equipped nodes) without rewriting the whole endpoint story or risking uptime in the core workflow.

### Why don't kitchen display systems (KDS) usually host AI directly?
Because KDS devices are designed to be reliable execution surfaces, not experimental compute nodes. The successful pattern is intelligence integrating with the KDS via remote inference (CPU, edge node, or cloud) without compromising predictability.

### Why is digital signage "quietly" AI-active?
Because audience analytics, dwell measurement, and content adaptation are inherently local problems where latency and privacy matter. Signage controllers with integrated NPUs can keep displays simple while placing intelligence close to the interaction surface.

### Why are platformized retail systems (Toast, Square, Clover) conservative at the endpoint?
Because their revenue favors stability. They monetize software and services, not device churn. So intelligence tends to live in controlled cloud services where it can be updated continuously, while endpoints remain stable to keep operations predictable.

### What's different about "enterprise vertical infrastructure" vendors?
They run the transactional backbone, and customers punish instability. Hardware tends to be conservative (often x86 long-life designs) which still supports durable CPU inference, orchestration logic, and integrations with adjacent edge or cloud intelligence. The cadence is slower, but the capabilities stick.

### What's the point of the HP vs Lenovo comparison?
It shows two routes to the same operational truth: distributing GPUs across thousands of endpoints rarely scales. Lenovo embraces heterogeneity across endpoints and edge nodes, while HP tends to concentrate intelligence adjacent to endpoints. Both converge on concentrating complexity where it can be cooled, serviced, upgraded, and governed.

### Why will payment terminals mostly consume AI services rather than host AI?
Compliance and certification define the boundary. Even when terminals run Android, AI execution is constrained, accelerators are rarely exposed, and CPU processing is sandboxed and vendor-controlled. Intelligence shifts upward into adjacent services for identity, risk, policy enforcement, and orchestration.

### What's the opportunity and risk with emerging Android-first OEMs?
They often expose NPUs earlier and move fast on MediaTek and Qualcomm silicon, making them great for pilots and innovation-forward deployments. The tradeoff is lifecycle ownership: shorter guarantees and faster refresh cycles push more responsibility onto the customer to keep fleets stable.

### How do you know if CPU-only inference is "enough"?
Skip theoretical peak performance and run a workload probe. Pick one representative use case, run it locally, and observe latency, concurrency, and failure behavior under realistic load. In practice, memory limits often bite before compute does, so watch RAM, storage throughput, and IO bandwidth as much as CPU.

### What does a sustainable edge AI strategy look like?
Intentional refresh, not a mass refresh. Keep endpoints modest, treat inference as a service, and use local edge compute as the bridge between silicon generations. The goal is compounding advantage: each new hardware generation expands what's possible without invalidating prior architectural decisions.

### What's the "timing" warning at the end?
Most edge AI conversations start after hardware is already chosen and budgets are locked, which turns architecture into constraint negotiation. The best outcomes happen earlier when inference placement is still flexible and the lifecycle tradeoffs can be designed instead of endured.