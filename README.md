# craft-check

an agent skill that reviews your changes against one principle: **craft over claims.**

users judge quality from using your product, not from what it says about itself. `craft-check` audits a diff, pr or feature for whether the work actually shows up in the experience, and points at code, not vibes.

## install

```bash
npx skills add mayeedwin/craft-check
```

works with any agent the [skills cli](https://github.com/vercel-labs/skills) supports, like claude code, cursor and others.

## use

ask your agent for a craft check on the current diff, or on something specific:

```text
run a craft check on this change
```

```text
craft check the new checkout flow
```

## what it checks

1. **the experience is the argument** - effort lands on surfaces people touch, not on copy describing them.
2. **no self-praise in the product** - flags "seamless", "premium", "blazing fast" and friends, and suggests plainer copy or the mechanism to show instead.
3. **invisible work is present** - data correctness, idempotent writes, request cancellation, layout stability, resilience, safe errors.
4. **details match the surrounding craft** - tokens, accessibility, tone and polish at the same bar as the neighbouring code.
5. **finished, not just rendered** - empty, loading, error and slow-network states, not just the happy path.

it ends with a short verdict: does the change let the product speak for itself, and the top one or two fixes if not.

## why

the thinking behind it:

- [you can't market your way to quality](https://maye.pwafire.org/reads/you-cannot-market-your-way-to-quality/)
- [the web is the product, not the pitch](https://maye.pwafire.org/reads/the-web-is-the-product-not-the-pitch/)

## license

[mit](LICENSE)
