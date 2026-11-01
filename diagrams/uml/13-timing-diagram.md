# Timing diagram

Mermaid type: none (Not supported). UML type: timing diagram.

## Description

Behavior of objects against a time axis, showing when state changes occur and how long each state lasts.

## Example usages

- Real-time or embedded system timing constraints
- Signal and bus protocol timing such as clocks and handshakes
- Latency analysis across components
- Showing timeouts and deadlines

## Limitation in Mermaid

Mermaid cannot draw timing diagrams with state lifelines on a shared time axis. `gantt` shows durations and dates only, so it is not a substitute. Use PlantUML (`@startuml` with `concise` or `robust` declarations) instead.
