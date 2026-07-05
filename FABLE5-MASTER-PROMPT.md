# Fable 5 Master Prompt — "Hum Banaye Kal" Platform

> Paste everything below the line into a fresh Claude Fable 5 session (effort: high) in this repository.
> Expected first response: a proposed phase plan and a stop for your approval — not code.

---

I'm building an EdTech SaaS platform for Pakistani school students (Class 1–10), their teachers, and their parents. The goal is a generation of deep thinkers and builders, not surface learners: AI as a gym that strengthens minds, not a crutch that weakens them. The core principle is **Productive Struggle — the AI never gives answers, only guides students to discover them.** Tagline: "Hum Banaye Kal" (We Build Tomorrow). With that in mind: build this platform end to end, in phases, as specified below.

## The vision

**1. AI Tutoring Engine — "Never Answer, Only Guide."** The heart of the system refuses to output direct answers. Roles: Socratic Questioner (asked "what is 6×7?", it responds with a counting-bags-of-marbles breakdown, never "42"); Incremental Hint Bot (3 hint levels — conceptual nudge → partial strategy → worked example of a *similar* problem, never the exact one; each hint unlocked only after the student attempts a step); Misconception Detector (wrong attempt → "you subtracted here — why that operation? what if we added?" — builds error analysis, never just "wrong"); "Explain It to Me" mode (student teaches the concept to an AI "younger student" character that pokes holes in weak explanations); Anti-Plagiarism Shield (detects pasted LLM-generated answers, discards them, restarts the student's own reasoning, may require step-by-step whiteboard input).

**2. Focus Subject specialization (Class 1–10).** Parents + teachers pick 1–2 focus subjects per child as early as Class 1. The system builds a 10-year spiraling curriculum using that subject as the lens for all learning. Example, Aerospace: Class 1–2 counting stars and nose-cone shapes; Class 3–5 fuel-calculation multiplication and water rockets; Class 6–8 thrust algebra, orbit simulations in Scratch, Muslim astronomer history in Islamiyat; Class 9–10 trajectory calculus, Python moon-landing simulations, model-rocket capstone with real altimeter. Focus can change, but by Class 10 the child is a young specialist with a project portfolio.

**3. Three dashboards.** Student "Mission Control": weekly quests, struggle metrics (celebrating time on hard problems, not just correctness), buildable portfolio, "My Lab" for projects/simulations/experiments. Teacher: disengagement and cheating signals (excessive hint-unlocking without attempts), custom struggle tasks, conceptual gap monitoring, AI-suggested peer-teaching groups. Parent: "Growth Tree" visualizing depth not grades, weekly snapshots ("45 productive struggle minutes on a physics simulation — showed resilience"), real-world connection suggestions without interfering in learning.

**4. Subject sandboxes.** Math: digital canvas — bar models, strips, dragging numbers; AI corrects the *process*, not the final answer. Programming: built-in IDE where the AI never writes code — it prompts for the next keyword, checks lines, and generates failing test cases that force debugging. Physics/Chemistry: virtual lab benches — short circuits fizzle, wrong chemical mixes cause harmless virtual explosions that prompt safety research. Biology: virtual dissections and ecosystems with population chain reactions and food-web reasoning. Islamiyat: interactive text analysis connecting Quranic verses to modern science (mountains as pegs → geological mountain roots), Hadith-based ethical debate with AI challenging the reasoning — critical thinking over rote memorization. Self-Development: scenario games for honesty, patience, teamwork — moral dilemmas explored through Socratic dialogue, character growth tracked by reasoning depth.

**5. Gamification rewarding grit, not genius.** Struggle Points for persistence, retrying after failure, and "aha" moments — they unlock cosmetics (avatar gear, rocket skins), never easier paths. Creator Badges for building projects, original code, experiments, peer teaching. "Pakistan's Future Innovators League": national inter-school monthly challenges with winning projects showcased to Pakistani tech companies.

**6. Term capstones.** Every term, an interdisciplinary practical project: early classes grow a plant measured with a handmade ruler; middle classes build a motor and connect it to magnetic-field theory; senior classes design a small business, code its profit calculator, and relate Islamiyat fair-trade ethics. "Dream Lab" module for student project proposals; approved ones earn hardware kits.

**7. "PhD mindset by Class 10."** Progressive training in Socratic inquiry, source evaluation ("how do you know? find a reliable source"), hypothesis-before-experiment prediction, and communication (2-minute project videos with AI clarity feedback). Each student maintains a Learning Journal that reads like a young researcher's notebook — a university-admissions portfolio.

**8. Technical moat.** Tutoring dialogue tuned for productive struggle on Pakistani curriculum with Urdu/English code-switching. Cognitive Load Tracker: hesitation, hint-request, and interaction patterns detect a student about to quit, triggering difficulty adjustment or encouragement. Parental "Future Compass" questionnaire seeds the focus subject.

**9. Teachers empowered, not replaced.** AI co-pilot generates struggle-based lesson plans, Socratic question sequences, and virtual lab setups from a stated objective. Struggle Heatmaps show class-wide conceptual friction. Built-in teacher professional development for inquiry-based facilitation.

**10. National dream.** "Made in Pakistan" hero stories woven into tutoring (Dr. Abdus Salam asked a question just like yours). Annual student-made tech showcase with internships and a Future Innovators Fund.

**11. Depth over surface.** Students must not live on the surface — they must live in the deep ocean of their subjects. Every design decision bends toward depth.

## Hard constraints

- **Stack:** Next.js web app (App Router), deployed by the user via GitHub to Vercel. Database is SQLite: a local SQLite file in development, and Turso (libSQL — SQLite-compatible) in production, because Vercel's serverless filesystem is ephemeral and a plain SQLite file will not persist there. Use one query layer (e.g. Drizzle with the libSQL driver) so dev and prod share the same schema and code. Auth implemented in-app (e.g. NextAuth/Auth.js with the same database). Do not use Supabase or Lovable anywhere.
- **Runtime tutor LLM:** a multi-provider gateway, not a single hardcoded vendor. Support OpenRouter, Moonshot/Kimi, Anthropic Claude, and any OpenAI-compatible endpoint. Model choice configurable per feature (cheap fast model for high-volume tutoring turns, stronger model for misconception analysis and lesson-plan generation). Provider keys via environment variables.
- **Never-answer is a product invariant, enforced server-side.** The guarantee that the tutor never leaks a direct answer must live in the backend (system-prompt construction, response filtering, hint-ladder state machine), never only in a client-side prompt a student could bypass.
- **Bilingual:** Urdu/English code-switching support in tutor dialogue and UI from the start.
- **This repo has a handoff system.** Read `AGENTS.md` first. Fill in the `docs/` scaffold (01-overview through 08-tasks) as part of Phase 0, and keep `docs/06-status.md` and `docs/07-decisions.md` current as you work.
- **Git:** commit at the end of each phase to the existing remote (branch `main`).

## Phase protocol

**Phase 0 first, nothing else:** read `AGENTS.md` and the repo, then propose a complete phase plan — build order, scope of each phase, what each phase delivers, and how each phase will be verified. Recommend the order you believe is right and say why. Fill in the `docs/` scaffold with the architecture and data model your plan implies. Then stop and wait for my approval of the phase plan.

**Every phase after approval:** build it, verify it, report it, and wait for my explicit approval before starting the next phase. Do not start the next phase on your own.

When you have enough information to act, act. Do not re-derive facts already established in the conversation, re-litigate a decision the user has already made, or narrate options you will not pursue in user-facing messages. If you are weighing a choice, give a recommendation, not an exhaustive survey. This does not apply to thinking blocks.

Don't add features, refactor, or introduce abstractions beyond what the task requires. A bug fix doesn't need surrounding cleanup and a one-shot operation usually doesn't need a helper. Don't design for hypothetical future requirements: do the simplest thing that works well. Avoid premature abstraction and half-finished implementations. Don't add error handling, fallbacks, or validation for scenarios that cannot happen. Trust internal code and framework guarantees. Only validate at system boundaries (user input, external APIs). Don't use feature flags or backwards-compatibility shims when you can just change the code.

Pause for the user only when the work genuinely requires them: a destructive or irreversible action, a real scope change, input that only they can provide — or the end of a phase, which always requires approval. If you hit one of these, ask and end the turn, rather than ending on a promise.

Before reporting progress, audit each claim against a tool result from this session. Only report work you can point to evidence for; if something is not yet verified, say so explicitly. Report outcomes faithfully: if tests fail, say so with the output; if a step was skipped, say that; when something is done and verified, state it plainly without hedging.

Establish a method for checking your own work as you build. At the end of every phase, verify your work with fresh-context subagents against the phase's stated deliverables before reporting it complete. Pay special attention to the never-answer invariant: every phase that touches the tutor must include an adversarial check that direct answers cannot be extracted.

Delegate independent subtasks to subagents and keep working while they run. Intervene if a subagent goes off track or is missing relevant context.

## End-of-phase reports

Terse shorthand is fine between tool calls (that's you thinking out loud, and brevity there is good). Your final summary is different: it's for a reader who didn't see any of that.

If you've been working for a while without the user watching (overnight, across many tool calls, since they last spoke), your final message is their first look at any of it. Write it as a re-grounding, not a continuation of your working thread: the outcome first, then the one or two things you need from them, each explained as if new. The vocabulary you built up while working is yours, not theirs; leave it behind unless you re-introduce it.

When you write the summary at the end, drop the working shorthand. Write complete sentences. Spell out terms. Don't use arrow chains, hyphen-stacked compounds, or labels you made up earlier. When you mention files, commits, flags, or other identifiers, give each one its own plain-language clause. Open with the outcome: one sentence on what happened or what you found. Then the supporting detail. If you have to choose between short and clear, choose clear.

Begin with Phase 0 now.
