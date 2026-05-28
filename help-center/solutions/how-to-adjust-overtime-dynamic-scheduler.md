---
title: How to Adjust How Much Overtime Dynamic Scheduler Assigns Drivers
description: >-
  This guide explains how to control how much overtime Dynamic Scheduler is
  allowed to use when assigning routes by enabling Custom Weekly Shift Hours and
  applying it to specific drivers.
---
## Overview

By default, Dynamic Scheduler follows preset weekly shift hour limits when assigning routes. The **Custom Weekly Shift Hours** feature allows your team to raise that limit at the company level and selectively apply it to individual drivers, giving you more flexibility during high-volume weeks.

---

## Default Weekly Shift Hour Limits

Before using this feature, it's helpful to understand the standard limits Dynamic Scheduler uses:

- **42 hours** for all drivers

- **56 hours** if any of the following apply:

  - The driver is **Solo 2 only**

  - The driver is assigned to a **4x4 contract**

  - Your carrier only operates **Solo 2 contracts**

Dynamic Scheduler will always respect these defaults unless Custom Weekly Shift Hours is enabled.

---

## Step 1: Enable Custom Weekly Shift Hours at the Company Level

Custom Weekly Shift Hours is configured in **Company Settings** and applies across your organization.

1. Go to **Company Settings**

2. Navigate to **Scheduling Features**

3. Find **Custom Weekly Shift Hours**

4. Toggle the setting **On**

5. Click **Edit** to open the configuration drawer

6. Enter your desired weekly shift hour limit

7. Save your changes

### Validation Rules

- Minimum value: **56 hours**

- Maximum value: **70 hours**

- The field cannot be empty

Once saved, the custom value will be displayed next to the toggle.

**Important:** Enabling this setting does not automatically increase hours for all drivers. You must apply it to individual drivers in the next step.

---

## Step 2: Apply Custom Weekly Shift Hours to Specific Drivers

After setting a company-wide overtime limit, you can choose which drivers are allowed to use it.

1. Open the driver's profile

2. Click **Edit**

3. Locate **Use Custom Weekly Shift Hours**

4. Select **Yes** to allow this driver to exceed default limits (up to the custom value)

5. Save the driver record

Drivers set to **No** will continue to follow the default weekly shift hour rules.

---

## How Dynamic Scheduler Uses Custom Weekly Shift Hours

When importing routes, Dynamic Scheduler applies overtime rules in two phases:

1. **Primary pass** — Routes are assigned to all drivers using **default weekly limits** first.

2. **Secondary pass** — If routes remain unassigned, Dynamic Scheduler assigns additional routes **only** to drivers with **Custom Weekly Shift Hours enabled**, up to the configured limit.

This ensures overtime is used intentionally and only when necessary.

---

## When to Use This Feature

Custom Weekly Shift Hours is best used when:

- Peak volume weeks require additional driver utilization

- You want tighter control over which drivers can take on extra hours

- You want to avoid globally increasing overtime exposure

---

## Need Help?

If you're unsure how to configure this feature for your operation or are seeing unexpected scheduling behavior, contact the **Laminar Copilot Support Team** for assistance.
