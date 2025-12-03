# Attach / Detach Disks & Snapshots

## Attach a data disk  
1. Portal → Compute → Virtual Machines → select VM.  
2. Go to **Disks** tab → click **Attach disk**.  
3. Select existing disk or create new data disk (select size/type).  
4. Click **Attach** and wait until state changes to “Active”.

## Create snapshot  
1. Portal → Disks → select disk → **Create snapshot**.  
2. Provide snapshot name → click **Create**.  
3. Use this snapshot to create custom image or restore disk.

## Detach a data disk  
1. Select VM → Disks tab → select data disk → **Detach**.  
2. Confirm → wait until disk is detached.

## Restore from snapshot  
1. Snapshot list → select snapshot → **Create disk from snapshot**.  
2. Attach new disk to VM as above.
