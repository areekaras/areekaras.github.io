---
title: "Day 5: One Feature, Three Bugs, and the Reality of Senior Engineering"
date: 2025-07-02 07:00:00 +0800
categories: [React Native Challenge, Development]
tags: [buildinpublic, reactnative, debugging, architecture, engineering]
image:
  path: /assets/img/posts/7Day-RN-Challenge/2025-07-02-Day5/rn-challenge-day-5.jpg
  alt: A developer depicted as a detective, analyzing code to hunt for bugs.
---

After the major performance optimization on [Day 4](/posts/day-4-the-40-minute-optimization-every-react-developer-should-know/), the app was lean and ready for its next core feature. The plan for Day 5 was to build the user "Watchlist" from scratch. On paper, it was a 40-minute task.

In reality, the session clocked in at **2 hours and 55 minutes.**

The good news is that I successfully built the entire feature. The real story, however, is that making a new feature *work* is only half the battle. Making it work *correctly* and *robustly* is where the real engineering begins. This is the unfiltered reality of senior-level development: a simple feature can uncover a web of complex challenges that must be solved.

### Step 1: Building the Initial Watchlist Feature

The goal was to allow users to save their favorite coins for easy tracking. The initial implementation plan was straightforward:
1.  Use `@react-native-async-storage/async-storage` for local persistence.
2.  Create a custom `useWatchlist` hook to encapsulate the logic for adding, removing, and loading favorited coins.
3.  Add a "star" icon to the `DetailsScreen` header to toggle a coin's status.
4.  Build the `WatchlistScreen` to display only the favorited coins.

With the plan set, I started building. And almost immediately, after getting the initial code in place, the plan met reality.

### The First Hurdle: The "Stale State" Bug

After implementing the hook and the UI, I tested the flow. I could star a coin on the Details screen, but when I navigated to the Watchlist screen, it was still empty. The change only appeared after a full app restart.

Here is the buggy behavior in action:

<p align="center">
  <strong>The Bug:</strong> The Watchlist screen doesn't update until the app is restarted.
  <br><br>
  <video src="/assets/img/posts/7Day-RN-Challenge/2025-07-02-Day5/rn-day5-stale-state-bug.mp4" width="800" autoplay loop muted playsinline></video>
</p>

**The Cause:** This was a classic state management problem. My custom hook created a separate, isolated state for each screen. The `DetailsScreen` and the `WatchlistScreen` had different instances of the state and were completely unaware of each other.

**The Fix:** The solution was a necessary refactor. I moved all the watchlist logic into our global Zustand store. By creating a single source of truth, any change made on one screen would now be instantly and reactively available everywhere else.

Here is the corrected version after the fix:

<p align="center">
  <strong>The Fix:</strong> With a global store, the Watchlist screen updates instantly.
  <br><br>
  <video src="/assets/img/posts/7Day-RN-Challenge/2025-07-02-Day5/rn-day5-stale-state-fixed.mp4" width="800" autoplay loop muted playsinline></video>
</p>

### The Second Hurdle: The Infinite Render Loop Crash

With the state management refactored, a much more sinister bug appeared. The app would crash with a terrifying "Maximum update depth exceeded" error whenever a price updated while I was on the DetailsScreen.

<p align="center">
  <img src="/assets/img/posts/7Day-RN-Challenge/2025-07-02-Day5/rn-day5-max-update-error.png" alt="Maximum update depth exceeded error" width="800px">
</p>

**The Cause:** This is a classic React infinite loop. A WebSocket price update caused the `DetailsScreen` to re-render. My `useLayoutEffect` hook, which set the header's star icon, depended on the entire `coin` object. Since the object reference changed on every re-render, the effect would run again, triggering another re-render, and so on, until the app crashed.

**The Fix:** An architectural one. I refactored the `DetailsScreen` to use granular selectors with Zustand (subscribing to individual data points instead of the whole object) and wrapped the star icon's `onPress` handler in a `React.useCallback` hook to give it a stable reference. This permanently broke the loop.

### The Third Hurdle: The API Rate Limit Crash

With the app stable, I noticed it would still sometimes crash with an `AxiosError: Request failed with status code 429`. I was hitting the free CoinGecko API's rate limit by fetching chart data every single time the DetailsScreen was opened.

![Axios 429 Too Many Requests error in the terminal logs](/assets/img/posts/7Day-RN-Challenge/2025-07-02-Day5/rn-day5-axios-429-error.png){: width="800" }

**The Fix:** I implemented a simple but effective caching strategy in my Zustand store. Now, my `fetchChartData` action first checks if data for a coin exists in a `chartDataCache` object. If it does, it returns the cached data instantly. If not, it fetches from the API and saves it to the cache for next time.

### The Final Challenge: A Pragmatic Decision

After fixing all the crashes, one warning remained: the `VirtualizedList: You have a large list that is slow to update...` log. Here, I made a conscious, senior-level decision: **I will not fix this for now.** For a 7-day challenge, a major refactor to a library like FlashList is out of scope. Acknowledging a known limitation and making a pragmatic decision based on project constraints is a critical engineering skill.

### Conclusion: More Than Just a Feature

Today, we didn't just build the Watchlist feature; we hardened the entire application. We took a simple feature, found its flaws, and re-architected it to be robust, performant, and crash-free. These are the challenges that truly level up your skills.

---
You can view the final state of the code for this feature in [this commit on GitHub](https://github.com/areekaras/signal-crypto-dashboard/compare/f276159...27366b9).

Next up on Day 6, we'll build on this stable foundation to [implement a personalized, reorderable Watchlist](/)
<!-- [implement a personalized, reorderable Watchlist](/posts/rn-challenge-day6-reorderable-list/). -->

---

### Join the Discussion

**1. What part of this post was most valuable to you?**
* (A) The state management (Zustand) solution.
* (B) The breakdown of the infinite render loop bug.
* (C) The pragmatic decision not to fix the final warning.

Let me know your answer (A, B, or C) in the comments below!

**2. A Question For You:**
What's the most complex bug you've ever had to hunt down? What was the "aha!" moment that finally led to the solution?

---
*The best way to follow this 7-day sprint is by joining my newsletter for daily updates directly in your inbox.*

{% include newsletter_form.html %}