---
title: Dynamic Scheduler FAQs
description: Answer to all things around the Dynamic Scheduler
---
### Q. What are the overtime limits that the Dynamic Scheduler follows when assigning routes to drivers?

The Dynamic Scheduler algorithm assigns up to **42 hours** of work to drivers who are eligible for Solo 1 or Solo 2 route assignments.

Drivers who are only eligible for Solo 2 routes will be allowed to have up to **56 hours** of work.

### Q. Does the Dynamic Scheduler prioritize certain drivers?

The Dynamic Scheduler first prioritizes drivers who are **not** marked as Standby drivers when scheduling routes. After all non-standby drivers have been utilized for route assignments, it then uses Standby drivers to assign out remaining routes.
