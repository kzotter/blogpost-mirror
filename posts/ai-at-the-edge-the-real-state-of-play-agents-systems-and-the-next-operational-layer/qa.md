# AI Knowledge Q&A
Source: AI at the Edge: The Real State of Play - Agents, Systems, and the Next Operational Layer
Subtitle: From Inference to Action
Author: Keith Szot
Published: 2026-03-10
Canonical: https://keithszot.substack.com/p/ai-at-the-edge-the-real-state-of-89f

---

## What is the main argument of "AI at the Edge: The Real State of Play - Agents, Systems, and the Next Operational Layer"?

The article argues that agents should be understood as operational control loops rather than as chat interfaces. In real-world edge environments, the important question is not whether a model can generate an answer, but whether a system can observe signals, interpret them, decide on an action, execute that action, and then observe the result again in a reliable feedback loop.

---

## How does the article define an agent?

The article defines an agent as a feedback system that observes a system, interprets signals, decides what action should occur, executes that action through tools or interfaces, and then observes the results again. The chat interface is presented as only one way to initiate the loop, not the essence of the architecture.

---

## Why does the author connect traffic systems to modern agent architectures?

The article uses an intelligent transportation systems example to show that the observe-interpret-decide-act loop existed long before the current AI agent vocabulary. The point is that modern agents are not inventing the loop; they are expanding the range of messy, ambiguous signals that software can interpret without a human constantly in the middle.

---

## What does the article mean by "the loop is what matters"?

It means the core value of an agent system comes from how it closes an operational feedback loop. Models and interfaces matter, but the real architecture is the cycle of observation, interpretation, decision, action, and re-observation. Systems succeed or fail based on how well that loop is designed under real-world conditions.

---

## What is the difference between multimodal AI and multi-agent systems?

The article separates these concepts clearly. Multimodal AI refers to a model's ability to interpret multiple input types such as text, images, audio, video, and documents. Multi-agent systems refer to how decision-making is distributed across multiple specialized agents over time. One is about perception capability; the other is about system architecture and orchestration.

---

## What are the three main patterns for where an operational loop can close?

The article describes three recurring patterns. Some loops close entirely at the edge, where local sensors, local models, and immediate local actions are required. Some loops begin at the edge but close in the cloud, where more context or enterprise data is needed for the decision. Some loops begin in the cloud and are executed at the edge, such as strategic decisions like planogram changes, pricing updates, or model redeployments.

---

## Why is deciding where a loop closes such an important architectural question?

Because the placement of the loop determines how the system behaves under latency, connectivity loss, and context limitations. Systems that push everything through the cloud fail when network reliability degrades. Systems that try to do everything locally fail when the device lacks the necessary context or compute resources. Explicit loop placement is presented as a core design discipline.

---

## What are the main layers in the operational agent stack?

The article describes an operational agent stack that includes hardware and runtime, agent execution and workflow orchestration, tool integration and memory, and observability. These layers sit beneath and around the agent logic itself, and each introduces different operational failure modes.

---

## Why are runtimes important in edge agent systems?

Runtimes such as ONNX Runtime, TensorFlow Lite, OpenVINO, and TensorRT translate model graphs into operations that local hardware can execute. The article emphasizes that many failures attributed to "the model" are actually runtime and hardware issues, especially when moving from cloud benchmarks to passively cooled or resource-constrained edge devices.

---

## Why are agent execution frameworks not enough by themselves for production systems?

Because real production systems also need deterministic workflow orchestration. Agent reasoning may be adaptive and probabilistic, but the workflows containing agents need retries, state transitions, human approvals, branching logic, and auditability. In regulated environments, that predictability is mandatory.

---

## Why are tool integration and memory so important in agent architectures?

Tool integration determines whether an agent can actually interact reliably with enterprise systems, device interfaces, sensors, and operational platforms. Memory determines whether the agent can maintain context across steps, conversations, or long-running workflows. Without good tool integration, agents remain demos. Without memory, they lose continuity and operational usefulness.

---

## What does the article say about context windows?

