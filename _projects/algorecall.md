---
layout: nested
title: AlgoRecall
description: A Progressive Web App for spaced repetition learning of LeetCode problems
files:
  - 'features'
  - 'tech_stack'
  - 'implementation'
---

# [**AlgoRecall - Check it out!**](https://leetcode-anki.web.app/)

`A Progressive Web App that helps you practice LeetCode problems using spaced repetition learning techniques. This platform optimizes memory retention through scientifically-proven algorithms to help developers prepare for technical interviews more efficiently.`

I built a full-stack web application that applies spaced repetition algorithms to coding practice. The app includes user authentication, real-time data synchronization, a code editor, and intelligent problem recommendations. The frontend uses React with TypeScript, while the backend leverages Firebase for authentication, database, and hosting. I implemented the SM-2 spaced repetition algorithm from scratch.

The key innovation is applying spaced repetition algorithms to coding problems, ensuring users review problems at optimal intervals for maximum retention rather than forgetting solutions shortly after solving them. Instead of random practice, users get personalized problem recommendations based on their learning history and retention patterns.

### Target Users

- Software engineers preparing for technical interviews
- Computer science students learning algorithms
- Anyone wanting to maintain coding skills through systematic practice

### Features

| Feature                    | Description                                                           |
|---------------------------|-----------------------------------------------------------------------|
| Spaced Repetition Engine  | SM-2 algorithm implementation with dynamic interval calculation.      |
| Real-time Data Sync       | Firebase-powered synchronization with offline support and conflict resolution. |
| Progressive Web App       | Installable app with service workers and offline functionality.       |
| Code Editor Integration   | CodeMirror-powered editor with syntax highlighting and solution comparison. |
| Problem Recommendation    | AI-driven problem suggestions based on user performance patterns.     |
| Authentication System     | Google OAuth integration with secure token management.                |
| Payment Integration       | Stripe integration ready for future monetization.                     |

