# Software_Processes_Management
Notes 
# Week 2 Lecture Deep Dive — How the Lecturer Actually Explained It

> This is the companion to the condensed study guide. Where that guide gives you the facts, this gives you the *reasoning* — the analogies, worked examples, and pros/cons exactly as the lecturer walked through them in the recording, so you can reconstruct the argument yourself rather than just recalling a bullet point.

---

## 1. Process: defined vs empirical

The lecture opens by extending last week's definition of a process (a series of steps to reach a goal) into two flavours:

- **Defined process**: you can predict the output with high confidence because the same inputs, run through the same activities, reliably produce the same result. The analogy used is buying a burger at any McDonald's anywhere in the world — the steps (toast the bun, prepare the patty, arrange the toppings) are trained and repeatable across every store. Minor customisation doesn't break this; the underlying process is still rigidly defined.
- **Empirical process**: you "work with the unexpected." Instead of following fixed steps, you observe what's happening, infer from it, and make course corrections as you go. The analogy used is a commercial flight: pilots file a flight plan (typically the great-circle route) before takeoff, but if storm clouds appear mid-flight, they don't fly through the plan regardless — they adapt, going around the storm or diverting to a nearby airport. The lecturer's key caveat: because empirical processes are adaptive rather than fixed, your estimates under this model are only ever indicative, not precise — and that's fine, it's how Scrum is designed to work.

This distinction is the lens for the entire lecture: the formal SDLCs that follow (Waterfall, Incremental, Prototyping, Spiral) sit closer to the defined end of the spectrum, while Agile and Scrum sit closer to the empirical end.

A process model is described as a simplified, abstracted description of the steps needed to hit a goal — and the lecturer is explicit that having a good process model does *not* remove the need for good project management. They work together: even with a solid methodology, projects drift off track for other reasons, and management principles are what pull them back.

---

## 2. The student-assignment exercise (why "code and fix" still happens today)

The lecturer runs a simple flowchart: read the spec (optional) → code → check for errors → fix → test against the one example the lecturer supplied → submit. A class poll asks whether this process actually works — the majority answer "maybe," landing around 60%.

