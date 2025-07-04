---
title: "7-Day Challenge Complete: A Pro-Level React Native App in Under 11 Hours"
date: 2025-07-04 07:00:00 +0800
categories: [Build in Public, 7 day React Native Challenge]
tags: [buildinpublic, reactnative, challenge, portfolio, retrospective, ai]
image:
  path: /assets/img/posts/7Day-RN-Challenge/2025-07-04-Day7/rn-challenge-day-7.jpg
#   alt: A clean developer's desk showing the finished app, code, and a completed checklist, symbolizing the end of a successful project.
---

One week ago, I started a public challenge: build a functional crypto tracking app in just seven days. The goal was to test my own limits, refresh my React Native skills, and document every step as a case study in software engineering. This final post is a comprehensive retrospective of that sprint, building on the work from [Day 6, where I focused on the art of UI polish and animation](/posts/day-6-the-art-of-polish-refining-ui-and-bringing-it-to-life/).

Today, the challenge is complete.

Not only is the application finished, but the entire project—from a hostile initial setup to a polished final product—was completed in **10 hours and 20 minutes** of focused development time. This was done across just three actual days, which is proof of what's possible when deep experience is paired with modern tools.

This post is a comprehensive retrospective of that journey. It's a showcase of the final product, a reflection on what it takes to build at speed, and a look at the real-world problems that define modern mobile development.

### The Final Product: "Signal" Crypto Dashboard

First, let's see the app in action. Here is a full demonstration of all its features, from the live-updating market list and smooth navigation to the interactive, persistent watchlist.

<p align="center">
  <video src="/assets/img/posts/7Day-RN-Challenge/2025-07-04-Day7/final-app-demo.mp4" width="350" autoplay muted controls></video>
</p>

The application is more than just a proof-of-concept; it's a production-ready foundation. You can explore the complete, well-documented source code for the project on GitHub:
**[https://github.com/areekaras/signal-crypto-dashboard](https://github.com/areekaras/signal-crypto-dashboard)**

### The Journey: A Day-by-Day Retrospective

This project was a marathon sprint, filled with tough challenges and rewarding breakthroughs. The entire story is captured in my daily blog posts.

* **[Day 1: The First Boss Battle](/posts/day-1-of-7-day-challenge-when-a-blank-slate-becomes-the-first-boss-battle/) (3h 40m):** A simple setup turned into an intense debugging session, proving a stable environment is the most critical prerequisite.
* **[Day 2: Hitting Hyperspeed](/posts/day-2-of-7-day-challenge-full-throttle-from-skeleton-to-live-data/) (1h 55m):** With the setup stable, progress exploded. I built the app's entire skeleton and displayed a live list of data.
* **[Day 3: The "Wow" Factor](/posts/day-3-of-7-day-challenge-real-time-data-charting-and-the-perils-of-force/) (1h 25m):** This session added dynamic features like a live WebSocket feed and data visualization with charting.
* **[Day 4: The 40-Minute Optimization](/posts/day-4-the-40-minute-optimization-every-react-developer-should-know/) (40m):** A short but critical session where I used `React.memo` to fix a major re-rendering issue, showing that performance is a feature.
* **[Day 5: The Reality of Senior Engineering](/posts/day-5-one-feature-three-bugs-and-the-reality-of-senior-engineering/) (2h 35m):** Building the "Watchlist" feature uncovered a cascade of bugs, turning the day into a deep dive into debugging and architecture.
* **[Day 6: The Art of Polish](/posts/day-6-the-art-of-polish-refining-ui-and-bringing-it-to-life/) (45m):** The final coding session was dedicated to user experience, refining the UI and adding subtle animations to make the app feel delightful.

### My Approach: Experience Amplified by AI

This project was a test of a modern workflow. With over 8 years of experience, my foundation is in system design and robust architecture. I understand the "why" behind the code.

For this challenge, I paired that experience with an AI coding assistant (Gemini). The AI was not a replacement for my skills; it was an amplifier. It acted as a tireless pair programmer, handling boilerplate tasks and generating initial component structures based on my precise prompts. This synergy allowed me to focus my energy on high-impact, senior-level work:

* **Architecting Data Flow:** Designing the state management, data fetching, and caching strategies required experience.
* **Debugging Complex Issues:** When the app crashed with an infinite render loop, the AI couldn't solve it. It required a deep understanding of React's render cycle to diagnose and fix the root cause.
* **Making Pragmatic Decisions:** The choice to accept the `VirtualizedList` warning was a strategic trade-off based on the project's constraints, a decision that comes from experience.

This combination of deep human experience and targeted AI assistance is what made it possible to build a quality application in such a short amount of time.

### The Final Day's Work: Professional Documentation

With the coding complete, the final task for Day 7 is one of the most important features of any professional project: **documentation.**

I will be creating a comprehensive `README.md` file for the project's GitHub repository. A great README is the front door to your project. It explains the "why" behind technical decisions, outlines the architecture, and provides a clear guide for anyone to run the app themselves. For a portfolio piece, this is non-negotiable. It demonstrates professionalism, clear communication, and respect for other developers.

### A Final Thought: The Engineer Behind the Code

This challenge was more than just a coding exercise. It was a demonstration of the principles I bring to every project I undertake.

My persistence was tested on Day 1, turning a 2.5-hour setup battle into a stable foundation. My discipline was proven through the daily documentation and methodical process, even when faced with unexpected hurdles. My passion for learning is evident in my deep dive into the modern React Native ecosystem and my strategic partnership with AI.

The world of technology is evolving at an incredible pace. For teams looking to navigate this landscape and implement modern solutions, my ability to pair a deep engineering foundation with a rapid, disciplined learning process is a powerful combination. This challenge proves that I don't just learn new technologies; I stress-test them, find their limits, and build high-quality, documented products with them.

If your team is looking for an engineer who brings not just technical skill, but also resilience, discipline, and a passion for building things the right way, I am confident I can be that person. I am always ready for the next difficult problem and the next steep climb.

Thank you for following along on this journey.

---

### Join the Discussion

**1. What part of the 7-day challenge was most interesting to you?**
* (A) The initial setup struggles (Day 1).
* (B) The deep-dive debugging sessions (Day 3 & 5).
* (C) The final thoughts on combining experience with AI.

Let me know your answer (A, B, or C) in the comments below!

**2. A Question For You:**
After seeing this week-long journey, what is one piece of advice you would give to someone starting their own "build in public" challenge?

---
*This 7-day sprint is complete, but the expedition continues. Get my future posts directly in your inbox by joining my newsletter.*

{% include newsletter_form.html %}q