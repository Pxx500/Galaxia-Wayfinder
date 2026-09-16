---
type: wayfinder-ticket
ticket_type: grilling
status: deferred
parent: Galaxia Alpha Wayfinder
areas:
  - "[[Area - Travel and Logistics]]"
secondary_areas:
  - Area - Automation and Infrastructure
blocked_by: []
claimed_by:
tags:
  - galaxia/alpha
  - wayfinder/ticket
  - wayfinder/grilling
  - wayfinder/deferred
---

# Define Team Notification System

## Question

How does Galaxia report team-wide asset, mission, logistics, and automation events so players can notice problems and react without continuously watching the Star Map?

## Established Direction

- The team needs a shared notification system for relevant Star Map assets and operations.
- Gameplay systems emit typed events. Players can configure which event types and conditions create notifications and what kind of notification they create.
- The Star Map provides a central place to review current notifications.
- Important new notifications may also appear as an on-screen corner notification while the player is outside the Star Map.
- A vehicle that cannot execute a configured action and remains waiting reports the concrete asset and reason, such as insufficient takeoff capability or a blocked launch path.
- Scheduled-action failures use a typed event carrying the affected vehicle, action, and concrete failure reason. Player-facing copy is localized at the rendering boundary.
- A conflict between vehicle-owned and dock-owned cargo actions may create an active warning carrying the affected vehicle, endpoint, and concrete conflict reason.
- Condition-backed problems use stable active notifications rather than repeated event spam. Retries update or renew the same notification identity.
- The source maintains an active notification while its condition remains true and resolves it when the condition clears.
- Active notifications have a bounded lifetime or lease. If the source stops maintaining one without resolving it, it expires instead of remaining stuck forever.
- Resolving a blocked scheduled action removes it from the active notification view. Any separate history policy remains deferred with the rest of the notification presentation design.
- Event sources are not limited to logistics or failures. Custom and narrative events, such as detecting an unknown spacecraft, may use the same notification system.
- Notifications report operational state; they do not invent destructive consequences for physically impossible actions.
- Notifications should let the player identify the affected asset and decide what intervention is needed.
- A changed vehicle destination, recalculated onward journey, and inability to perform that journey use this general system. Any player acknowledgement belongs to the shared notification policies rather than a dedicated route-change dialog mechanism. Exact presentation remains deferred.

## Deferred Boundary

Stable active-notification identity, renewal, resolution, and bounded expiry are accepted above. The concrete event catalogue, notification history, presentation, and player configuration remain deferred until the event-producing systems provide concrete requirements. The vehicle-owned dispatch model is already resolved.

## Open Questions

- Which event categories and severities belong in Alpha?
- Which notifications appear outside the Star Map?
- Should selecting a notification focus the affected asset or open its relevant screen?
- How are one-off events, acknowledgements, and history presented? Condition-backed retry deduplication and expiry are already settled.
- Which notifications are visible to the whole team versus only the acting player?

## Related Topics

- [[Define Destination Access Levels]]
- [[Define Alpha Transport Roles]]
- [[Define Player Flight Interaction Model]]
- [[Area - Automation and Infrastructure]]
