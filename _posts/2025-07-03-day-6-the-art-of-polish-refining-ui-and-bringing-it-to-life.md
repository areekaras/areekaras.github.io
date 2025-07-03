---
title: "Day 6: The Art of Polish—Refining UI and Bringing it to Life"
date: 2025-07-03 07:00:00 +0800
categories: [Build in Public, 7 day React Native Challenge]
tags: [buildinpublic, reactnative, animation, ui, ux, polish]
image:
  path: /assets/img/posts/7Day-RN-Challenge/2025-07-03-Day6/rn-challenge-day-6.jpg
#   alt: A developer meticulously polishing a UI on a screen, making it glow.
---

After a marathon [Day 5 session of hunting bugs](/posts/day-5-one-feature-three-bugs-and-the-reality-of-senior-engineering/), the app was robust, functional, and stable. Today, we shift our mindset. Day 6 is dedicated to the final 10% of work that makes 90% of the difference to the user: **UI polish and animation.**

This is the phase where an app transforms from a tool that simply works into an experience that feels delightful to use. It's about refining every pixel, considering every interaction, and adding subtle motion that guides and reassures the user.

To reflect this move towards a more polished process, I also adopted a more professional Git workflow today, performing all my work on a dedicated feature branch (`feature/day6-ui-polish`).

### Part 1: Visual Polish - The Power of Spacing and Hierarchy

Before adding motion, I did a full review of the app's static UI. A clean interface isn't just about colors; it's about creating a clear visual hierarchy that makes information easy to digest.

**Refining the PriceTicker:** In the main list, I made several small but impactful changes to each row. I increased the font size and weight of the coin's full name while making the symbol slightly more subtle. This simple change immediately draws the user's eye to the most important piece of information. I also adjusted the vertical and horizontal padding to give each element more room to breathe.

<p align="center">
  <img src="/assets/img/posts/7Day-RN-Challenge/2025-07-03-Day6/ui-polish-before-after-pickerfield.png" alt="Before and after comparison of the UI polish" width="800px">
</p>

**Refining the DetailsScreen:** On the details page, the most critical piece of information is the current price. I significantly increased its font size to make it the hero element of the screen. I also added the 24-hour percentage change directly below it, providing immediate context for the price movement shown in the chart.

<p align="center">
  <img src="/assets/img/posts/7Day-RN-Challenge/2025-07-03-Day6/ui-polish-before-after-detailscreen.png" alt="Before and after comparison of the UI polish" width="800px">
</p>

These may seem like minor tweaks, but collectively, they create a much more professional and user-friendly experience.

### Part 2: The Animation Journey

My goal was to add a simple, satisfying animation for when a user adds or removes a coin from their watchlist. I decided to use React Native's built-in `LayoutAnimation` API, a great tool for simple transitions without adding a heavy new library.

After enabling it in my `App.tsx` file, I added the animation trigger to my `WatchlistScreen`. I added a coin to my watchlist on the details page and navigated over, expecting to see it animate into view.

But nothing happened.

#### The Debugging Insight: When Does State *Really* Change?

This led to a fascinating debugging session and a key insight into how React and navigation work together.

**The Problem:** The animation wasn't firing because the data was changing *before* I got to the screen. Here's the sequence:
1. On the `DetailsScreen`, I tap the star icon.
2. The `toggleWatchlist` action updates the global Zustand store **instantly**.
3. The `WatchlistScreen`, though not visible, is now aware that its list of coins has changed.
4. I navigate to the `WatchlistScreen`. It mounts with the **already updated** list.
5. Since the list's content doesn't change *while the screen is visible*, `LayoutAnimation` has nothing to animate.

**The Solution:** To see the animation, the state change must be triggered while the user is looking at the component that needs to animate.

The fix was to enhance the user experience by adding a "remove" button directly to the list items on the `WatchlistScreen`. I modified the `PriceTicker` component to accept an optional `onRemove` function. On the `WatchlistScreen`, I passed the `toggleWatchlist` action to this new prop.

Now, when the user is on the watchlist and taps the trash can icon, the state updates, `LayoutAnimation` is triggered, and the item smoothly animates out of the list with a satisfying spring effect.

<p align="center">
  <strong>The Final Result:</strong> Watch as tapping the trash can icon triggers a smooth spring animation, removing the item from the list.
  <br><br>
  <video src="/assets/img/posts/7Day-RN-Challenge/2025-07-03-Day6/watchlist-remove-animation.mp4" autoplay loop muted playsinline width="350"></video>
</p>

### Conclusion: A New Workflow and a Polished Product

Day 6 was about more than just aesthetics. It was about improving my development process and thinking deeply about the user's experience. By adopting feature branches, my work is now more organized and easier to review.

<p align="center">
  <a href="https://github.com/areekaras/signal-crypto-dashboard/pull/1" target="_blank" rel="noopener noreferrer">
    <img src="/assets/img/posts/7Day-RN-Challenge/2025-07-03-Day6/github-pull-request.png" alt="Pull Request for the Day 6 UI Polish feature branch" width="800px">
  </a>
</p>

By debugging the animation timing, I was able to add a new piece of functionality that not only solved the problem but also made the app better to use. We now have a polished, animated, and professionally structured application.

### What's Next: The Final Feature is Documentation

With the core functionality built and polished, the coding phase of this 7-day challenge is effectively complete. We are well ahead of schedule, which gives us the breathing room to focus on what I consider to be the final, and one of the most important, features of any professional project: **documentation.**

Tomorrow, on Day 7, the focus will shift from writing code to writing prose. I will be creating a comprehensive `README.md` file for the project's GitHub repository. A great README is more than just instructions; it's the front door to your project. It explains the "why" behind the technical decisions, outlines the architecture, and provides a clear guide for anyone who wants to run the app themselves.

For a portfolio piece, this is non-negotiable. It demonstrates professionalism, clear communication, and a respect for other developers who might interact with your work. The code tells the story of what the app does; the documentation tells the story of how and why it was built.

---

### Join the Discussion

**1. What part of this post was most valuable to you?**
* (A) The UI polish and visual hierarchy tips.
* (B) The detailed breakdown of the `LayoutAnimation` bug and fix.
* (C) The insight into using a proper Git workflow with feature branches.

Let me know your answer (A, B, or C) in the comments below!

**2. A Question For You:**
What is one small UI polish or animation you've added to a project that made a huge difference to the user experience?

---
*The best way to follow this 7-day sprint is by joining my newsletter for daily updates directly in your inbox.*

{% include newsletter_form.html %}