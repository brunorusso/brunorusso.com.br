---
title: "Architecture & Engineering in Technology"
author: "Bruno Russo"
date: 2026-10-11 21:30 +0300
categories: ["Arquitetura"]
tags: ["arquitetura", "governança", "tecnologia"]
ping: true
math: true
mermaid: true
image: 
    path: https://www.brunorusso.com.br/assets/2026/arquitetura_engenharia.jpeg
    alt: "The image illustrates the path from the macro to the micro: on the left, the technology architecture represented by diagrams, flows, and infrastructure models; and as one moves to the right, these plans connect and materialize into source code—the essence of daily software engineering delivery."
---

## Architecture & Engineering in Technology

What I am going to share in this post is simply my personal opinion, based on articles, conversations with leaders from various companies, other architects, friends, and so on.

Architecture and Engineering: two teams working together to build the best solutions for customers. This is the model many companies adopt to develop and evolve their applications, whether for internal use or for external use by their customers, for example.

Before starting any discussion, as the topic can be controversial depending on your perspective, it is important to define these two areas.

### Definition of Architecture and Engineering

**Architecture**

Technology Architecture is the discipline responsible for designing, structuring, and aligning information technology components (software, infrastructure, data, and networks) with a business's strategic goals. It defines technical standards, integration rules, security guidelines, and system topologies to ensure that IT environments are scalable, resilient, secure, and cost- and operationally efficient.

Martin Fowler, in his article “Who Needs an Architect?” (Fowler, 2003), shared Ralph Johnson's thoughts on architecture, highlighting: “Architecture is about the important stuff. Whatever that may be.”

