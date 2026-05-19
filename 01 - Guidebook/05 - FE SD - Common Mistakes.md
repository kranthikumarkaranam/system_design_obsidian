#source/greatfrontend #guide

Source: [Common Mistakes to Avoid for Front End System Design Interviews](https://www.greatfrontend.com/front-end-system-design-playbook/common-mistakes)
Back to: [[FE SD - MOC]] 


> 💡 Unlike coding interviews, it is much harder to practice and simulate FE system design interview conditions. These mistakes are common precisely because candidates don't realize they're making them.

---

## ❌ Mistake 1 — Answering the wrong question

**What happens:** Diving into a solution immediately without scoping the problem. The candidate produces a polished answer for a product the interviewer never had in mind.

**Why it hurts:** System design prompts are deliberately under-specified. Answering the wrong question well is worse than answering the right question poorly. This is one of the fastest ways to fail the round.

**Fix:** Always start with [[03 - RADIO Framework]] → Requirements. Ask clarifying questions to determine exactly what product/feature is being designed before drawing a single component. See [[04 - FE SD - Evaluation Axes]] → Problem Exploration.

---

## ❌ Mistake 2 — Approaching the question in an unstructured manner

**What happens:** The candidate goes all over the place — jumping between topics, revisiting areas without signalling, and missing entire RADIO sections by the end.

**Why it hurts:** System design interviews are open-ended. Without an explicit structure, candidates appear disorganised and interviewers can't track where they are in the answer.

**Fix:** Write down each step of the [[03 - RADIO Framework]] on the whiteboard at the start of the interview. Work through sections visibly. You don't have to follow the order strictly, but ensure every section is covered before the end. Revisit earlier sections explicitly if needed.

---

## ❌ Mistake 3 — Insisting on only one solution or the best solution

**What happens:** The candidate presents one solution and treats it as the only correct answer, even when the interviewer explicitly prompts for alternatives.

**Why it hurts:** The interviewer wants to see you identify a solution with the right tradeoffs, not prove there is a single right answer. Every solution has tradeoffs — refusing to acknowledge them signals shallow thinking.

**Fix:** Offer two or three approaches. Explain the pros and cons of each. Make a recommendation with reasoning. Even if alternative solutions are obviously worse, name them and briefly explain why they are bad. See [[04 - FE SD - Evaluation Axes]] → Exploration and Tradeoffs.

---

## ❌ Mistake 4 — Remaining silent the entire time

**What happens:** The candidate thinks privately and only speaks when they have a fully-formed answer. Long silences dominate the session.

**Why it hurts:** System design interviews are collaborative exercises between you and the interviewer. Silence prevents the interviewer from seeing your reasoning process, which is most of what they're evaluating.

**Fix:** Think out loud. Treat the interviewer as a coworker. Surface issues as you identify them, float half-formed ideas, bounce solutions off them, and ask for their input on tradeoffs. See [[04 - FE SD - Evaluation Axes]] → Communication and Collaboration.

---

## ❌ Mistake 5 — Going down a rabbit hole

**What happens:** The candidate dives too deep into one specific component (e.g. the exact debouncing implementation for search) and runs out of time before covering the overall architecture or other critical sections.

**Why it hurts:** An unimportant component getting 15 minutes of detail provides few useful signals. The interviewer needs breadth first — high-level architecture across all [[03 - RADIO Framework]] sections — before depth on any one part.

**Fix:** Define the initial architecture first. Then ask the interviewer explicitly if they want you to dive deeper into a specific component before doing so. Focus depth on the parts most important to the problem. See [[Performance Optimization]], [[Accessibility (A11y)]] for deep-dive topics that commonly matter.

---

## ❌ Mistake 6 — Using buzzwords without being able to explain them

**What happens:** The candidate drops technical terms like "Virtual DOM", "DOM Reconciliation", "Partial Hydration", or "Streaming Server-side Rendering" but cannot explain what they mean or why they're relevant when probed.

**Why it hurts:** Interviewers routinely probe buzzwords to test depth. Being unable to explain a term after using it is a clear signal of surface-level knowledge and is harder to recover from than simply not mentioning the term.

**Fix:** Only use a term if you can define it precisely and explain why it is relevant to the current question. If you're not sure whether a term applies, describe the concept in plain language instead. See [[Rendering Strategies]], [[Networking & APIs]], [[Performance Optimization]] for concepts worth knowing deeply.

> 💡 Never drop a term you can't defend under follow-up questioning. "Partial Hydration" said with confidence and then fumbled when probed is worse than not mentioning it at all.