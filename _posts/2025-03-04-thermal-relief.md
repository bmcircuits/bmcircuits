---
title: "Thermal relief on high-current PCBs: getting it right"
date: 2025-03-04
read_time: 5 min read
tags: [PCB Design, Thermal]
excerpt: Thermal relief pads are a soldering aid, not a heat management strategy. A look at when they help, when they hurt, and how to spec them correctly for power planes.
---

Thermal relief is one of those defaults that gets applied without thinking, and on most PCBs it's fine. Through-hole components on signal nets? Use thermal relief, make soldering easy. Power planes carrying 10A? That's where the default starts costing you.

## What thermal relief actually does

A thermal relief pad connects a through-hole pin to a copper plane via narrow spokes rather than a full flood connection. This reduces the thermal mass the iron has to overcome when soldering — without it, the plane acts as a heatsink and the joint won't flow properly. For hand or selective soldering, full-flood connections on inner power planes are a reliable way to get cold joints.

## When it hurts you

The spokes that make soldering easy also restrict current. Each spoke is a bottleneck, and for high-current paths — motor connectors, power input terminals, anything carrying more than 3–4A continuously — the resistance of four narrow copper spokes adds up to real voltage drop and localised heating. I've seen connector pins running visibly warm because of thermal relief on a 5A rail.

The fix is straightforward: for high-current vias and pads, remove thermal relief and use a full solid connection. Accept that you'll need a higher-wattage iron, pre-heat the board, or use reflow rather than hand soldering. The electrical performance is worth it.

## Spokes: how many, how wide?

If you do need thermal relief on a higher-current net, you can improve it by increasing spoke width and count. Most EDA tools let you set spoke width per net class. For a 3A net with thermal relief, four 0.5mm spokes is marginal — four 0.8mm spokes or six 0.5mm spokes give meaningfully lower resistance and better current handling.

Run a quick calculation: model each spoke as a short track and check the temperature rise at operating current using the IPC-2152 curves. It takes five minutes and will tell you whether your relief configuration is workable.

## The TL;DR

- Signal and low-current nets: thermal relief is fine, leave the default.
- High-current connections (>3A): remove thermal relief, use solid connection.
- Mid-range: calculate, or widen the spokes.