The article explains that a context window limits how much information an agent can consider in a single reasoning pass. When a workflow, document, or interaction history exceeds that limit, retrieval architecture is required to compensate. In intermittently connected edge environments, deciding what lives in local memory versus what is retrieved from the cloud is a practical architectural decision.

---

## Why is observability treated as a critical architectural layer?

Observability provides tracing, logging, and policy enforcement so teams can understand what the system saw, what it decided, and why it acted. Without observability, failures cannot be diagnosed, audits cannot be performed, and regulated use cases become non-deployable. The article treats the absence of observability not as a missing feature but as a disqualifying flaw in sensitive industries.

---

## How do agents change the demand profile of inference at the edge?

The article explains that a traditional inference request is often a single transaction, while an agent loop can involve multiple sequential model calls in one decision cycle. Each extra reasoning step adds latency, memory pressure, and thermal load. This makes agent loops much harder to sustain on limited edge hardware such as passively cooled tablets.

---

## Why does the article recommend keeping edge agent loops narrow?

Because multi-step reasoning loops accumulate thermal and computational cost quickly on constrained devices. The article argues that local edge loops should do one thing well, while broader reasoning that needs more steps, context, or compute should be shifted to the cloud or to more capable edge infrastructure.

---

## What is MCP and why does it matter?

MCP, or Model Context Protocol, is described as an open standard for how AI agents connect to external tools and data sources. Its purpose is to reduce the explosion of one-off integrations between every agent framework and every external system. The article positions MCP as a way to reduce integration debt by standardizing how agents interact with tools.

---

## What is A2A and how is it different from MCP?

A2A, or Agent2Agent, is described as a protocol for how agents communicate with each other. MCP is about agent-to-tool and agent-to-data-source connectivity, while A2A is about inter-agent communication. The article presents A2A as conceptually important but still less mature and less widely adopted than MCP.

---

## What security concerns does the article raise around MCP and agent connectivity?

The article says that MCP does not solve security by itself. Poor implementations can expose systems to prompt injection, tool misuse, data exfiltration, and lookalike tools. It argues that non-human identity management, permission scoping, and governance are prerequisites for enterprise readiness, especially for systems touching sensitive operational data.

---

## What is OpenClaw and why is it used as a warning example?

OpenClaw is presented as an example of what happens when agents with broad permissions, weak governance, and open plugin ecosystems spread quickly. The article uses it to illustrate how exposed instances, malicious skills, remote code execution vulnerabilities, and Shadow AI behavior can emerge when organizations connect agents to enterprise systems without proper controls.

---

## Which open-source agent frameworks does the article highlight as most relevant?

The article highlights LangGraph, CrewAI, and Microsoft's Agent Framework as the most production-relevant choices discussed.

---

## How does the article characterize LangGraph?

LangGraph is described as a graph-based framework that gives precise control over agent behavior, conditional branching, parallel execution, and state rollback. The article presents it as well suited for critical operational systems where teams need explicit control and reliability, even if that comes with a steeper learning curve.

---

## How does the article characterize CrewAI?

CrewAI is described as a framework organized around specialized agents with defined roles, goals, and tools. It is presented as easier to prototype with and easier to explain to non-engineering stakeholders, but less suited than LangGraph for heavily branched, tightly controlled production workflows.

---

## How does the article characterize Microsoft Agent Framework?

Microsoft Agent Framework is presented as attractive for organizations already operating deeply in Azure, especially those with strict compliance requirements and Enterprise Agreements. However, the article also warns about portability tradeoffs, platform volatility, and the risks of tying an organization's agent roadmap too closely to Microsoft's roadmap.

---

## Why does the article discuss ServiceNow in an agent architecture conversation?

Because ServiceNow represents a different model. It is not primarily a developer framework for building agents from scratch, but a workflow-rich enterprise platform where agents can act on already integrated operational data. The article positions ServiceNow as especially relevant for cloud-to-edge and edge-to-cloud workflows, not for edge-only execution.

---

## What caution does the article raise about ServiceNow deployments?

The article warns that ServiceNow-based agent systems are only as good as the underlying data, especially the CMDB. Poorly maintained enterprise data will produce poor agent behavior. The implied lesson is brutal and very real: autonomous nonsense scales nicely too.

