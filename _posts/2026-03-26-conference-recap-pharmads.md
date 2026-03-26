---
layout: post_with_subscribe
title: "Conference Recap - PharmaDS"
date: 2026-03-26
category: blog
tags: [coding-agents, llm, agents, conferences, biotech, pharma]
---

# Conference Recap: PharmaDS 2026

I spent the past few days at the [Pharmaceutical Data Science](https://phds.nestat.org/) (PharmaDS) Conference in Edison, NJ. It’s a small, focused conference sponsored by the New England Statistical Society, and I’d recommend it to anyone doing data science or AI engineering in pharma or biotech. I like the size (50–100 people). If you’re in this niche, basically every talk is directly relevant to your interests. It’s also a great way to get a pulse check on where everyone is with AI in our highly regulated space.

“AI in pharma” is a very different conversation from “AI, generally.” A lot of the “hook a Mac Mini up to Open Claw and YOLO, baby” energy can’t apply in our world. The constraints of building tech in a regulated space can feel frustratingly slow at times, but they also make for a more interesting problem. They force certain challenges into sharp focus. The tools we build are held to high standards of reproducibility and explainability, so many of the talks emphasized building those in from the start. There’s no room to just try something and maybe get it wrong when it comes to medicine. You have to get it right from the beginning. It means we move more slowly, but more deliberately, and that’s a work style I don’t mind.

I noticed a few themes that emerged from across the talks.

---

## Look beyond the core science for places AI can help with clinical trials

One of the clearest throughlines was this: AI is making a real impact today, but mostly on operations, not core science. The keynote speaker, [Andrew Garrett](https://phds.nestat.org/speakers.html#andrewgarrett), said he sees that:
- AI is improving efficiency of clinical trials.
- These improvements have been in things like site performance, scheduling, and operational logistics. Think things like measuring which clinical trial sites are most efficient and optimizing for their participation.
- The main use of AI in clinical trials today is not necessarily replacing core statistical or clinical decision-making yet.

The keynote was followed by a panel which included [the FDA’s Assistant Director for Data Science and AI Policy](https://www.linkedin.com/in/ginnes/), who pointed out that AI is easiest to deploy in areas that are not directly under regulatory scrutiny. For example, using AI for things like scheduling clinic time could decrease trial time and cost without falling in the FDA’s regulatory purview.

The takeaway seemed to be that there are lots of places where AI can increase clinical trial speed and efficiency while decreasing costs without touching the trial protocols or scientific operations directly.

---

## AI is best with standardization, and our world is already really good at standardization.

In the clinical trial world, the Clinical Data Interchange Standards Consortium (CDISC) is a global nonprofit that develops data standards for clinical data. Their Study Data Tabulation Model (SDTM) is a data standard that is required for any clinical trial submission to the FDA. This means that our whole field has aligned on a tabular data standard - doesn’t matter if the data is coming from academia, different companies, etc. That’s great news! Universal standards makes development smoother and easier for programmers and makes things smoother for AI as well. 

Bill Wang (Merck) talked about this in his session on quantitative safety evaluation. He showed examples of using LLMs to turn unstructured text into structured regulatory data. That includes converting FDA drug labels into binary or ternary toxicity classifications, or doing [large-scale extraction of liver toxicity mechanisms from free text](https://www.frontiersin.org/journals/artificial-intelligence/articles/10.3389/frai.2022.999289/full). I asked him what we can do to better prepare clinical data for AI, and his answer was pretty simple. We already have the right foundation. Standards like SDTM are exactly what you want. You just have to build them into the process early instead of treating them as a final formatting step. That feels directionally right to me. If your data is already structured, consistent, and machine-readable, you are setting yourself up to actually get value out of AI systems instead of fighting your inputs.

---

## Human-in-the-loop isn’t going away

I think "human-in-the-loop" was the phrase I heard the most often throughout the talks. During the keynote panel, the FDA perspective was that documentation and oversight scale with risk, which naturally pushes toward systems where humans stay involved in higher-stakes decisions . That showed up globally too. In the regulatory session on China, Prof. Hou discussed the explicit requirements that physicians verify AI outputs before they’re used in clinical decision-making . And even in more technical system design talks, the pattern was the same. Multi-agent workflows for things like literature review or inclusion and exclusion criteria generation always included expert oversight or a validation layer. There was also a lot of emphasis on auditability, versioning, and traceability in systems that touch GxP workflows. You can absolutely use AI to draft, extract, and accelerate, but you still need a clear chain of responsibility. 

This was something I was trying to emphasize in my own presentation as well. I presented on the tool that my colleague [Swathi Yanture](https://www.linkedin.com/in/swathi-yanture/) and I built that uses a hybrid agentic/RAG system for MedDRA coding, and I always love talking about the cool tech parts, but I allocated a good part of the talk to discuss the human review and oversight parts that are baked directly into our pipeline.

The takeaway for me is that in this space, the goal is not autonomy, but rather building systems where AI does more of the work, but humans remain accountable for the outcome.

---

## The take I’ll carry with me 

> “Don’t automate an inefficient process.”

The keynote speaker said to think of it like a dishwasher. A dishwasher doesn’t wash dishes the same way a human does, it does it better and more efficiently. And, for what it’s worth, a dishwasher is a human-in-the-loop system - you put the dishes in and look at them when you take them out. I learned from Janelle Shane that in AI, there’s [chess problems and there’s laundry problems](https://www.sciencefriday.com/segments/weird-artificial-intelligence/#segment-transcript). Now from this conference I will be thinking about chess problems, laundry problems, and dishwasher solutions.

---
