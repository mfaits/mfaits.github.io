---
layout: post_with_subscribe
title: "Filing Cabinets, Institutional World Models, and Going to the Warehouse"
date: 2026-09-28
category: blog
tags: [AI, data science, LLMs, RAG]
---

This blog post from Byrne Hobart does an excellent job contextualizing the types of project that I’m being asked to build over and over in my data science work lately: [https://www.thediff.co/archive/forward-deployed/](https://www.thediff.co/archive/forward-deployed/)

I’m a Senior Data Scientist at my org (in West Coast terms, cracked AI Engineer) and part of my work is evaluating and scoping new project requests from business as they come in before they get distributed to engineers and data scientists for building. I see new requests from business stakeholders in their raw form. Repeatedly, for a couple years now, the requests have the following kind of shape - “we have lots of team knowledge stored in disparate places, and we’d like an AI we can talk to that knows all of that stuff.”

As a shorthand, I started calling these “filing cabinet” projects at work. As in: “Can you please plug my filing cabinet full of documents into AI?”

The frustration seems to be that LLMs are powerful, but not useful without context. Most business teams do not have their knowledge neatly arranged in a form that an LLM can consume.

Hobart writes:

> “It’s trapped in email inboxes, groupchats, ERPs, CRMs, Excel files, the airwaves of phone calls and also in the heads of (and in the conversations between) doctors, line engineers, and other front-line workers who embody the valuable knowhow they’ve earned through experience.”

This echoes pretty much exactly the issue that business stakeholders bring to me. “All our stuff is in Sharepoint or emails, how do I get an AI that knows all that stuff so I can use it effectively?”

The general pattern we’ve been repeating is to figure out where all the relevant information is, try to enforce some data hygiene about keeping it all in certain defined places moving forward, and then usually vectorize it and expose a RAG system to an LLM chat interface for the requesting team.

![A telephone sitting on top of a filing cabinet in a drab office](/assets/images/filing-cabinet-ai.png)

*My custom GPT connected to a RAG API. Slop image source: ChatGPT.*

That “try to enforce some data hygiene” is doing a lot of heavy lifting there. Eventually, people realize they have additional context from other Teams chats that aren’t getting ingested by your bespoke RAG system, or they copy a file from your beautiful “all documents in here can be assumed to be ground truth” repository and they start saving it and editing it locally and then sharing it through other channels, or at the very least, the place where one business team saves all their documents isn’t the same place as another business team so you’ll be starting another filing cabinet project pretty soon with all new data connectors.

The fact that filing cabinet projects kept coming up over and over again gave me the intuition that there must be some kind of fundamental first-principles problem going on, but I couldn’t put it into words. I think Hobart nails it though, and that’s why I’ve been widely sharing that post link with people along with a message like “read this if you have time, I think it’s important”:

> “Palantir bet that the next generation-defining company would natively align itself with institutions to make their data legible, integrate it into computable ground truth, and in the process enables these institutions to solve problems and serve society more effectively. The dream was that they could finally connect the rapid progress the economy has been experiencing in the world of bits for the past 50 years to the relatively stagnant world of atoms, and, in this process of extending increasing-returns-to-scale characteristics to more of the economy, become fabulously rich themselves.”

Fundamentally these requests keep coming back to the same problem that I haven’t been able to put into words - all this knowledge is not accessible as computable ground truth.

But big players like Palantir and the frontier AI labs with their forward-deployed engineers are currently hard at work doing this integration. So:

- This confirmed for me that the filing cabinet problem is not unique to my workplace - lots of organizations are seeing the same thing.
- We can’t assume the current “but what can I actually DO with AI” feeling is going to hold, as institutional knowledge gets integrated into bits. I think pretty quickly, all my stakeholders that are feeling like “I can’t really ask the AI what I really want because it can’t possibly know all the important and relevant things that I know” aren’t going to feel that way any more, and then AI use for non-tech people is going to feel more like how it feels for engineers now.

For engineers, AI systems are already increasingly useful because they can be connected to the things we actually work with: the codebase, documentation, tools, logs, APIs, environments. They don’t have to answer a programming question while pretending that none of those things exist. I think nontechnical knowledge work starts feeling very different when the same thing happens for the rest of an institution.

For me, after Hobart’s post put these filing cabinet problems into a broader perspective, I was left with this question: if this is what the filing cabinet projects are actually pointing toward, what does this mean for what's next for data scientists and engineers? I came away with two conclusions.

First, I think the right technical direction to focus on is getting very, very good at building what Hobart calls “institutional world models.” Sam Altman says [“almost everyone I’ve ever met would be well-served by spending more time thinking about what to focus on”](https://blog.samaltman.com/how-to-be-successful). Hobart describes the idea this way: institutional world models represent the real-time state of an organization well enough that people can use them to understand what is happening, predict the consequences of decisions, act, and then learn from what happened. That matches what I think business stakeholders have fundamentally been asking for and what I think will allow them to leverage technology most effectively.

And second, maybe consilience is a moat. I had to look up the word consilience after reading Hobart’s post (dictionary definition: “linking together of facts and theories from separate academic fields to create a common groundwork of explanation”) and it describes what I think has been the secret sauce of excellent technologists for a long time - can you understand the context of a brand new project well enough to know how the pieces fit together and build the tool that solves the real problem, even if the end users didn’t know how to describe what the real problem is?

Hobart writes:

> “Like Elon, the prototypical engineer-CEO, the best FDEs are deeply curious and ruthlessly pragmatic. They seek to possess an almost superhuman understanding of the real-time state of capabilities and opportunities within their businesses, identify the key blockers (problems) to executing on those opportunities, and go to ground truth as a way to access and instrument the context required to devise systematic solutions.
>
> In repeatedly doing this, they not only develop an exceptional big picture understanding of the businesses they work within, but also translate that understanding into software that embodies that representation with more and more accuracy over time, and allows everyone in an organization to use that better global understanding to better solve their local problems.”

This concept gives me something to steer towards while trying to understand the role of the engineer in the age of AI, which without something to steer towards can start to feel like this:

<blockquote class="twitter-tweet">
  <a href="https://twitter.com/simeonGriggs/status/2102866666682249325"></a>
</blockquote>
<script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

Stay deeply curious and ruthlessly pragmatic. Understand, deeply understand, deep in your bones, the context of what you’re building.

When I was building a truck route optimizer for a company that had warehouses across the US, I requested our materials data with volume measurements for what we stocked in the warehouse. I was told by data teams in corporate that this data did not exist. “You’ll have to ask the warehouse employees to measure them with a tape measure and record it for you,” they said. The team building the optimizer took field trips to the warehouses to talk to the dispatchers who would be using our tool. I mentioned that we didn’t have volume information about our stocked materials, so I was having a hard time building in loading capacity constraints for the available trucks. The dispatchers, rightfully, looked at me like I was an idiot. Of course they had volume information for all materials that they stocked in the warehouse. The warehouse was enormous. It all ran on an inventory system that dictated where things got stored based partly on their size. The entire physical operation depended on knowing this information.

I asked them what the inventory software was called, which was enough for me to find the underlying data tables, and I was able to integrate the volume constraint into the truck routing tool.

What the corporate data teams lacked, and what I lacked until I went to the warehouse, was an accurate model in my head of how the institution worked.

Institutions are endlessly complex. Every data science project I’ve worked on in my career is like a glass pane over an infinitely deep rabbit hole of complexity. You can choose (or sometimes are forced to choose based on time constraint) whether to just ship based on what’s asked of you or to explore the rabbit hole - why do you store the data this way? What regulatory rule caused you to make that decision? Who actually enters this field? What does it mean when they leave it blank? Can I please talk to the person who uploads this information? What happens after someone clicks this button?

Go to the warehouse, understand how it works. I think this is the key to being a great engineer/data scientist in the AI era.
