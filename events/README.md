---
title: Events
nav_order: 5
has_children: true
permalink: /events/
---

# Events

{% assign all_events = site.pages | where: "type", "Event" %}
{% assign actual_events = all_events | where: "actuality", "actual" | sort: "event_date" | reverse %}
{% assign hypothetical_events = all_events | where: "actuality", "hypothetical" | sort: "event_date" | reverse %}

## Actual Events

*Sorted newest first by event date.*

{% for event in actual_events %}
* **{{ event.event_date | date: "%Y-%m-%d" }}** — [{{ event.title }}]({{ event.url | relative_url }}) _{{ event.status }}_ — {{ event.description }}{% endfor %}

{% if hypothetical_events.size > 0 %}
## Hypothetical Scenarios

*Projected or speculative events, sorted by projected date.*

{% for event in hypothetical_events %}
* **{{ event.event_date | date: "%Y-%m-%d" }}** — [{{ event.title }}]({{ event.url | relative_url }}) _{{ event.status }}_ — {{ event.description }}{% endfor %}
{% endif %}
