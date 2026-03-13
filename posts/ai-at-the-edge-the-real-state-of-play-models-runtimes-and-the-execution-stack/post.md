---
title: "AI at the Edge: Models, Runtimes, and the Execution Stack"
series: "AI at the Edge: The Real State of Play"
author: "Keith Szot"
date: "2026-02-06"
canonical_url: "https://keithszot.substack.com/p/ai-at-the-edge-the-real-state-of-3c1"
slug: "ai-at-the-edge-the-real-state-of-play-models-runtimes-and-the-execution-stack"
---

The edge AI conversation often starts in the wrong place.

Most discussions begin with models. Which one is best, which one is smallest, which one can run locally. Those questions matter, but they hide a deeper system reality. A model is not a product. A model is not even a workload by itself. A model is a component that only becomes useful once it is placed inside an execution environment that can feed it data, manage its lifecycle, and survive the operational realities of real deployments.

Once teams move beyond demos, the problem quickly shifts away from model selection and toward execution architecture.

The real question becomes: how does the model run?

This is where runtimes, execution providers, and inference stacks enter the conversation.

Edge AI systems live or die based on the interaction between three layers:

- The model itself  
- The runtime that executes the model  
- The hardware acceleration layer beneath the runtime  

When these layers align, inference becomes predictable and efficient. When they do not, the system behaves inconsistently, consumes too much power, or simply fails to deploy.

Understanding this stack is essential before anyone begins designing edge AI systems at scale.

## Models: The Portable Illusion

Modern machine learning models are often described as portable artifacts. Export a model from a training framework, package it in a standardized format, and deploy it anywhere.

Reality is less tidy.

Model portability exists mostly at the serialization layer. Formats like ONNX, TensorFlow Lite, and PyTorch packages provide ways to represent neural network graphs and parameters. But those formats do not guarantee that a model will execute efficiently — or even correctly — across different hardware platforms.

Different runtimes support different operator sets. Some runtimes perform graph rewriting or optimization passes during loading. Others require compilation steps before inference can occur. Quantization strategies vary. Memory alignment assumptions differ.

What appears to be a universal model artifact is often closer to a negotiation between the model and the runtime environment that loads it.

Teams usually discover this when the same model produces dramatically different performance across devices that appear similar on paper.

The model did not change. The runtime environment did.

## Runtimes: The Hidden Operating System of AI

If models are the artifacts, runtimes are the machines that interpret them.

A runtime loads the model, schedules operations, manages memory buffers, dispatches compute to hardware accelerators, and handles fallback paths when hardware capabilities are missing. In effect, the runtime behaves like a miniature operating system dedicated to machine learning workloads.

Several runtimes dominate edge AI environments today.

### ONNX Runtime

ONNX Runtime has become one of the most widely adopted inference runtimes for cross-platform AI deployment. It supports execution across CPUs, GPUs, and NPUs through modular execution providers.

This architecture allows the runtime to delegate portions of the model graph to different accelerators depending on hardware availability. If an accelerator cannot execute a particular operator, the runtime falls back to CPU execution.

This flexibility makes ONNX Runtime attractive for heterogeneous fleets where hardware capabilities vary across devices.

### TensorFlow Lite / LiteRT

TensorFlow Lite, now evolving into LiteRT, remains deeply integrated into the Android ecosystem. It provides optimized inference for mobile and embedded platforms and supports hardware acceleration through delegates such as NNAPI, GPU delegates, and vendor-specific accelerators.

LiteRT is increasingly becoming the default runtime for Android-based edge AI deployments, particularly when tight integration with platform services is required.

### PyTorch Mobile and ExecuTorch

PyTorch has historically been associated with training environments rather than deployment. That is changing.

ExecuTorch represents Meta's effort to create a lightweight runtime capable of executing PyTorch models efficiently on edge hardware. It focuses on small footprint deployment, compatibility with PyTorch workflows, and integration with modern accelerator pipelines.

For teams deeply invested in the PyTorch ecosystem, ExecuTorch may reduce the friction between training and inference.

## Execution Providers and Hardware Acceleration

Runtimes alone do not guarantee performance. Hardware acceleration is where the theoretical efficiency of AI workloads becomes practical.

Modern edge processors increasingly include specialized hardware for AI workloads:

- GPUs for parallel compute  
- NPUs designed specifically for neural network inference  
- DSPs optimized for signal processing workloads  

Execution providers act as bridges between runtimes and these hardware accelerators. They translate runtime instructions into hardware-specific commands.

The difficulty is that execution providers are rarely portable. Each silicon vendor implements its own acceleration stack.

Qualcomm, MediaTek, Intel, NVIDIA, and Apple all expose different toolchains and optimization pipelines. A model optimized for one platform may perform poorly on another without additional tuning.

This fragmentation is one of the central challenges in edge AI deployment.

## Memory and Thermal Constraints

Edge devices operate within physical constraints that do not exist in cloud environments.

Memory capacity is limited. Thermal envelopes restrict sustained compute workloads. Power availability varies widely across device classes.

Transformer-based language models illustrate this clearly. Memory bandwidth often becomes the limiting factor long before raw compute capacity is exhausted. Even when a device technically supports running a model, sustained inference may cause thermal throttling that dramatically reduces performance over time.

Designing edge AI systems therefore requires understanding not just peak performance, but sustained performance.

A model that performs well for thirty seconds may behave very differently after thirty minutes of continuous inference.

## The Importance of Benchmarking

Because runtime behavior varies across hardware platforms, benchmarking becomes essential.

Synthetic benchmarks often fail to capture real-world performance characteristics. They measure peak throughput rather than operational stability.

Effective benchmarking for edge AI deployments should consider:

- Cold start latency  
- Sustained inference throughput  
- Thermal throttling behavior  
- Memory pressure under concurrent workloads  

These measurements provide a more accurate picture of how systems behave under production conditions.

## The Edge Execution Stack

When these layers are viewed together, the edge AI execution stack becomes clearer.

At the top sits the model — the artifact created during training.

Beneath the model sits the runtime, which interprets and executes the model graph.

Below the runtime sits the hardware acceleration layer, translating runtime instructions into device-specific compute operations.

Each layer introduces variability. The success of an edge AI system depends on how well these layers align with each other and with the constraints of the target hardware.

## Why This Matters

The excitement around edge AI often focuses on models and capabilities.

But systems do not run on models alone.

They run on stacks — and stacks have friction.

The teams that succeed with edge AI are rarely the ones that chase the newest models. They are the teams that understand how the execution stack behaves under real-world conditions.

In edge computing, architectural discipline matters more than novelty.

Because once the system ships, the hardware stays where it is.

And the software must live with the consequences.