Beyond these points, I believe all of this is anchored by one fundamental word: **communication**, which I address at the end of the article. In an excellent article, [Ana Brenes](https://www.betterask.erni.ch/the-triple-a-saga-architecture-architects-and-agile-part-i/#:~:text=%E2%80%9C(1)%20A%20formal%20description%20of%20a%20system%2C,design%20and%20evolution%20over%20time%E2%80%9D%20(TOG%2C%202018)) covers this communication topic, describing the importance of "communicating ... to the relevant people."

**Engineering**

Software Engineering (or IT Engineering) is the application of a systematic, disciplined, and quantifiable approach to the development, operation, and maintenance of software systems.

The term became widely adopted across the industry because building software at an enterprise scale requires practices very similar to traditional engineering (civil, mechanical, or electrical). Some practices adopted by engineering include:

1. **Full Software Development Life Cycle (SDLC):** From inception, requirements gathering, and feasibility analysis to test automation, deployment (CI/CD), production monitoring, and eventual decommissioning;

2. **Quality Assurance and Testing:** Defining automated testing strategies (unit, integration, regression, load, and security) to prevent regressions and ensure predictability;

3. **Maintenance and Evolution:** Continuous focus on reducing technical debt, refactoring, and ensuring ease of maintainability by other teams;

4. **Metrics and Processes:** Using data to measure efficiency and reliability—such as lead time, deployment frequency, change failure rate, and mean time to recovery (MTTR).


## Architecture & Engineering: How Do They Work in Practice?

The distinction between the two areas is typically understood through the relationship between **the design (what to build)** and **the construction (how to build and maintain it)**. The table below provides a high-level comparison of key differences between them:

| Aspect | Technology Architecture | Software / IT Engineering |
| --- | --- | --- |
| **Main Focus** | Structure, standards, feasibility, and strategic alignment. | Implementation, construction, automation, and efficient operations. |
| **Scope of Vision** | Macro/systemic vision (how building blocks and platforms connect). | Micro/operational vision (how internal components are coded and tested). |
| **Typical Deliverables** | Blueprints, C4 diagrams, technical standards, trade-off analyses. | Source code, CI/CD pipelines, test suites, deployable artifacts. |
| **Fundamental Question** | *"How should this solution be designed to meet the requirements?"* | *"How do we build, test, and maintain this solution with maximum quality?"* |

In modern organizations, both areas operate in continuous collaboration: architects set the guidelines and boundaries, while engineering builds and validates solutions within those guardrails. At least, that is what is expected.


### Steak on the Plate vs. Bread Dough

Looking at the table above, specifically the first row, we have the **Main Focus**. Notice that architecture is responsible for defining _structure_, _standards_, etc., whereas engineering focuses on _Implementation_.

> I understand and agree that the more thoroughly business needs are analyzed and structured into a plan, the better the final application will be. However, let's face it: with the massive adoption of artificial intelligence today, the task of "coding" itself has become much "faster" compared to two decades ago.

What I want to highlight here is that engineering puts "steak on the plate"—that is, it delivers usable software quickly and practical. Architecture, on the other hand, prepares what I call "bread dough": the dough needs to be kneaded, rested, shaped, and then baked. Consequently, engineering delivers ready value quickly, whereas architecture often takes a long time to produce a deliverable.

> It is important to emphasize that I am not judging the quality of what is delivered. I am simply presenting facts.

To illustrate this difference from another angle, consider the following scenario.

**The simple calculation scenario**

In the same room analyzing a requirement sit an engineer and an architect. The following problem is presented to both:

Consider variable Value-A equal to 1 and variable Value-B equal to 1. What is the result of adding these two variables?

The Engineer promptly answers: **2**

The Architect responds: **It depends.** And asks whether the values of each variable are integers.

A short explanation of this context:

**The Engineer's answer is strictly correct**, while the Architect's response comes from an excess of **caution**.

Breaking down the explanation for both sides:

Why is the Engineer's answer mathematically correct?

In pure mathematics and number theory:

- The symbol **1** represents the unit within a number system (whether Natural numbers $\mathbb{N}$, Integers $\mathbb{Z}$, Rationals $\mathbb{Q}$, or Reals $\mathbb{R}$).
- Addition $+$ is a binary function universally defined across these sets.
- By the axiomatic definition of numbers (Peano Axioms), the sum of $1 + 1$ is **invariably 2**, regardless of whether the number is classified as an integer, float, or complex number. $1.0 + 1.0$ remains $2.0$.

**Where does the Architect's provocative question come from?**

The Architect's doubt would only make sense if we were dealing with **data typing in programming** or **problem domain context**, rather than pure mathematics:

1. **Typing and Memory Representation:**
- If they are integers: `1 + 1 = 2`.
- If they are *strings* (text): `"1" + "1"` results in `"11"` (concatenation).
- If they are booleans: `true + true` in C/C++ results in `2`, but in boolean logic ($1 \lor 1$) the result is $1$.
- In floating-point arithmetic with limited precision, $1.0 + 1.0$ results in $2.0$, but *overflow* or type conversions could alter the stored result.


**The Architect's "Professional Bias":**

The joke accurately portrays the Architect's mindset: before accepting a premise or performing a calculation, they question **boundaries, context, data types, and system constraints** (non-functional requirements).


**Summary**

Mathematically, **1 + 1 is 2** and there is no ambiguity. The Architect attempted to treat a basic **arithmetic problem** as if it were a **system modeling problem**, where unstated assumptions can break an application in production.

> Thanks to Google Gemini for helping with the explanation above.

Jokes aside, note that the engineer's priority is delivery, while the architect's priority is identifying edge cases that may not even need to be discussed. Thus, the architect keeps making the "bread dough" while the engineer puts the "steak on the plate."

From a business perspective—which is always hungry and needs immediate satisfaction—it naturally prefers the steak on the plate, as it solves the immediate problem.


### The Real Value Delivered

In an ideal scenario, both roles function as a necessary counterweight. However, when poorly balanced (which is the main problem), their behaviors introduce well-defined risks to the business:

**The fast-delivery perspective (Engineering focus)**

Execution and value delivery drive the company. Focusing on solving the immediate problem and getting value into customers' hands quickly generates revenue, validates hypotheses, and keeps the company competitive.

- **The value:** Fast deliveries (Time-to-Market), practical problem solving, and focus on immediate results.
- **The risk of excess:** If engineering focuses *only* on the short term while ignoring context, it builds what the market calls a "house of cards." The system accumulates **technical debt** so rapidly that, within 1 or 2 years, any simple change takes months or causes production outages.

**The sustainability perspective (Architecture focus)**

Architecture's role is to prevent today's decisions from crippling the company tomorrow. However, unpragmatic questions disconnected from the business context lead to **Analysis Paralysis** (*Over-engineering*).

- **The value:** Medium/long-term vision, scalability, security, and ensuring maintenance costs do not explode in the future.
- **The risk of excess:** Questions disconnected from immediate reality that block deliveries, waste hours in conceptual meetings, and fail to deliver real business value in time.

> A corporate balance point is essential

This provocation exposes a common failure in "ivory tower" architectures: **the architect who questions just for the sake of questioning, lacking pragmatism**.

In the modern corporate landscape, a good architect **is not someone who blocks fast delivery**, but someone who enables engineering to deliver fast **with the lowest possible risk**, making *trade-offs* explicit—and communication is fundamental to achieving this.

> Engineering's value delivery is **frequent and immediate**; Architecture's value is **cumulative**, ensuring the organization can continue delivering quickly 2 to 5 years down the road.


### The New Architectural Mindset

I see one of the biggest pain points in modern technology as the mismatch between the **speed of edge innovation** (engineering) and the **capacity for central governance** (architecture).

> In my view, the major issue lies in attempting to govern after something is built and delivered. Conversely, trying to govern too far in advance often leads to excessive bureaucratic overhead.

The feeling that architecture is "always one step behind" happens primarily when companies adopt traditional, reactive architectural models.

**Why does Engineering usually bring innovations first?**

1. **Proximity to real problems:** Engineering teams feel daily pain points directly in code, infrastructure, and CI/CD pipelines. When a new tool, framework, or cloud service emerges to solve that exact pain point, engineering is the first to test and adopt it.
2. **Pressure for speed:** Under pressure to deliver faster, engineering seeks technological shortcuts.
3. **Volume and specialization:** It is mathematically impossible for a central architecture team to keep up with every library, tool, or trend across dozens of ecosystems at the same pace as hundreds of engineers.

If architecture tries to act as a **"Tollbooth"** (where nothing passes without prior architect approval), it becomes a bottleneck. Engineering bypasses it, adopting tools independently (sometimes creating dangerous *Shadow IT*), and architecture only finds out once an issue hits production.


### Architecture's Role: Being Ahead Does Not Mean Knowing Everything First

Being "ahead" of engineering does not mean architects must discover every market tool before engineers do. Leading the process requires changing how standards are created:

1. Define Guardrails (Tracks), Not Concrete Walls

Instead of dictating the exact tool (*"you can only use Database X on version Y"*), architecture defines **eligibility criteria**:

- *"Any new technology brought by engineering must support observability, integrate with corporate SSO, be compatible with the CI/CD pipeline, and include a cost analysis."*
- This gives engineering the autonomy to innovate within pre-established safe boundaries.

2. Evolutionary Architecture and "Paved Roads"

Architecture establishes the default path ("the paved road") where everything is automated, documented, and easy to use.

3. Enablement, Not Enforcement

Architecture acts proactively by identifying **structural business trends** (e.g., cloud migration, data strategy, regulatory resilience, FinOps/cost management) while engineering focuses on **tactical product innovation**.

**The Difference Between Reactive and Proactive Architecture**

| Model | Reactive Architecture (One step behind) | Proactive Architecture (Ahead of the business) |
| --- | --- | --- |
| **Action** | Discovers innovations when issues explode in production. | Establishes clear adoption criteria and policies before choices are made. |
| **Position** | Acts as a compliance officer and "request approver." | Acts as a technical advisor and standards curator. |
| **Relationship** | Seen by Engineering as delivery-delaying bureaucracy. | Seen by Engineering as a partner that unblocks and protects systems. |
| **Focus** | Micro-managing every line of code or tool. | Designing long-term macro platform strategies. |


When architecture focuses on **defining strategic drivers, reference architectures, and security guardrails**, it stops getting overrun by engineering's technical pace and begins guiding it sustainably.

Proactive architecture does not start "making the steak" (since building features remains Engineering's core deliverable); rather, it **prepares the commercial kitchen, automates the grill, and readies the cuts** so Engineering can serve the steak 10 times faster without contamination risks. This reinforces how Architecture enables Engineering to deliver immediate value.

However, even when acting proactively, architecture cannot remain passive—meaning defining a standard and calling it done! That approach will continue to deliver zero business value.


### Reaching the Next Level

To achieve maturity and move beyond generic or purely operational models, **Proactive Technology Architecture** can be structured around key pillars. One crucial pillar I want to address is **Risk Management and Technical Resilience**.


**Evolutionary Architecture and Technical Debt Management**

Enterprise systems naturally degrade over time unless mechanisms exist to measure and manage technological obsolescence.

- **Fitness Functions:** Automated tests executed in the continuous integration pipeline to validate non-functional requirements and architectural rules. If a module attempts to query another service's database directly or a dependency violates coupling rules, the build breaks.
- **Obsolescence and Risk Matrix:** Continuous tracking of software components, libraries, and infrastructure services against their lifecycle (LTS status, community or vendor deprecation, CVE security vulnerabilities).
- **Refactoring Quota:** Institutional agreement between Architecture, Engineering, and Product Management to allocate a fixed percentage of development capacity (e.g., 15% to 20% of sprints) specifically toward technical debt reduction and core component upgrades.

---

## Architecture Maturity Matrix

| Dimension | Level 1: Passive / Reactive | Level 2: Standardizing / Normative | Level 3: Proactive / Enabler |
| --- | --- | --- | --- |
| **Technical Standards** | Documented in isolated PDFs or wikis. | Manually validated in architecture boards. | Automatically embedded in templates and CI/CD pipelines. |
| **Approval Bottlenecks** | Requires human review for any technical change. | Requires approval for new infrastructure components. | Automated *guardrails* grant full autonomy within boundaries. |
| **Cost Management** | Ad-hoc cloud bill review after payment. | Reactive cost-cutting when budgets are exceeded. | *Cost-Driven Architecture* with cost visibility right in code. |
| **Engineering Relationship** | Seen as a policing team that delays deliveries. | Seen as a advisory group consulted sporadically. | Platform provider accelerating team productivity. |


### What About Communication?

Communication in architecture is not about filling out forms, Excel spreadsheets, or making pretty presentations. It is about translating technical complexity into different contexts and languages.

> If you work in architecture and only make pretty presentations, watch out! That is not a good sign.

An architect who cannot communicate effectively falls into one of two extremes: either an "ivory tower architect" who is misunderstood and ignored, or a "bureaucratic cop" everyone tries to bypass.

Knowing how to communicate across all organizational levels is fundamental. Here are key examples:

- **With Engineering:** Speak the language of those in the code. Dictating rules in a 50-page PDF doesn't work; communication here must be pragmatic, grounded in transparent trade-offs, listening to team pain points, and turning guidelines into automation (the "ready kitchen" mentioned earlier).

- **With Product Management (POs/PMs):** Explain the impact of technical debt in terms of future velocity. Product wants "steak on the plate" today, but the architect must communicate clearly: "If we don't allocate 15% of the sprint to refactoring now, delivering new features next quarter will take twice as long." Creating [ADRs](https://brunorusso.com.br/posts/ADR-a-chave-para-documentacoes-ageis-e-eficientes-de-arquitetura/) has become common for this, but the problem is that ADRs often turn into just another form to fill out, losing their real value.

- **With Leadership and Business (C-Level/Execs):** Translate technical decisions into financial and risk terms. Executives don't need to know if a database is NoSQL or Relational; they need to know if the solution will scale during critical periods like Black Friday, comply with regulatory requirements (such as LGPD/GDPR), and understand the financial impact on the business.


### Brief Conclusion

Ultimately, technology is built by people, for people. Standards, paved roads, and risk matrices only create real impact when paired with active listening and pragmatism. When architecture stops being a bureaucratic tollbooth and becomes an enabler for engineering, the business gets the best of both worlds: the immediate speed the market demands paired with the technical sustainability the future requires.