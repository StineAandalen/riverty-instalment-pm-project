# A/B Experiment Brief, Riverty business-unit case

## Parameters
| Parameter | Decision |
|---|---|
| Feature under test | Why we ask |
| Persona | Consumers |
| Expected outcome | The user enters a super transparent portal. She would easily understand the documents that are requested. And she can easily understand how she can set up a plan that combine several cases that is affordable for the user. The European rollout gets proof. A pilot with evidence, guardrails and a clear stop condition makes extending to other markets and portfolios a decision backed by data, not a leap. SSR becomes a trustworthy north star. Reading it alongside the 60-day miss rate means a rising SSR reflects better outcomes. |
| Primary success metric | Uplift of the current SSR with launching a new feature or improve the current journey. The instalment is created in the portal with no agent contact ( 30 days before or after the setup of an instalment) and the consumer keep the instalment with no missing payments within 60 days. |
| Baseline rate | 31% Journey starters contacting an agent within 7 days |
| Guardrail metric | 60-day plan survival: no more than 19% of new agreements missing a payment within 60 days (baseline), so a higher completion rate can't come from plans people can't keep. |
| Guardrail boundary | Must not fall below 81%. Today, 19% miss a payment. No room below that baseline. |
| Second guardrail | · |
| Minimum Detectable Effect | 5% |
| Sample size per arm | 2796 |
| Traffic split | 50/50 |
| Test duration | 4 weeks |
| Significance threshold | 0,05 |

## Control vs. Variant
- **Control (A):** 31% of starters contact an agent within 7 days, roughly 2,600. The research themes say consumers don't know what's affordable, don't understand why income is requested, and fear the consequences of a wrong answer or missed payment. 28% of uploaded income documents need clarification or review.
- **Variant (B):** Screens to build (exactly 3) Screen 1: Entry point, "Start instalment request" Riverty header with logo placeholder. Page title: "Arrange an instalment plan". One-line context: "You received a payment reminder" with a synthetic case reference (for example DEMO-0001). Intro line: "We ask a few short questions. Under each one, we explain why." Primary button: "Continue". Screen 2: Feature core, "About your income" Up to three question blocks stacked on one screen (two when she selects "No income right now"). Each block has a label, a note and a control. Monthly net income: euro amount field. Income pattern: radio group with "Stays the same", "Changes (for example shift work)" and "No income right now". Proof of income (required): instruction line "Add your latest proof of income", then a mock file picker (filename held in state only). Shown only when she has not selected "No income right now". There is no skip option. Each note is a bordered panel directly under the label with a visible heading "Why we ask". Its body has three parts: why asked, how used, who can see it. A small "Draft wording" tag appears on every note in the prototype. Other elements on this screen: inline error text under each field a "Back" link a "Continue" button Draft note pattern (English gloss; the German final copy is written in week 1): "We ask this to show you instalments that fit your income. We use your answer only for [use: CONFIRM WITH DATA PROTECTION]. [Roles: CONFIRM WITH DATA PROTECTION] can see it." Screen 3: Success and confirmation, "We have your details" Check icon and title: "Thanks, we have your income details." Recap list showing each question, her answer and an "Edit" link. Document row with chip "Uploaded: [filename]". The row is omitted when she selected "No income right now". Next-step line: "Next, you'll see your instalment options." Primary button: "Continue to instalment options". This is a stub, and the prototype ends here. Functional requirement; Functional requirements

Each requirement is a rule, followed by how it is verified and the must-have it comes from.

FR1: Every question has a note. Every income, affordability and document question the journey shows must display a note. That is 3 questions, or 2 when she selects "No income right now". Verified by an automated check that finds 0 question IDs without a copy entry. Source: Must have 1 and 2.

FR2: Notes are short and complete. Each note must have 40 words or fewer and at most 2 sentences. It must cover why the question is asked, how the answer is used and who can see it. Verified by a lint on the copy file. Source: Must have 2 and 3.

FR3: Notes use plain language. No sentence in a note may be longer than 20 words, and no note may use a term from the jargon list agreed with legal. Verified by a lint on the copy file. Source: Must have 4.

FR4: The "who can see it" statement is confirmed. 100% of notes must contain a "who can see it" statement, and it must come from the confirmed-facts table, not be written freely. Verified by checking that every copy entry links to a fact ID. Source: Must have 3.

FR5: Notes are visible by default and readable on a phone. Notes must be visible on load with no tap or hover, and they must sit directly under the question label. At a 360 px viewport there must be no horizontal scroll, body text must be at least 14 px, and text contrast must be at least 4.5:1. Verified by a visual check at 360 px and a contrast check. Source: Must have 5.

FR6: Copy is fixed. Note text must be stored as fixed text in one file, keyed by question ID, with no runtime generation. The text shown on screen must match the stored text exactly. Verified by an automated comparison that must match 100%. Source: Must have 4.

FR7: Unapproved wording cannot be released. Every copy entry must carry a version, an approver, a date and a status. Any entry whose status is not "approved" must block the release build. Verified by a build-gate test. Source: Must have 6.
- **Held constant (isolation check):** The consumers still not trust the why we ask statements and give up and call an agent

## Hypothesis
> I believe that Why we ask for Consumers will result in The user enters a super transparent portal. She would easily understand the documents that are requested. And she can easily understand how she can set up a plan that combine several cases that is affordable for the user. The European rollout gets proof. A pilot with evidence, guardrails and a clear stop condition makes extending to other markets and portfolios a decision backed by data, not a leap. SSR becomes a trustworthy north star. Reading it alongside the 60-day miss rate means a rising SSR reflects better outcomes., as measured by a 5% change in Uplift of the current SSR with launching a new feature or improve the current journey. The instalment is created in the portal with no agent contact ( 30 days before or after the setup of an instalment) and the consumer keep the instalment with no missing payments within 60 days. within 4 weeks. We will protect 60-day plan survival: no more than 19% of new agreements missing a payment within 60 days (baseline), so a higher completion rate can't come from plans people can't keep. throughout the test.

## Shipping criteria
> We will **ship** if Uplift of the current SSR with launching a new feature or improve the current journey. The instalment is created in the portal with no agent contact ( 30 days before or after the setup of an instalment) and the consumer keep the instalment with no missing payments within 60 days. improves by ≥ 5% at 0,05 and 60-day plan survival: no more than 19% of new agreements missing a payment within 60 days (baseline), so a higher completion rate can't come from plans people can't keep. does not reach Must not fall below 81%. Today, 19% miss a payment. No room below that baseline. after 4 weeks.
> We will **iterate** if direction is positive but lift is below the MDE.
> We will **kill** if the primary metric shows no improvement or moves negatively.
> The read date is fixed at the end of 4 weeks, no results reviewed before this date.