The reasoning he draws out: it depends on complexity. For something trivial (a first-year "Hello World"), testing against one example might genuinely be enough. For a real client project with complex, real-world requirements, one passing test case proves almost nothing — the submitted code is likely to fail on different inputs, may not match what was actually specified (because the spec wasn't read carefully, or a requirement was interpreted differently than intended), and may exhibit poor design from not following the brief properly.

This exercise exists to set up the next topic: this exact flow — code, fix until it passes, ship — is literally the oldest SDLC in software history.

---

## 3. Code and Fix (1940s–50s)

The process: write code, keep cleaning it up until it works, deliver it. It worked reasonably well at the time for a specific set of reasons:

- Systems were small by any modern standard
- The field was the domain of a narrow group of highly trained specialists (often advanced degrees in maths or engineering)
- The developer, client, stakeholder, and end user were frequently the same person — so there was little of the requirements misalignment that plagues projects today
- Programs were often run once and discarded — so there was little need for long-term maintenance, configuration management, or version control
- The actual workflow was physically slow: instructions went on punch cards, were submitted, and you might wait days to get back a list of errors before resubmitting a corrected deck. Interactive terminals later sped this cycle up, but the underlying ad hoc process didn't change.

The problem: working this way at any real scale produces systems that are hard to maintain, insecure, and not robust — illustrated with a few visual gags (a half-collapsed shed, a truck improvised with a trolley welded on, a bathroom layout with an obvious design flaw) that all share the same theme — a quick patch that technically functions but was clearly never planned properly.

---

## 4. The 1960s software crisis

As computers grew more powerful, the programs being asked of them grew more complex — and the user base widened from a small academic circle to businesses and their customers, whose requirements were far less simple. Working in the old ad hoc style against this new complexity produced a wave of failures: a large share of software projects shipped late or never shipped at all, blew their budgets, or simply didn't work — frequently more than one of these at once. The lecturer notes that even much more recent industry surveys still show roughly half of projects landing in a "challenged" category — the crisis reshaped the discipline, but the underlying pressures never fully disappeared.

---

## 5. The NATO conferences (1968–69)

This is where the term **software engineering** was coined for the first time. The famous framing from the era: *"we build systems like the Wright brothers built airplanes"* — build the whole thing, push it off a cliff, see if it crashes, and start again if it does. That's a direct description of Code and Fix failing at scale.

Attendees included some of the most prominent computer scientists of the time — Dijkstra, Hoare, Gill, Perlis, Naur. The lecturer also points out that the recognition of software engineering as a "real" engineering discipline (on par with civil or mechanical engineering) took decades — professional bodies like Engineers Australia only formally recognised it within the last twenty years or so.

---

## 6. Waterfall (Royce, 1970)

The name is literal — water flows in one direction, top to bottom. Phases: **Requirements → Analysis → Design → Implementation → Maintenance → Retirement**, with each phase producing a document that feeds the next:

- **Requirements**: sit with the client, hammer out exactly what the system needs to do, and get a physical sign-off
- **Analysis**: dig into the non-functional requirements (security, safety, etc.) and produce a robust Software Requirements Specification (SRS) — this becomes the main input to design
- **Design**: figure out how the system will actually be built — subsystems, and how they interact
- **Implementation**: code and integrate everything
- **Maintenance**: repair and enhance after release
- **Retirement**: end of life

Two bedrock principles hold this together: stability of requirements, and heavy emphasis on documentation, since each phase's output document is what makes the next phase possible. Formal documentation standards (e.g. IEEE) govern how much detail each of these documents needs.

The real problem, explained through a worked scenario: you've physically signed off requirements with the client. Later, an ambiguity or missed requirement turns up. Now you have to negotiate who pays for the fix — is it on the development team, or does the client pay extra for something missed at sign-off? If the fix takes an hour at a $200/hour billing rate, that's a genuinely awkward $2,000 conversation. The takeaway: change is *possible* in Waterfall, but the formal sign-off structure makes it expensive and adversarial to negotiate.

The more realistic version — **Waterfall with feedback** — adds loops back to earlier phases when an error surfaces. It's still a document-driven approach, so syncing documentation after a change remains costly. The point isn't that you can't go back; it's that going back always costs you.

---

## 7. Why move past Waterfall

Two reasons given, beyond cost-of-change:

- **"The customer is always right" is a myth.** Clients usually have a genuine vision but need professional expertise to translate that vision into something workable. The example given: a project collecting indigenous health data in rural Australia, where the client insisted on an iPad-based app — without accounting for the very limited connectivity in the rural areas the system actually had to operate in. The team had to push back and steer the solution toward something that would actually work. The broader point: fulfilling the literal letter of a signed-off requirement doesn't guarantee a happy client if their deeper need wasn't actually met — you can tick every contractual box and still lose the next contract.
- **You can't fully insulate a project from external change** — business conditions, regulatory environments, and the surrounding technology landscape (OS versions, libraries, network speeds) are outside both the developer's and the client's control.

---

## 8. Incremental SDLC

The core move: instead of a "Big Bang" (build everything, deliver once, six months later find out if it worked), slice the project into multiple manageable mini-waterfalls. Each release builds on the last — Release 1 might cover the first four major requirements, Release 2 adds the next set on top, and so on.

**Why it helps:**
- Risk of total project failure drops, because a problem in one increment doesn't sink the whole project
- The client sees and uses an operational product earlier, and that feedback shapes later increments
- Initial delivery is faster, simply because you're shipping a slice rather than the whole thing

**Where it bites back:**
- Deciding *how* to slice the requirements isn't trivial — on a genuinely complex project, dependencies between slices can be hard to untangle
- Each mini-waterfall is, underneath, still a waterfall — the same rigidity persists, just contained at a smaller, cheaper scale

---

## 9. Prototyping (Royce, 1970s)

Essentially Waterfall-with-feedback plus one extra step at the start: build a small prototype before committing to the full build. Its purpose is narrow and specific — de-risking the requirements phase by showing the client something tangible early, to confirm both sides actually understand the requirement the same way. The lecturer flags that requirements misalignment is *still* one of the leading causes of project failure today (pointing to the dedicated requirements engineering subject as evidence it remains a genuinely hard problem, not a solved one).

The catch at the time: in the 1970s, building prototypes was expensive given the technology available. Today's tooling makes this far cheaper and more varied — you can prototype a UI, an architecture, or performance characteristics independently. But a single prototype still might not be enough for a sufficiently complex project — and that limitation is exactly what motivated the Spiral model.

---

## 10. Rapid prototyping

An evolution of Prototyping into a tight cycle: build → get fast client feedback → refine → repeat. The prototype is a constrained, functional subset of the eventual product — enough to validate direction quickly. Once the team and client have converged through these cycles, the actual build proceeds using whichever full SDLC suits the rest of the project.

---

## 11. Spiral model (Boehm, 1986)

Historically popular in defence work, and still common today in heavily regulated domains — medical device development was the example given, where legal and regulatory obligations demand serious rigour. The analogy used is climbing a spiral staircase: each loop repeats the same four activities, but you're progressively further along, with an increasingly refined prototype each time.

**The four quadrants of each spiral, in order:**
1. **Plan** — decide what this particular spiral is trying to achieve (e.g. "plan the requirements for this spiral")
2. **Determine objectives, alternatives, constraints** — given that plan, what are the options, and what are the limits?
3. **Risk analysis** — assess the risk in those alternatives and constraints; if something significant turns up, address it with a targeted prototype
4. **Build and validate** — develop and validate the next-level prototype/engineering output

**Worked example**: an online food-ordering app. In the very first spiral, while nailing down the "concept of operation" (how will users actually interact with the system?), the team realises there's a real risk in not knowing whether users will search by restaurant, by food type, or some hybrid — get that UX wrong and the product could fail outright. Rather than guessing, they build a targeted prototype specifically to resolve that one risk before moving on. Not every spiral needs a prototype — only when a risk is genuinely too uncertain to resolve any other way.

Each spiral produces a progressively more refined prototype until an operational prototype is reached and can be released — comparable to a release in the Incremental model. The lecturer explicitly frames Spiral as a direct precursor to Agile's iterative, risk-managed mindset: later Agile models borrow heavily from these same principles.

---

## 12. The Agile family (2001)

Seventeen software engineers, each already running their own preferred lightweight alternative to the formal models, met at a resort in Snowbird, Utah, sharing one common goal: reduce the rigid documentation burden of formal SDLCs. The result was the **Agile Manifesto** — not a single process, but a shared set of values.

The manifesto's own framing is explicit and important: while there is value in the items on the right (process and tools, comprehensive documentation, contract negotiation, following a plan), the manifesto argues for valuing the items on the left more (individuals and interactions, working software, customer collaboration, responding to change). It is **not** a call to eliminate the items on the right.

The lecturer flags this directly as a persistent misconception — that "agile" is often wrongly taken to mean "no documentation," and that plenty of student teams still operate under that mistaken belief today. Agile is not Code and Fix with better branding.

---

## 13. The Nordstrom video — Agile in practice

The lecture includes a real filmed example: an innovation team builds an iPad app (letting customers compare sunglasses side by side) in a single week, working inside an actual Nordstrom store with real shoppers.

The process shown: user story mapping → paper prototypes tested live with real customers → coding the single highest-priority feature first → same-day feedback loops, where a feature could be delivered and useful customer feedback collected within roughly ten minutes. A genuinely useful bug surfaced this way: a customer wearing polarised sunglasses held the iPad in portrait orientation and saw a completely black screen, because the screen's and the lenses' polarisation cancelled each other out — switching to landscape fixed it instantly. That's a clean real-world example of the empirical process in action: an unplannable problem, found only through observation, fixed through fast adaptation.

On the question of "when is it done," the team's own answer was that it depends entirely on how much time you have — the week was timeboxed, and they called it finished once it satisfied users and solved the main problems within that box.

The lecturer is explicit that this video shows one extreme end of the Agile spectrum, illustrative rather than prescriptive — and pointedly notes what's *missing* from it: no detailed upfront planning, no heavy documentation, no predefined handoffs between teams, all of which are hallmarks of the formal models covered earlier.

---

## 14. When *not* to go fully Agile — the pacemaker example

The test case offered: would you want a pacemaker manufacturer casually adding new features and asking you to sign off on the spot? Obviously not — legal, regulatory, and safety considerations rule that out.

The broader myth-bust here: students often assume you pick exactly one SDLC for an entire project based on a checklist of its requirements. In reality, most real projects are **hybrids** — safety-critical or heavily regulated components get built formally, while lower-risk, fast-changing components get built with Agile approaches, within the same project.

---

## 15. Agile process assumptions — when Agile genuinely fits

(Sourced from the requirements-engineering textbook referenced in the companion subject, SWEN90009.)

- The project is small enough for a single, co-located team
- Users and clients are available promptly — not "let's schedule a meeting next week to clarify this." The Nordstrom video pushed this to its limit, with literal real-time customer interviews.
- New or changing requirements are unlikely to need major rewrites — with a practical nuance added: a team can't realistically sell a client on a sprint that's purely refactoring with nothing new to show for it. Technical debt has to be paid down alongside value delivery, not pitched as a standalone activity.
- Safety- or mission-critical systems: again, "it depends" — frequently resolved with hybrid SDLCs rather than an all-or-nothing choice.

The key reframe offered: these assumptions aren't a strict yes/no checklist. Agility itself can be dialled up or down — it's not a binary choice between "fully formal" and "fully agile."

---

## 16. Kanban

Kanban didn't originate in software at all — it comes from Toyota's lean manufacturing system, and the word itself translates to billboard or signboard. Lean thinking, in this context, means focusing development effort on whatever drives the most value for the client first, deferring lower-value work. The physical board — backlog, to-do, in-progress, done, with sticky notes moving across swim lanes — gives anyone a snapshot of exactly where the project stands at any given moment. The overall goal is maximising flow efficiency: minimising the time between starting something and finishing it.

---

## 17. Scrum

The term itself dates to 1986, but the framework was formalised when Sutherland and Schwaber presented their paper at a 1995 conference. The core mechanic is the timeboxed sprint, typically two to four weeks (three weeks being most common): a product vision is decomposed into user stories, collected into a product backlog, and the Product Owner selects the highest-value items for the upcoming sprint.

The daily stand-up — fifteen to thirty minutes, covering what you did yesterday, what you're doing today, and any blockers — gets its name because attendees genuinely stay standing, which keeps the meeting short by design. Each sprint ends with a potentially shippable increment, and the cycle repeats.

A class poll asked whether "Agile" and "Scrum" can be used interchangeably — 71% answered "depends on the project." The lecturer's resolution: in an organisation that standardises every single project on Scrum, the two terms become practically interchangeable in that context. But strictly speaking, Agile is the broader mindset and value set, while Scrum is just one specific implementation of it (alongside Kanban, XP, and others) — so in any organisation mixing methodologies across projects, treating the two terms as synonyms creates real ambiguity about which specific framework is actually being discussed.

The risk-management angle: because Scrum reviews and adjusts every two to four weeks, problems surface early and get addressed proactively — rather than discovering six or eight months in that the whole project has quietly become "challenged."

---

## 18. Extreme Programming (XP)

Kent Beck, late 1990s. Shares Scrum's spirit of frequent releases in short cycles, but does not formalise a fixed-length timebox the way Scrum's sprints do — it has its own defined checkpoints for introducing customer-driven change instead. Pair programming is the practice most associated with XP: two people work on the same task together, one typing while the other actively reviews and checks that good practice is being followed — still common in industry today.

---

## 19. Scrum's foundations — tying back to the start of the lecture

Scrum is explicitly built on empiricism (observe, infer, adapt — the exact definition given at the very start of the lecture) combined with lean thinking (deliver the highest-value items first, the same underlying principle as Kanban). The Product Owner is the mechanism that resolves "which of my hundred requirements actually matters right now?" — setting sprint direction based on stakeholder priority. New, higher-value requirements that surface mid-sprint don't derail the current sprint; the Product Owner captures and prioritises them into the *next* sprint instead.

---

## 20. The three pillars, with the lecturer's own examples

- **Transparency**: the example given is a student team member who, stuck on a genuinely difficult feature, keeps reporting "almost there" at every daily stand-up for two weeks — when in reality they're blocked and need help. Hiding the struggle (instead of being transparent about it) creates a ripple effect that hits the whole team near the deadline. Transparency is what actually allows a Scrum Master to do their job, since protecting and supporting the team only works if the team's real state is visible.
- **Inspection**: goals need to be checked frequently, through the sprint ceremonies (showcases/reviews, retrospectives), so blockers are caught early rather than at the very end.
- **Adaptation**: once inspection reveals you're off track, the framework needs to let you course-correct immediately — that flexibility is the entire point of the model.

---

## 21. Definition of Done — sharper than it looks on the slide

The anecdote given: you ask a teammate whether they've finished a requirement, and they say "almost done" — but for them, that often just means the *coding* is finished, not that edge cases or boundary conditions have actually been handled, tested, or reviewed. The Definition of Done exists precisely to remove that ambiguity: one uniform, binary standard the whole team agrees on, so a requirement is either met or it isn't — no grey areas.

---

## 22. Product Owner and Scrum Master — why each role exists, not just what they do

- **Product Owner**: acts as a proxy for stakeholders and end users who often aren't available on demand. Since a team needs fast answers to requirement questions mid-sprint (waiting days isn't an option), the Product Owner is the always-reachable point of contact who owns the backlog, decides what delivers the most value, and ultimately accepts or rejects the sprint's output on the stakeholders' behalf.
- **Scrum Master**: framed explicitly as a *servant leader* — their job is removing impediments (getting a struggling teammate extra help, training, or resources), fostering good communication, and shielding the team from external noise so they can actually focus on delivering.

