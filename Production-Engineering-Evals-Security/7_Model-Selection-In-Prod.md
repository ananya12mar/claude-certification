# Model Selection in Production

## Problem

The model you choose sets the baseline cost, latency, and quality for the system.

## Why it matters

- Model choice is a production decision, not just a prompt decision.
- Higher-tier models cost more and usually run slower.
- The cheapest model is not always the right one if quality drops below the bar.

## Model trade-off

- Haiku: lowest cost and latency; best for simple tasks
- Sonnet: balanced default for most production workloads
- Opus: stronger reasoning and more capable on hard tasks

## What to do

- Start with the cheapest model that still meets the quality bar.
- Use evals to decide when to step up or down.
- Route only the hard cases to a stronger model.
- Keep a single default model when traffic is uniform.

## When to change tiers

- Step up when evals show current quality is below the required bar.
- Step down when a cheaper model still meets the task quality standard.

## Takeaway

Model selection should be driven by measured quality, not by default habit.

Choose the cheapest model that passes the eval for the workload.
