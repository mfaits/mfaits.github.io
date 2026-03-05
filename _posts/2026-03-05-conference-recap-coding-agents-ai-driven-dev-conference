---
layout: post_with_subscribe
title: "Conference Recap - Coding Agents: AI-Driven Dev Conference"
date: 2026-03-05
category: blog
tags: [coding-agents, llm, agents, evals, devtools, mlops]
—

# Conference Recap — Coding Agents: AI-Driven Dev Conference

The [Coding Agents: AI Driven Dev Conference](https://app.mlops.community/events/coding-agents/agenda) was a one-day conference put on by the [MLOps Community](https://home.mlops.community/home/events). I recommend this group’s events, and I found this one especially useful. It was aimed at technical builders, and many of the talks included practical action steps for people building with agents.

The lightning talks were especially strong, and they managed to get a lot of talented people on stage sharing very concrete advice. I walked away with several ideas that I’ve already started implementing, and being there in person gave me a really good pulse check on where engineers are right now.

---

## Top-level themes

* The bottleneck in software has shifted from code → process.
* Everyone seems to have moved past the phase where LLMs proving they can solve greenfield problems was surprising. The conversation has shifted away from which model is best, or look how good this model does on a benchmark evaluation. We all assume you have your favorite model doing good work for you, and the conversation now is what happens when you put these systems inside large production codebases.
* Trust, verification, and evals are becoming core engineering problems.
* Infrastructure for agents (durability, orchestration, and tooling) is like the next frontier.

---

## Spiciest take

> “We don’t really believe in PMs.”

Scott Breitenother from Kilo Code said that with agentic coding, their model is that one engineer owns one feature, end to end, from design to collecting user feedback. They have a very horizontal organization where one PM owns the platform, and that’s it. This generated a lot of opinions over lunch.
---

## Most actionable takeaway

Run the scorecard tool in [this repo](https://github.com/sshh12/coding-agents-workshop) to evaluate how optimized your codebase is for agents.

[Shrivu Shankar](https://blog.sshh.io/) ran a workshop called **“Optimizing Codebases for Agents,”** which was one of the highlights of the conference for me. He started from the premise that agents will increasingly become the primary interface for interacting with codebases, so we should design codebases with agents in mind. This seems quite right to me.

[His slides are available here](https://html-preview.github.io/?url=https://github.com/sshh12/coding-agents-workshop/blob/main/slides.html) and are worth reading.

There is a striking video in there of a side-by-side agent session in which the same model is given the same prompt:

> “Add experiment tagging. New endpoint POST /api/experiments/{id}/tags and show tags on the detail page. Follow existing patterns. Run tests.”

The prompt is run against two repositories, one which is a typical messy production repo and one in which Shankar implemented his suggested optimization steps for repo optimized for agent collaboration. The agent working in the messy repo actually runs faster, but it overwrites tests and ignores design conventions. The optimized repo produces much cleaner results.

The scorecard tool evaluates a repository along three dimensions Shankar identifies as key for agent readiness:

- Rules File & Agent Config  
- File Organization  
- Test & Verification  

Below is a truncated output from running the tool on one of my own vibe-coded projects. It produces very actionable feedback, including suggestions like adding resolution hints to error messages and adding test protection rules.

> Dimension 1: Rules File & Agent Config — 0/3
> No CLAUDE.md exists. The README is a single line (just the project title). There is no .claude/ directory, no hooks, and no documented commands, repo map, or completion criteria.
> Key gaps:
> * No documented setup commands, test commands, or deployment steps
> * 15+ required environment variables scattered across code with no documentation
> * No architecture overview or definition of done
>  * Tests exist in CI/CD infra but no test commands are documented anywhere
> Quick win to Score 1: Create a ~100-line CLAUDE.md with setup instructions, python -m pytest tests/, and a repo map.
> –-
> Dimension 2: File Organization — 1/3
> Basic layer-based structure exists, but significant mixed concerns:
> *Type hints are present throughout (good)
> *Error messages are generic with no resolution guidance (e.g., logging.error(f"Error loading CSV: {e}"))
> *No feature-based subfolders (e.g., scrapers/aila/, scrapers/calbar/)
> To reach Score 2: Split update_attorneys.py into per-source modules under scripts/scrapers/.
> 
> Dimension 3: Test & Verification — 1/3
> 172 test methods across 32 test classes in tests/test_core.py — solid unit test coverage with full mocking of external dependencies.
> However:
> *Tests are not protected — no .claude/settings.json, no CLAUDE.md rules
> *Tests never run in CI/CD — deploy_lambda.yml deploys without running tests
> *No linting, formatting, or type-checking enforcement (type hints exist in code but mypy/flake8/black are not configured)
> *Post-commit hooks exist only for roborev code review, not test execution
> To reach Score 2: Add test protection rules to a CLAUDE.md + add python -m unittest to the deploy workflow.
> To reach Score 3: Add PostToolUse hooks + configure flake8/mypy/black + integrate into CI/CD as a gate.
> –-
> Summary
> The codebase has solid technical fundamentals (good test coverage, working CI/CD, type hints) but zero AI collaboration infrastructure. The highest-impact improvements are: (1)          > create a CLAUDE.md, (2) add tests to the deploy workflow, and (3) split update_attorneys.py > by scraper source.
 
My favorite rules, which have already changed how I work, come from the Test & Verification dimension:

> “Baseline tests are immutable. Protect existing tests from agent modification.”

and

> “Agents write new tests, test-first.”

In other words: **TDD for agents**. Write the failing test first, then implement.

I’ve been letting agents write tests for a while, it was one of the first things I outsourced to AI, but the idea of locking a baseline test suite is clever. It keeps you in control of how your project evolves.

Shankar’s three slides with guidance on how to optimize the three dimensions are reproduced below - I highly recommend checking out his [full slides](https://html-preview.github.io/?url=https://github.com/sshh12/coding-agents-workshop/blob/main/slides.html).

<h3>Slides: Agent-readiness dimensions (Shrivu Shankar)</h3>

<p>
Shankar summarized agent-ready repositories along three dimensions. These slides from the workshop outline concrete patterns for each.
</p>

<div style="
  display:grid;
  grid-template-columns: repeat(auto-fit, minmax(320px, 1fr));
  gap: 1.5rem;
  margin: 1.5rem 0;
">

<figure>
  <img src="{{ '/assets/images/shankar-agent-readiness-1.png' | relative_url }}" 
       alt="Agent readiness dimension: Rules files and agent configuration"
       style="width:100%; border-radius:8px;">
  <figcaption style="color:#666; font-size:0.9em; margin-top:0.5rem;">
    Rules files and agent configuration patterns that help agents understand how to work in a repository.
  </figcaption>
</figure>

<figure>
  <img src="{{ '/assets/images/shankar-agent-readiness-2.png' | relative_url }}" 
       alt="Agent readiness dimension: File organization patterns"
       style="width:100%; border-radius:8px;">
  <figcaption style="color:#666; font-size:0.9em; margin-top:0.5rem;">
    File organization patterns that make it easier for agents to navigate large codebases.
  </figcaption>
</figure>

<figure>
  <img src="{{ '/assets/images/shankar-agent-readiness-3.png' | relative_url }}" 
       alt="Agent readiness dimension: Testing and verification practices"
       style="width:100%; border-radius:8px;">
  <figcaption style="color:#666; font-size:0.9em; margin-top:0.5rem;">
    Test and verification practices, including immutable baseline tests and TDD workflows for agents.
  </figcaption>
</figure>

</div>


---

# Quick talk-by-talk highlights from the rest of the day

## Sid Bidasaria (Anthropic) — Verification, governance, and “plan mode”
Sid’s through-line was that getting value from coding agents isn’t just about model quality—it’s about verification and workflow design. Anthropic has moved toward remote dev environments, which created surprising friction around verification (including needing a proxy setup back to a local machine). He emphasized that Claude can work with logging/observability tools, but only if you deliberately configure access. On team adoption, his advice was basically: let people experiment, and consensus will emerge around what works—then measure it (plugin marketplace + usage/download counts as a signal).
The most practical thing I’m stealing: his heavy emphasis on plan files. He has Claude “interview” him for edge cases, then produces a high-density plan that correlates strongly with successful outcomes—and they check those plans into version control, both for humans and for future agent runs.
**Why it matters:** The bottleneck shifts to trust, and plans + tailored review harnesses are how you keep trust from collapsing as PR volume explodes.

---

## Scott Breitenother (Kilo Code) — Process is the bottleneck
Scott’s message was blunt and consistent with what a lot of people were hinting at: when implementation gets cheap, the process becomes the bottleneck. He described Kilo’s move toward end-to-end ownership (one engineer owns one feature, including user feedback loops) and a culture that minimizes collaboration unless it adds value (he referenced the “anti-collaboration” framing).

**Why it matters:** Even “great agents” stall if the organization is still optimized for a world where coding speed is scarce.
---

## Niels Bantilan (Union AI) — The step after observability is durability

Niels’s talk hit a theme I heard repeatedly: you can build a great agent… and then production infrastructure ruins your day. He framed this as an agent infrastructure problem: failures at the container/compute/network layer, preempted spot instances, resource contention, etc.
His solution pattern was essentially self-healing agents, enabled by three building blocks:
- Replay logs (recover state + resume a run)
- Global caching (don’t pay twice for the same work)
- Intermediate state persistence (treat state like a first-class artifact you can reload)
He anchored it with a case study building a “solutions architect” agent that maintains a huge knowledge graph—where durability and caching unlock both reliability and cost savings.
**Why it matters:** If agents are going to run continuously, reliability has to be designed in—not bolted on.

---

## Zach Lloyd (Warp) — Agents in the cloud
Warp’s keynote was about moving multi-agent workflows off the laptop and into a cloud runtime—basically treating agent runs like managed compute tasks. The pitch: named agents + reusable skills + scheduling + monitoring + shared infrastructure that makes it easier for teams to standardize and scale.
This infrastructure makes it easier for teams to run large multi-agent workflows collaboratively.

**Why it matters:**  
We are in the “one engineer managing several agents” era, and local machines aren’t a great fit for that anymore.

---

# Lightning talk grab bag

### Pinterest (Faye Zhang) — Productionizing subagents
Faye focused on using subagents/swarm mode to compress ML development timelines (she cited a dramatic improvement in cycle time). She listed common failure modes (drift, imbalance, memory collapse, tool misuse) and emphasized structured instructions + hooks for machine-readable outputs + customized memory systems.
**Why it matters:** Once agents become part of core dev workflows, “ops for agent teams” becomes a real discipline.
### Cleric (Erin Ahmed) — Fixing agent amnesia
Erin framed learning agents as the opposite of stateless chat sessions: agents should learn your environment, your team preferences, and corrections over time—where good corrections persist and compound.
**Why it matters:** Persistent learning is a requirement for long-lived agents doing ongoing operational work.
### Semgrep (Milan Williams) — Practical security for AI-generated code
Milan’s advice was classic security posture, but updated for agents: least-privilege permissions, logging before you need it, hooks for audit logs, and scanning before code ships.
**Why it matters:** If PR volume goes exponential, security posture can’t be manual.
### Databricks (Ankit Mathur, Aarushi Shah) — Agent sprawl and the gateway layer
They argued the “inevitable outcome” is coding agent sprawl—different tools for different tasks—which becomes a top cost driver. Their response: a gateway for observability, cost controls, privacy, and unified authentication for MCP tools.
**Why it matters:** Tool standardization won’t happen by decree. It’ll happen via shared governance layers.

---

## Final thoughts

The biggest shift I noticed throughout the conference is that the hard problems are moving away from models and toward systems. Models are improving quickly, that’s a given. The real engineering challenges now involve:

- trust and verification  
- evaluation frameworks  
- infrastructure durability  
- agent-friendly codebases  
- governance and cost control  

In other words, building with coding agents is rapidly becoming a systems engineering problem. For now, this is what the role of the dev has changed to, and what we can do beyond what non-engineers vibe coding with an agent can do. The work is to build robust and resilient production systems. While we’re at it, we have to rethink the bottlenecks of code review and meetings.

