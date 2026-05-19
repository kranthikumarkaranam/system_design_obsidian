#source/greatfrontend #guide

Source: [Evaluation Criteria for Front End System Design Interviews](https://www.greatfrontend.com/front-end-system-design-playbook/evaluation-axes)
Back to: [[FE SD - MOC]] 

> 💡 The more detailed and mature the answers, the higher the likelhood of a "hire" recommendation. Interviewers look for signals displayed by candidates before making an overall hiring decision.

---

## 1. Problem Exploration

- Demonstrated thorough understanding of the problem.
- Explored the requirements sufficiently by asking relevant clarifying questions to remove ambiguities.
- Gathered functional and non-functional requirements of the problem.
- Defined the scope of the problem.
- Identified the important aspects of the problem to focus on and address.

**Relevant framework sections:** Requirements exploration

---

## 2. Architecture

- Designed an architecture that solved the entire problem sufficiently.
- Broke down the problem into smaller independent parts of suitable granularity.
- Identified components of the system and defined their responsibilities clearly.
- Identified how these components will work together and defined/described the API between these components.
- Developed an architecture that can be put into practice.
- Developed an architecture with scalability and reusability in mind, one that can be extended to support future requirements.

**Relevant framework sections:** Architecture/High-level design, Data model, Interface definition

---

## 3. Technical Proficiency

- Demonstrated technical knowledge and proficiency of front end fundamentals, common technologies and APIs.
- Dived into specific front end domain areas where relevant to the problem.
- Identified areas that need to be paid special attention to and addressed them by proposing solutions and analyzing their tradeoffs.

Front end domain areas include: [[Performance Optimization]], [[Networking & APIs]], HTML/CSS, [[Accessibility (A11y)]], [[Internationalization (i18n)]], Security, Scalability, etc.

**Relevant framework sections:** Architecture / High-level design, Optimizations and deep dive

---

## 4. Exploration and Tradeoffs

- Offered various possible solutions to the problems at hand and explained the pros and cons of each solution.
- While solving the given question, there would be smaller problems to solve/questions to answer and each small problem/question can have various solutions and choices to make.
- Explained the suitability of the solutions given the context and requirements and provided recommendations for the context of the question.
- Do not insist there is only one possible solution. Good questions usually have a few possible solutions where the suitability of each depends on the context.
- Even if other solutions are clearly and obviously bad, still mention them and briefly explain why they are bad.

> 💡 Show the alternatives you rejected, not just the one you picked. Naming two or three options and articulating why the chosen one fits the context is a stronger leading signal than arriving at the same answer blindly. Dismissing obvious non-starters out loud still counts as tradeoff reasoning.

**Relevant framework sections:** Requirements exploration, Data model, Interface definition, Optimizations and deep dive

---

## 5. Product and UX Sense

- Proposed a robust solution that has the foundation of a good product.
- Considered user experience when answering: loading states, performance (perceived or actual), mobile-friendliness, keyboard-friendliness, etc.
- Considered error cases and suggested ways to handle them.

**Relevant framework sections:** Optimizations and deep dive

---

## 6. Communication and Collaboration

- Conveyed their thoughts and ideas clearly and concisely.
- Explained their complete solution with ease.
- Engaged the interviewer during the session, asked good questions and sought opinions when necessary.
- Was open to feedback from the interviewer and incorporated the feedback to refine their solutions.
- Treated the session as collaborative — not a solo exercise.

**Relevant framework sections:** Architecture / High-level design, Data model, Interface definition, Optimizations and deep dive


---

## Summary

Here's a table summarizing how the evaluation axes can be mapped to the various sections of the **RADIO framework**: Requirements Exploration, Architecture/High-level Design, Data Model, Interface Definition, Optimizations and Deep Dive.

| Axis                            | R   | A   | D   | I   | O   |
| ------------------------------- | --- | --- | --- | --- | --- |
| Problem exploration             | ✅   | -   | -   | -   | -   |
| Architecture                    | -   | ✅   | ✅   | ✅   | -   |
| Technical proficiency           | -   | ✅   | -   | -   | ✅   |
| Exploration and tradeoffs       | -   | ✅   | ✅   | ✅   | ✅   |
| Product and UX sense            | -   | -   | -   | -   | ✅   |
| Communication and collaboration | ✅   | ✅   | ✅   | ✅   | ✅   |