---

## 23. PayPal case study — the full narrative

PayPal, acquired by eBay in 2002, was a payments industry leader that scaled rapidly to thousands of employees. What went wrong: heavy bureaucracy, a highly centralised structure with little decision-making autonomy at team level, formal/waterfall-style processes, and very long integration cycles — releases only landing a few times a year. The organisation simply couldn't keep pace with how quickly the market and customer expectations were moving. The resulting frustration showed up everywhere: developers facing delayed results and no autonomy, and customers visibly seeing the product fall behind the rest of the industry.

The fix was a deliberate **Big Bang approach** — explicitly against normal industry wisdom, which usually favours a phased rollout for change this disruptive. PayPal adopted Agile across the *entire* organisation simultaneously, not as a pilot in one or two teams. The scale: roughly 300–350 Scrum teams, using Large Scale Scrum (LeSS), one of several "agile at scale" frameworks. (The lecturer flags that SAFe — a more widely used industry framework today — gets its own dedicated lecture later in the unit.) The transformation is broadly considered a success: faster feature rollout and a visibly happier customer base.

Why this case study matters beyond the history lesson: it's the direct bridge from the small-team Scrum you'll practice all semester (around 7–10 people) to the reality that real industry projects often run 50–100+ people across many teams — exactly the problem the later scaled-Agile lecture addresses.

---