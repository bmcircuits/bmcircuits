---
title: The case for writing a short design doc before touching KiCad
date: 2025-01-20
read_time: 7 min read
tags: [Process, Hardware]
excerpt: Two pages of plain text up front can save you a board respin. What I put in a pre-layout design document and why it's become a non-negotiable part of my process.
---

The temptation when starting a new hardware project is to open KiCad, create a schematic, and start placing components. It's satisfying, it feels like progress, and the design doc can always come later. I've done this more times than I'd like to admit, and it has cost me board respins every single time.

## What goes in the document

It doesn't need to be long. Two pages is usually enough. I cover:

- **Functional requirements** — what must this board do, at what voltage, drawing how much current.
- **Interface requirements** — what connectors, what protocols, what pinout constraints exist from the mating system.
- **Mechanical constraints** — board outline, mounting holes, keep-out areas, connector orientation requirements.
- **Open questions** — the things I don't know yet and need to resolve before layout starts.

That last section is the most valuable. Writing it down forces you to realise what you're assuming. "The microcontroller has enough timer channels for PWM generation" is easy to assume; writing it down prompts you to actually check the datasheet. It turns vague assumptions into explicit design decisions that can be verified or challenged.

## The real payoff

The document also serves as a communication tool. If you're working with a client, having them sign off on a requirements doc before you start means the schematic review conversation is about implementation, not about whether the requirements were right. That's a much more productive place to have disagreements.

Even on solo projects, writing the requirements down and sleeping on it before opening KiCad has caught more than a few issues that would otherwise have become respin-worthy.

## What format?

Plain text or Markdown, in version control alongside the design files. Not a Word document, not a shared Google Doc with tracking turned off. The design doc should evolve with the project — it's a living reference, not a waterfall deliverable.

I use a simple template I've built up over several projects. If there's interest, I'll post it as a separate article.
