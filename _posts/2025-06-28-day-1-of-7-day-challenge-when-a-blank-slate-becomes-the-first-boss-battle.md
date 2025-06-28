---
title: "Day 1 of the 7-Day Challenge: When a 'Blank Slate' Becomes the First Boss Battle"
date: 2025-06-28 07:00:00 +0800
categories: [Build in Public, 7 day React Native Challenge]
tags: [buildinpublic, reactnative, challenge, debugging, engineering]
image:
  path: /assets/img/posts/7Day-RN-Challenge/2025-06-28-Day1/rn-challenge-day-1.jpg
#   alt: A developer looking frustrated at a screen full of error messages in a dark room.
---

Yesterday, I announced [a strategic pivot and a new 7-Day React Native Challenge](/posts/a-strategic-pivot-the-7-day-react-native-challenge/). The sprint started today.

Every developer knows the feeling. You have a new project, a clean slate, and a solid plan. The energy is high, and you're ready to build. That was me this morning. My Day 1 plan seemed simple enough: get the basic environment set up and initialize a blank project.

My to-do list was straightforward:
* Create the GitHub repo
* Install Node.js, Watchman, Expo CLI, and the Gemini CLI
* Initialize a blank TypeScript project with Expo
* Create the basic folder structure
* Get the app running on the simulator

I've learned that while coding features is the visible part of our work, environment setup is often the first, unseen hurdle. For me, Day 1 turned into a 2.5-hour deep dive into just how challenging that hurdle can be.

## The Wall: `npm pack exited with non-zero code: 1`

After methodically setting up my tools, I reached the final step: creating the project itself. I ran the standard command: `npx create-expo-app . --template blank-ts`.

And hit a wall. Hard.

![Initial npm error message showing non-zero exit code](/assets/img/posts/7Day-RN-Challenge/2025-06-28-Day1/rn-challenge-day1-npm-pack-error.png){: width="800" }

This error, `npm pack blank-ts@latest --dry-run --json exited with non-zero code: 1`, became the villain of my day. It's a cryptic message that essentially meant my computer was failing to download the "blank-ts" starter template from the internet via npm.

What followed was an extensive debugging session where my AI consultant, Gemini, and I suspected every part of my new M4 Mac's setup:
* We cleaned the npm cache with `--force`. No luck.
* We used `nvm` (Node Version Manager) to switch my Node.js version to the stable LTS. Same error.
* We did a "deep clean," suspecting that files from my old Intel Mac backup were causing conflicts on the new Apple Silicon architecture. This involved `sudo`-level commands to remove every trace of old Node installations.

No matter what we tried, `npm pack` refused to cooperate. The automatic route was completely blocked.

## The Breakthrough: Asking a Better Question

After hours of hitting the same wall, I took a step back. Instead of asking "How do I fix this command?", I asked, **"What is this command *actually trying to do*?"**

The answer was simple: it was just trying to download a folder of template files.

Gemini suggested an alternative: what if we just download the files ourselves? It was a simple, elegant solution that bypassed the broken command entirely. I went directly to the Expo GitHub repository, downloaded the `expo-template-blank-typescript` folder as a ZIP file, and set up the project manually.

It felt like finding a secret passage around the castle wall I'd been trying to break down for hours.

## First Light, and a Final Glitch

With the template files now on my machine, I ran `npm install --legacy-peer-deps` (which gave some normal warnings but worked!) and then the magic command: `npx expo start`.

![Metro bundler running successfully in the terminal](/assets/img/posts/7Day-RN-Challenge/2025-06-28-Day1/rn-challenge-day1-metro.png){: width="800" }

The app launched on my simulator! It was a massive moment of relief. But, of course, there was one final mini-boss to defeat: the "React Native version mismatch" error.

![Red screen error on iPhone simulator showing React Native version mismatch](/assets/img/posts/7Day-RN-Challenge/2025-06-28-Day1/rn-challenge-day1-redscreen.png){: width="350" }

This error meant the app's cache was stale from all our previous attempts. Thankfully, the fix was simple: shutting down the server and restarting it with `npx expo start --clear`.

## The Triumph: A True Blank Slate

And then, finally. Success.

![A clean, error-free "blank slate" app running on the iPhone simulator](/assets/img/posts/7Day-RN-Challenge/2025-06-28-Day1/rn-challenge-day1-success.png){: width="350" }

After a 2.5-hour battle, I had my blank canvas. It was a powerful reminder that sometimes the simplest-sounding tasks can hide the most complex problems.

### Key Learnings from Day 1

This intense setup session gave me a few key insights I wasn't expecting:
1.  **Understand the "Why," Not Just the "How":** When a tool fails, understanding *what it does* is more powerful than just knowing how to use it. Realizing `create-expo-app` was just a file downloader allowed me to find an alternative path.
2.  **`sudo` Isn't Pseudocode:** A "today I learned" moment. I always thought `sudo` was just some jargon. I learned it stands for "Super User Do," a command to perform actions with administrative privileges. It was the key to cleaning up stubborn, permission-locked files.
3.  **The Environment is Everything:** A stable, clean development environment is the most critical and often most overlooked part of software engineering. The time spent today getting it right will pay dividends for the rest of the challenge.

Day 1 wasn't about writing features; it was about persistence. Now that the foundation is truly set, I'm excited to finally start building.

---
Now that the environment is stable, Day 2 will be about giving the app its identity. Next up: [Building the UI Skeleton with Theming and Navigation](/)
<!-- [Building the UI Skeleton with Theming and Navigation](/posts/rn-challenge-day2-theming-and-navigation/). -->

---

### Join the Discussion

I'm documenting my journey to learn in public. Your feedback is a crucial part of that process.

**1. What part of this post was most valuable to you?**
* (A) The detailed debugging process.
* (B) The "aha!" moment of asking a better question.
* (C) The final key learnings and reflections.

**Let me know your answer (A, B, or C) in the comments below!**

**2. A Question For You:**
What's the longest you've ever spent debugging a "simple" setup problem that turned out to have a surprisingly straightforward solution?

---
*The best way to follow this 7-day sprint is by joining my newsletter for daily updates directly in your inbox.*
{% include newsletter_form.html %}