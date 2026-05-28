---
title: Scheduling a Route
description: The building blocks to scheduling a route in Copilot.
---
## Adding a Route in Copilot

To schedule a route in Laminar Copilot, you'll first need to add the route into the app. Follow these steps:

1. **Open the Command Center**

2. **Click "+ Add Route"**

3. **Select the Route Type** — choose the appropriate route type (Solo 1, Solo 2, RLB, or MAINT). The fields required to complete scheduling will vary based on the route type (see below).

4. **Enter required details** — fill in all mandatory fields for the route type you selected. For example, Solo 1 and Solo 2 routes require Block ID, Start Date, Contract, Start Point, End Point, Driver, and Asset.

5. **Review driver and asset eligibility** — use the dropdowns to assign available drivers and assets. Copilot will automatically prioritize eligible drivers and filter assets based on availability.

6. **Save the route** — once all required fields are complete, click **Save**. The new route will appear in your Routes list and can be scheduled immediately.

**Note:** If any required fields are missing, Copilot will flag them and prevent the route from being scheduled until they're completed.

---

# Scheduling Different Route Types

Scheduling any route in Laminar Copilot has a set of required fields based on the Route Type.

## Solo 1 or Solo 2 Routes

If a route has the route type of **Solo 1** or **Solo 2**, the following fields are required:

- Block ID

- Start Date

- Contract – pulls in start times from the Contracts tab

- Start Point

- End Point

- Driver – pulls in drivers from the Driver tab

- Asset – pulls in assets from the Assets tab

For Solo 1 and Solo 2 routes, Copilot will automatically calculate the route's ending date and time based on the route type. Solo 1 routes have a set length of 14 hours. Solo 2 routes have a set length of 38 hours.

## Relay Load Board Routes

If a route has the route type of **RLB**, the following fields are required:

- Trip ID

- Start Date

- Start Time

- End Date

- End Time

- Start Point

- End Point

- Driver

- Asset

## Incremental Routes

- Block ID

- Start Date

- Start Time

- End Date

- End Time

- Start Point

- End Point

- Driver

- Asset

## Maintenance Routes

Maintenance (MAINT) routes record when assets are out for maintenance. Required fields:

- Start Date

- Start Time

- End Date

- End Time

- Start Point

- End Point

- Asset

---

# Contract, Driver, and Asset Fields

## Contracts

Contract start times can be selected if the contract's route type matches the route type of the route being scheduled.

## Drivers

Drivers can be selected if:

- The driver is configured to work the route type in the Driver Roster.

- The driver is not working another route or is not in their reset period during the duration of the route being scheduled.

- The driver will not be violating any other regulations by taking the route.

## Driver Priority Dropdown

To help you select the best driver for a route, eligible drivers are listed by priority based on how well their preferences match the route's date and time:

- **Green check mark:** Driver is **highly preferred** — the route's start time matches the driver's preferred shift start days and times.

- **Green calendar:** Driver is **preferred** — the route's starting day aligns with the driver's preferred shift start days.

- **Green clock:** Driver is **preferred** — the route's starting time aligns with the driver's preferred shift start times.

- **Greyed out:** Driver is not eligible for the route/block.

## Assets

Assets can be selected if:

- The asset is marked as available in the Assets tab.

- The asset is not assigned to another route (including Maintenance routes) during the duration of the route being scheduled.

