# Configuring Program Lists and Automated Broadcasting

**Last Updated:** 2025-12-19

Live Video Caster (LVC) allows you to configure scheduled broadcasting. Schedules automate when programs go live, switch, and stop without manual intervention.

---

## Prerequisites

- Input sources have been added  
- Directing & editing completed  

---

# 1. Enter the Caster

![IMG-01 Caster List Page](images/lvc-01-caster-list.png)

**Description:**  
Displays all casters. Selecting **ID** or **Open** enters the editing interface for schedule configuration.

---

# 2. Open Schedule Panel

![IMG-02 Schedule Panel Button](images/lvc-02-open-schedule-panel.png)

**Description:**  
Opens the scheduling system where automated playout rules are managed.

---

# 3. Create Schedule — Entry

![IMG-03 Create Schedule Popup](images/lvc-03-create-schedule-popup.png)

**Description:**  
Launches the schedule creation workflow.

---

## Schedule Basic Information

![IMG-04 Schedule Basic Info Fields](images/lvc-04-schedule-basic-info.png)

| Item | Description |
|------|-------------|
| Schedule Name | Identifier (≤10 characters) |
| Start Time | When automated broadcasting begins |
| End Time | When broadcasting stops |
| Switch Audio/Video Together | Controls background audio logic |

**System Behavior:**  
At the start time, LVC automatically enables PGM output.

---

# 4. Add Program Panel

![IMG-05 Add Program Empty State](images/lvc-05-add-program-empty.png)

**Description:**  
Shows an empty schedule ready to receive program entries.

---

## Program Configuration

![IMG-06 Program Configuration Form](images/lvc-06-program-config-form.png)

| Item | Description |
|------|-------------|
| Program Name | Identifier (≤10 characters) |
| Stream Time | When program plays |
| Program Type | Source or layout |
| Watermark | Up to 5 overlays |
| Text | Up to 5 text overlays |

---

# 5. Add Program to Schedule

![IMG-07 Add to Schedule Button](images/lvc-07-add-to-schedule.png)

**Description:**  
Commits the program into the schedule timeline.

![IMG-08 Program Added List](images/lvc-08-program-added.png)

**Description:**  
Shows programs now sequenced in the schedule.

---

# 6. Save Schedule

![IMG-09 Schedule Save Screen](images/lvc-09-schedule-save.png)

**Description:**  
Finalizes schedule creation and stores configuration.

> ⚠ Stream times must be future times.

---

# 7. Edit Existing Schedule

![IMG-10 Schedule Edit Entry](images/lvc-10-edit-schedule-entry.png)

**Description:**  
Access point to modify an existing schedule.

![IMG-11 Schedule Edit Panel](images/lvc-11-edit-schedule-panel.png)

**Description:**  
Allows updating schedule timing and switching behavior.

---

# 8. Edit Program

![IMG-12 Program Edit Button](images/lvc-12-edit-program.png)

**Description:**  
Initiates editing of an individual program.

![IMG-13 Program Edit Panel](images/lvc-13-program-edit-panel.png)

**Description:**  
Modify content, overlays, or timing of that program.

---

# 9. Delete Program

![IMG-14 Program Delete Button](images/lvc-14-delete-program.png)

**Description:**  
Removes the selected program from the schedule.

---

# 10. Change Program Content

![IMG-15 Change Program Source](images/lvc-15-change-program.png)

**Description:**  
Allows switching to a different source/layout without deleting the entry.

---

# 11. Save After Editing

![IMG-16 Save Edited Schedule](images/lvc-16-save-edits.png)

**Description:**  
Applies all edits to the schedule.

---

# 12. Delete Schedule

![IMG-17 Delete Schedule Button](images/lvc-17-delete-schedule.png)

![IMG-18 Delete Confirmation Popup](images/lvc-18-delete-confirm.png)

**Description:**  
Permanently removes schedule.

> ⚠ Deleted schedules cannot be recovered.

---

# 13. Insert Schedule

![IMG-19 Insert Schedule Button](images/lvc-19-insert-schedule.png)

**Description:**  
Creates an additional schedule block.

---

# 14. Close Schedule Panel

![IMG-20 Close Schedule Panel](images/lvc-20-close-panel.png)

**Description:**  
Closes scheduling UI without deleting schedules.

---

# 15. Enable Scheduled Broadcasting

![IMG-21 Enable Schedule Toggle](images/lvc-21-enable-schedules.png)

![IMG-22 Enable Confirmation Popup](images/lvc-22-enable-confirm.png)

**System Behavior**

| Event | Action |
|------|-------|
| Schedule Start | PGM activates |
| Program Time | LVC switches program |
| Schedule End | PGM stops |

---

# 16. Disable Scheduled Broadcasting

![IMG-23 Disable Toggle](images/lvc-23-disable-toggle.png)

![IMG-24 Disable Confirmation](images/lvc-24-disable-confirm.png)

**Description:**  
Stops automated playout.

---

## Operational Notes

- Disabling schedules mid-run stops switching  
- Billing occurs while PGM is active  
- Turn off schedules + PGM to stop charges
