---
name: craft-check
description: Review a change against the "craft over claims" principle - users judge quality from using the product, not from what it says about itself. Use when reviewing a diff, PR, feature or UI change for real product quality - whether effort lands on surfaces people touch, whether copy brags instead of informs, whether invisible work (correctness, cancellation, layout stability, safe errors) is present, and whether the feature is actually finished rather than just rendered.
---

# craft check

audit the work in scope against one principle: **craft over claims.**

users decide whether a product is good after they use it, never from what it says about itself. so the effort goes into the experience, not into describing the experience.

## scope

- if the user named a change, file, feature or pr, review that.
- otherwise, review the current diff (staged and unstaged changes, or the branch against its base).
- read enough of the surrounding code to judge the local standard - a change is measured against its neighbours, not in isolation.

cite `file:line` for every point. point at code, not vibes.

## the five checks

### 1. the experience is the argument

does the effort land on the surfaces people actually touch - the form, the checkout, the dashboard, the search, the onboarding flow - rather than on surfaces that only describe them?

flag polish spent on copy, marketing or landing pages while the underlying interaction is slower, flakier or unverified.

### 2. no self-praise in the product

scan ui strings, landing and marketing copy, empty states and error messages for adjectives that assert quality instead of informing: *premium, seamless, world-class, blazing fast, effortless, best-in-class, quality.*

for each one, propose a plainer, informative replacement, or a cut. behind every adjective is a mechanism - suggest showing the mechanism instead (e.g. "seamless checkout" → make it one step, and say what the step does).

### 3. invisible work is present

confirm the correctness and polish a user feels but never sees. look for what applies to the change:

- **data correctness** - totals, counts, stock or balances that stay right under retries and concurrent use.
- **idempotent writes** - payments, orders and submissions that can't double-fire on a double-tap or a retry.
- **cancellation** - in-flight requests aborted when the user navigates away or the input changes (e.g. `AbortController` / `AbortSignal`, or the framework's equivalent).
- **layout stability** - skeletons or reserved space that match the real layout, so content doesn't jump as it loads.
- **resilience** - slow and flaky networks, offline, timeouts; forms that keep the user's input when something fails.
- **safe errors** - messages that help the user and don't leak stack traces, ids or internals.

flag anywhere the happy path renders but these are missing.

### 4. details match the surrounding craft

new surfaces should hold the same bar as their neighbours. check for:

- the same design tokens, spacing and components the rest of the codebase uses - no one-off values.
- accessibility at the local standard - labels and hints, focus states, contrast, a reduced-motion fallback for animation.
- consistent tone in copy.
- no leaked internals - debug text, raw keys, placeholder content.

flag anything that lowers the local standard.

### 5. finished, not just rendered

is the experience actually right and verified, or only announced? look at the edges:

- empty, loading and error states.
- slow network and failure paths.
- unexpected input and the person using it "wrong".
- tests or verification that cover more than the happy path.

flag features shipped on the happy path alone.

## calibrate to the category

"good" is segmented. an internal tool wins on speed and clarity, a consumer app on delight, anything touching money or personal data on trust and correctness. weigh the checks for the kind of product in front of you, and say which lens you used.

## report

report each check in order with its findings and `file:line` references. if a check doesn't apply to the change, say so in one line rather than inventing findings.

end with a short verdict:

- **does this change let the product speak for itself?** yes, or not yet.
- **the top one or two fixes**, if not - the ones a user would feel first.

keep it concrete and short. no praise padding, no generic advice.
