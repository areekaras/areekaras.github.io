---
title: "The 7-Day Challenge: Bonus Round — 3 Pro-Level Features in 25 Minutes"
date: 2025-07-07 06:30:00 +0800
categories: [Build in Public, 7 day React Native Challenge]
tags: [buildinpublic, reactnative, polish, search, refactoring]
image:
  path: /assets/img/posts/7Day-RN-Challenge/2025-07-07-Bonus/rn-challenge-bonus-round.jpg
#   alt: A developer adding a final, glowing gear to a complex mechanism, symbolizing polish.
---

In my last post, I shared the [final retrospective of my 7-Day Challenge](/posts/7-day-challenge-complete-a-pro-level-react-native-app-in-under-11-hours/). The official challenge was complete. But a good project is never truly "done."

The true measure of an engineer is the commitment to iteration. With the main goals achieved ahead of schedule, I decided to hold a "bonus round"—a focused, 25-minute sprint to fix a lingering visual bug and add two of the most requested features for any list-based app: pull-to-refresh and search.

This session was about showing how to iterate on a solid foundation and rapidly add significant value. All work was done on a dedicated feature branch and merged via a Pull Request.

### Part 1: The Bug Hunt - Fixing the "Janky" First-Load Animation

First, I had to fix a subtle but annoying visual bug. When navigating to the Watchlist for the first time, the screen would perform a strange, full-screen fading animation. It felt jarring and out of place.

<p align="center">
  <strong>The Bug:</strong> Notice the jarring, full-screen animation when the watchlist first loads.
  <br><br>
  <video src="/assets/img/posts/7Day-RN-Challenge/2025-07-07-Bonus/bonus-animation-bug.mp4" width="350" autoplay loop muted controls></video>
</p>

**The Cause:** After some digging, I found the issue was an interaction between my asynchronous data loading and the `LayoutAnimation` API. The animation was being triggered on the initial render when the watchlist array went from `empty` to `populated`. This was not the intended experience.

**The Fix:** I needed to prevent the animation from running on the *first* render only. To do this, I used a `React.useRef` hook to create an `isInitialRender` flag. A ref is perfect for this because it persists across renders without causing re-renders itself. The `useEffect` that triggers the animation now checks this flag, only firing on subsequent user-driven changes. This small change completely fixed the bug.

<p align="center">
  <strong>The Fix:</strong> With the `useRef` flag, the screen now loads instantly without unwanted animation.
  <br><br>
  <video src="/assets/img/posts/7Day-RN-Challenge/2025-07-07-Bonus/bonus-animation-fixed.mp4" width="350" autoplay loop muted controls></video>
</p>

### Part 2: Feature #1 - Implementing Pull-to-Refresh

Even with live WebSockets, users have a deeply ingrained expectation for pull-to-refresh. It's a standard UX pattern that provides a sense of control.

**The Implementation:** This was surprisingly straightforward thanks to React Native's built-in `RefreshControl` component. I added a `refreshing` state variable, created an `onRefresh` callback function to re-fetch my API data, and passed them to the `<RefreshControl />` inside my `FlatList`. This resulted in a clean, native-feeling pull-to-refresh experience.

<p align="center">
  <strong>Feature 1:</strong> The Markets screen now supports native pull-to-refresh.
  <br><br>
  <video src="/assets/img/posts/7Day-RN-Challenge/2025-07-07-Bonus/bonus-pull-to-refresh.mp4" width="350" autoplay loop muted controls></video>
</p>

### Part 3: Feature #2 - Implementing Performant Search

For a list of 100 items, search is a core feature. My focus was on building a search that was both functional and highly performant.

**The Implementation:** I added a `searchQuery` state variable to hold the user's input from a `<TextInput>`. The core of the logic is a `React.useMemo` hook. This powerful hook creates a `filteredCoins` array. It's configured to only re-run its expensive filtering logic when one of its dependencies (the main `coins` array or the `searchQuery`) actually changes. This avoids re-filtering on every single price update and keeps the UI snappy.

The result is an instant, responsive search that filters the list as the user types, without any lag.

<p align="center">
  <strong>Feature 2:</strong> A search bar allows for instant, performant filtering of the coin list.
  <br><br>
  <video src="/assets/img/posts/7Day-RN-Challenge/2025-07-07-Bonus/bonus-search.mp4" width="350" autoplay loop muted controls></video>
</p>

### Conclusion: The Power of Iteration

This bonus 25-minute session elevated the application from a "completed challenge" to a genuinely useful and professional-feeling product. It's proof that a project is a living entity, constantly being improved. This process of listening to feedback (even your own), identifying areas for improvement, and rapidly iterating is the true essence of modern software development.

---

### Join the Discussion

**1. What part of this post was most valuable to you?**
* (A) The `useRef` trick for fixing the animation bug.
* (B) The `useMemo` strategy for performant search.
* (C) The philosophy of adding "bonus" polish after a project is "done."

Let me know your answer (A, B, or C) in the comments below!

**2. A Question For You:**
What's one "quality-of-life" feature you've added to a project that made you feel proud of the result?

---
*The best way to follow my expedition is by joining my newsletter for insights directly in your inbox.*
{% include newsletter_form.html %}