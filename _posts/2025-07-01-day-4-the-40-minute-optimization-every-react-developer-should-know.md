---
title: "Day 4: The 40-Minute Optimization Every React Developer Should Know"
date: 2025-07-01 07:00:00 +0800
categories: [Build in Public, 7 day React Native Challenge]
tags: [buildinpublic, reactnative, performance, optimization, react]
image:
  path: /assets/img/posts/7Day-RN-Challenge/2025-07-01-Day4/rn-challenge-day-4.jpg
#   alt: A data visualization showing a chaotic data stream becoming clean and optimized.
---

After the hyper-productive session building the app's core features on [Day 3](/posts/day-3-of-7-day-challenge-real-time-data-charting-and-the-perils-of-force/), my focus shifted. In software development, there's a critical milestone you cross when the primary question is no longer "Does it work?" but rather, "Does it work *well*?".

This is the transition from building features to engineering robust products. Day 4 of my 7-day challenge was dedicated entirely to this principle: the unseen work of performance optimization.

### The Hidden Problem: The High Cost of Re-rendering

Our app's Markets screen displays a list of 100 coins, with prices updating in real-time via a WebSocket. It looks great and feels fast. So, what's the problem?

The issue lies in how React "sees" change. When a WebSocket message arrives with a new price for a single coin, our global store updates the `coins` array. Because this array is technically a new object, React tells our entire `MarketsScreen` to re-render.

Crucially, the `<FlatList>` component then tells **every single visible `PriceTicker` row** to re-render itself.

Even though only Bitcoin's price changed, we were paying the performance cost of re-rendering Dogecoin, Ethereum, and every other visible row. On a high-end device, this might go unnoticed. On an older phone, it could lead to a sluggish UI, dropped frames, and increased battery drain.

### Step 1: Proving the Problem (The "Before" State)

A senior engineer doesn't optimize based on feelings; they optimize based on data. To prove the issue, I added a single `console.log()` statement to my `PriceTicker` component to log a message every time it rendered.

The result was a constant flood of render logs, even when only one or two prices were changing per second.

<video width="800" autoplay loop muted playsinline>
  <source src="/assets/img/posts/7Day-RN-Challenge/2025-07-01-Day4/rn-day4-before-memoization.mp4" type="video/mp4">
  Before Optimization: Notice the constant stream of render logs in the terminal, even for coins whose prices are not changing.
</video>

### Step 2: The Solution - `React.memo`

The fix for this specific problem is an elegant and powerful tool provided by React itself: `React.memo`.

`React.memo` is a Higher-Order Component (HOC) that you wrap around your own component. It "memoizes" the component, remembering the props it received. Before re-rendering, `React.memo` performs a quick check: "Have any of these props actually changed since the last render?"

- If **yes** (e.g., Bitcoin's price prop is different), it re-renders the component.
- If **no** (e.g., Dogecoin's props are identical), it **skips the render entirely.**

Implementing this was a simple, one-line change in `PriceTicker.tsx`:

```javascript
// Before
// export default PriceTicker;

// After
import React from 'react'; // Make sure React is imported
const MemoizedPriceTicker = React.memo(PriceTicker);
export default MemoizedPriceTicker;
```

### Step 3: Verifying the Fix (The "After" State)

With the `console.log` still in place, I re-ran the app. The difference was night and day. The terminal was now quiet, only printing logs for the specific coins whose prices were actively being updated.

<video width="800" autoplay loop muted playsinline>
  <source src="/assets/img/posts/7Day-RN-Challenge/2025-07-01-Day4/rn-day4-after-memoization.mp4" type="video/mp4">
  After Optimization: The terminal is now calm. Render logs only appear for the specific coins receiving real-time price updates.
</video>

### Conclusion: An Investment in Quality

This entire cycle—identifying a potential issue, proving it with data, implementing a fix, and verifying the result—was completed in just 40 minutes. It was a small investment of time that yielded a massive improvement in the app's efficiency.

This is the kind of proactive, "under-the-hood" work that defines senior-level engineering. It's about anticipating problems and building a foundation that is not just functional, but truly performant.

---

With the app now optimized, I could confidently build the next core feature: the Watchlist. However, adding new code to a stable system is the ultimate test of its architecture, and the session quickly turned into a deep dive into the messy reality of feature development.

**Next up on Day 5:** [One Feature, Three Bugs, and the Reality of Senior Engineering](/posts/day-5-one-feature-three-bugs-and-the-reality-of-senior-engineering/)

---

### Join the Discussion

**1. What part of this post was most valuable to you?**

* (A) The explanation of the performance problem.
* (B) The clear, simple solution using `React.memo`.
* (C) The process of proving the problem and verifying the fix.

**Let me know your answer (A, B, or C) in the comments below!**

**2. A Question For You:**

What is one simple performance optimization you've implemented in your own projects that had a surprisingly massive impact?

---
*The best way to follow this 7-day sprint is by joining my newsletter for daily updates directly in your inbox.*

{% include newsletter_form.html %}