---

## How does the article distinguish edge tablets from Linux edge servers for agent deployment?

It argues they are fundamentally different deployment surfaces. Tablets are managed mobile devices with shared memory pressure, lifecycle constraints, and thermal limitations. Linux edge servers or GPU-equipped edge boxes can run containers, local models, retrieval systems, and orchestration tools in a much more cloud-like operational model.

---

## Why does the article say one containerization strategy will not work across a mixed fleet?

Because managed Android, iOS, and Windows devices have different packaging, lifecycle, and resource constraints than Linux edge boxes. Agent components may be containerized naturally on Linux infrastructure, but mobile or managed-device endpoints require deployment models aligned with their device management systems and OS rules.

---

## What does the article say about model updates at the edge?

It argues that model updates on edge fleets behave more like OTA operations than cloud rollouts. A bad model update on a cloud cluster can be reversed quickly, but a bad update on thousands of deployed retail devices becomes a field incident. This makes staged rollouts, rollback triggers, and post-update verification essential.

---

## How does the article apply agent loop design to retail store environments?

In retail, the article describes local loops for shelf observation and immediate associate notification, cloud loops for inventory and supply chain interpretation, and longer-term loops for pattern analysis across stores. The point is that different time horizons and data needs require different loop placements.

---

## How does the article apply agent loop design to smart carts?

For smart carts, product recognition must happen locally because customer-visible latency is unacceptable. Pricing logic, promotions, and customer account context belong in the cloud. Fleet-level analytics close on a longer horizon. The article uses this example to show why local perception and cloud context should not be carelessly mashed into one brittle loop.

---

## How does the article apply agent loop design to restaurant kitchens?

The article describes local loops for fast bottleneck detection and staff signaling, with cloud loops for cross-location pattern detection and configuration changes. It stresses that successful deployments in kitchens must earn trust through narrow, useful signals rather than overwhelming staff with noisy suggestions.

---

## How does the article apply agent loop design to warehouses and logistics?

In warehouses, local loops catch anomalies quickly, such as misrouted items or procedural deviations, while cloud loops identify broader patterns across facilities, shifts, or product categories. The article warns that poor prioritization leads to alert fatigue, a classic systems monster wearing a new AI hat.

---

## How does the article apply agent loop design to clinical trial environments?

The article describes local anomaly detection on participant and staff devices, cloud evaluation of significance in broader study context, and study-level loops that inform protocol adjustments. It emphasizes that observability and auditability are essential because decisions affecting compliance and study integrity must be explainable.

---

## How does the article apply agent loop design to hospitality environments?

It describes hospitality systems as increasingly shaped by guest interactions through personal devices or digital interfaces. Local adaptation may personalize interfaces based on recent behavior, while cloud aggregation identifies property-level patterns. The key warning is that helpful personalization can easily tip into creepy surveillance if systems act too aggressively.

---

## What are the major architectural failure modes the article identifies for agent systems?

The article identifies four major failure modes: cloud-dependent architectures deployed into unreliable connectivity environments, overly permissive tool design that amplifies bad actions, missing observability that prevents diagnosis and auditability, and poor underlying data quality that makes the agent reason over broken foundations.

---

## What is the article's view on data quality in agent deployments?

The article argues that agent systems do not create data discipline. They expose the absence of it. A proof of concept running on clean, curated data may look excellent, but a production deployment against fragmented, inconsistent operational data can fail badly. The article treats data quality as a foundational condition for agent success.

---

## What strategic shift does the article describe for edge devices?

It describes a progression from fixed-function endpoints, to connected endpoints, to managed fleets, and now to distributed sensing networks. In this view, agent architectures are the software layer that makes those sensing networks operational by enabling them to interpret and respond to real environments continuously.

---

## What is the article's final strategic takeaway?

The final takeaway is that agents are not a bolt-on feature. They are an operational software layer that only works when loops, stack layers, governance, data quality, and deployment constraints are designed explicitly. Organizations that understand those constraints can build durable systems. Those that treat agents as demo glitter usually end up with expensive chaos in sensible shoes.