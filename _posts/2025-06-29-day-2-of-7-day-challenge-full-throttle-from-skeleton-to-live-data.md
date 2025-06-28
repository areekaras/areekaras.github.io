---
title: "Day 2 of the 7-Day Challenge: Full Throttle—From Skeleton to Live Data"
date: 2025-06-29 07:00:00 +0800
categories: [Build in Public, 7 day React Native Challenge]
tags: [buildinpublic, reactnative, challenge, debugging, productivity, flow-state]
image:
  path: /assets/img/posts/7Day-RN-Challenge/2025-06-29-Day2/rn-challenge-day-2.jpg
#   alt: A developer in a flow state, with code streaming from their fingertips onto a screen.
---

[Day 1 was a battle](/posts/day-1-of-7-day-challenge-when-a-blank-slate-becomes-the-first-boss-battle/)—a 2.5-hour grind against a stubborn setup error. Today was the reward. The resolution of that initial struggle unlocked a state of pure, productive flow.

This post covers the work I had *planned* for Day 2 of my 7-day challenge. The truth is, I accomplished all of this in a hyper-focused 2-hour session yesterday, right after solving the Day 1 issues. This is the part of software development I love: when the foundation is solid and you can just *build*.

Let's break down how we went from an empty screen to a functional, data-driven app.

## Part 1: Building the Skeleton & The Final Hurdles

The first order of business was to build the app's skeleton. However, because I had to manually download the project template yesterday, the `package.json` file wasn't perfectly aligned with my Expo SDK version. This led to a few final hurdles.

When I ran `npm install`, I was immediately greeted with a dependency conflict.

![NPM ERESOLVE dependency conflict error in the terminal](/assets/img/posts/7Day-RN-Challenge/2025-06-29-Day2/rn-day2-eresolve-error.png){: width="800" }

This `ERESOLVE` error is npm's way of saying that different packages in the project had conflicting requirements. For example, the `expo-template-blank-typescript` I downloaded from GitHub specified `react-native: "0.80.0"`, but other libraries expected a different version.

![Original package.json file showing conflicting versions](/assets/img/posts/7Day-RN-Challenge/2025-06-29-Day2/rn-day2-original-package-json.png){: width="800" }

The fix was to manually edit my `package.json` to use the exact versions compatible with my Expo SDK, and then run the installation with a special flag: `npm install --legacy-peer-deps`. This tells npm to be more lenient and resolve the minor conflicts.

With that solved, I created the theme file and the bottom tab navigator. But when I ran the app, I was met with one final, unexpected error.

![ExpoFontLoader error in the simulator red screen](/assets/img/posts/7Day-RN-Challenge/2025-06-29-Day2/rn-day2-expofontloader-error.png){: width="800" }

This `_ExpoFontLoader.default.getLoadedFonts is not a function` error was happening because the icon library (`@expo/vector-icons`) couldn't load its fonts. The fix was to explicitly re-install the `expo-font` package using `npx expo install expo-font`.

After clearing that final hurdle, the app's skeleton was finally complete and running correctly.

![The app skeleton with dark theme and bottom navigation tabs](/assets/img/posts/7Day-RN-Challenge/2025-06-29-Day2/rn-day2-skeleton-app.png){: width="800" }

## Part 2: Breathing Life into the App with Live Data

With the UI shell fully functional, it was time for the most exciting part: fetching real data from the CoinGecko API.

### The API Service Layer
I created a dedicated file, `coingeckoAPI.ts`, to handle all API communication. This separation of concerns is vital. My UI components don't need to know *how* the data is fetched; they just need to receive it. I used `axios` for the HTTP request and defined a clear TypeScript `Coin` interface to ensure my data was strongly typed.

### The PriceTicker Component
Before displaying a list, I needed to design the row. I built a reusable React component called `PriceTicker.tsx`. It takes all the necessary data for one coin and renders it in a clean layout. A key detail here was styling the price change percentage: green for positive, red for negative, using the colors from our theme file.

### The Markets Screen & The FlatList
This is where everything came together. I updated the `MarketsScreen.tsx` file to use a `useEffect` hook to call my API function when the screen loads and store the data in state. The list itself is rendered using React Native's `<FlatList>` component, which is essential for performance with long lists.

## The Result: A Day of Pure Flow

In what felt like a blink of an eye compared to yesterday, I went from a blank screen to this:

<video width="40%" autoplay loop muted playsinline>
  <source src="/assets/img/posts/7Day-RN-Challenge/2025-06-29-Day2/rn-day2-final-app.mp4" type="video/mp4">
  Your browser does not support the video tag.
</video>

...

The speed and progress were exhilarating. It's a testament to the power of a stable environment and the force-multiplying effect of modern tools. In fact, I was so in the zone that after finishing this work, I immediately started on the tasks planned for Day 3 in the same evening session.

---
This post covers the first half of my hyper-productive Saturday. In the next post, I'll share the results of that second session, where I tackled [real-time data with WebSockets, charting, and the perils of `--force`](/). 
<!-- [real-time data with WebSockets, charting, and the perils of `--force`](/posts/day-3-of-7-day-challenge-real-time-data-charting-and-the-perils-of-force/). -->

---

### Join the Discussion

I'm documenting my journey to learn in public. Your feedback is a crucial part of that process.

**1. What part of this post was most valuable to you?**

* (A) The details on resolving `package.json` conflicts.
* (B) The architectural approach (API layer, reusable components).
* (C) The story of overcoming struggle to find a flow state.

**Let me know your answer (A, B, or C) in the comments below!**

**2. A Question For You:**

What's one tool or technique in your workflow that, once set up correctly, unlocks a huge boost in your productivity and flow state?

---
*The best way to follow this 7-day sprint is by joining my newsletter for daily updates directly in your inbox.*
{% include newsletter_form.html %}