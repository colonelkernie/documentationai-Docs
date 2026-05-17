# Time Off Tracker

> Keep track of your drivers' time off

**Source:** https://help.laminarcopilot.com/en/articles/12120421-time-off-tracker  
**Collection:** Solutions > Managing Drivers  
**Last Updated:** August 30, 2025

---

## Track Driver Time-Off Records in Copilot

Copilot's Time Off Tracker allows you to input and keep record of all your drivers' requests to take time off from their regular working days. Copilot will take all Time Off records into account when running Dynamic Scheduler and determining driver eligibility for a route.

## Create a New Time Off Record

To access the Time Off Tracker, navigate to the **Team Management tab** in the left navigation and click **Time Off Tracker**.

When creating a new Time Off record, you can categorize the **type of Time Off** *(required field)*:

- Paid Time Off
- Unpaid Time Off
- Accommodation

**Note:** These Time Off types are only for your reference and will not impact any scheduling functionality.

Fill out the remaining fields and save changes:

- Team Member *(required)*
- Start Time *(required)*
- End Time *(required)*
- Comments *(optional)*

After a record has been created, you can **only edit the Comments field**. If you need to update any other field, you'll need to delete the record and re-create it.

## Viewing All Time Off Records

The Time Off Tracker comes with two views: a **List view** and a **Calendar view**.

- The **List view** shows a list of all Time Off records you've created.
- The **Calendar view** shows all Time Off records in a monthly view. The Calendar view defaults to the current month, but you can use the dropdown to navigate to different months.

In the Calendar view, you can click on a Time Off block to edit the record.

## Scheduling with Time Off Records

### Dynamic Scheduler

When you import your routes via CSV and run Dynamic Scheduler, Copilot will take all Time Off records into account. Copilot will not schedule drivers to routes that fall on the day(s) of their Time Off record(s).

### Driver Eligibility

When creating or editing a route, the assigned driver dropdown will not allow you to select a driver if that driver has a Time Off record that would conflict with the route.
