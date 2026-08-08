# Day 13 – Linux Volume Management (LVM)

## Task
Learn LVM to manage storage flexibly — create, extend, and mount volumes.

---

## Challenge Tasks

### Task 1: Check Current Storage
```
lsblk
pvs
vgs
lvs
df -h
```

### Task 2: Create Physical Volume
```
pvcreate /dev/sdb   # or your loop device
pvs
```

### Task 3: Create Volume Group
```
vgcreate devops-vg /dev/sdb
vgs
```

### Task 4: Create Logical Volume
```
lvcreate -L 500M -n app-data devops-vg
lvs
```

### Task 5: Format and Mount
```
mkfs.ext4 /dev/devops-vg/app-data
mkdir -p /mnt/app-data
mount /dev/devops-vg/app-data /mnt/app-data
df -h /mnt/app-data
```

**Tasks 1–5 output** *(commands marked red, responses marked green for visibility):*

*[screenshot: LVM setup — tasks 1 through 5]*

### Task 6: Extend the Volume
```
lvextend -L +200M /dev/devops-vg/app-data
resize2fs /dev/devops-vg/app-data
df -h /mnt/app-data
```

*[screenshot: volume extension]*

---

## Real Flow (on AWS EC2)

1. Added a 4GB EBS volume to the EC2 instance
2. Verified disk: `lsblk`
3. Created Physical Volume:
   ```
   sudo pvcreate /dev/xvdf
   pvs
   ```
4. Created Volume Group — creates `devops-vg` under `/dev/`:
   ```
   sudo vgcreate devops-vg /dev/xvdf
   vgs
   ```
5. Created Logical Volume — creates `app-data` under `/dev/devops-vg/`:
   ```
   sudo lvcreate -L 2G -n app-data devops-vg
   lvs
   ```
6. Formatted the volume:
   ```
   sudo mkfs.ext4 /dev/devops-vg/app-data
   ```
7. Mounted the volume:
   ```
   sudo mkdir -p /mnt/app-data
   sudo mount /dev/devops-vg/app-data /mnt/app-data
   ```
8. Verified mount: `df -h`
9. Extended the Logical Volume:
   ```
   sudo lvextend -L +1G /dev/devops-vg/app-data
   sudo resize2fs /dev/devops-vg/app-data
   ```
10. Verified updated size: `df -h`

---

## Explanation, Step by Step

### Step 0: AWS Disk
Attached a new 4GB disk via EBS on AWS to the EC2 instance. Linux sees it as `/dev/nvme1n1`.

**`lsblk`** — shows all disks; confirms the new disk exists.

### Step 1: `pvcreate`
```
pvcreate /dev/nvme1n1
```
Converts a raw disk into a **Physical Volume (PV)**. Think: *"make this disk usable for LVM."*

**`pvs`** — shows all PVs.

### Step 2: `vgcreate`
```
vgcreate devops-vg /dev/nvme1n1
```
Creates a **Volume Group (VG)**. Think: *"create a storage pool from the disk."*

**`vgs`** — shows available storage pools.

### Step 3: `lvcreate`
```
lvcreate -L 2G -n app-data devops-vg
```
Creates a **Logical Volume (LV)**. Think: *"create a partition from the pool."*
- `-L 2G` → exact size (2GB)
- `-n app-data` → name
- `devops-vg` → source pool

**`lvs`** — shows logical volumes.

### Step 4: `mkfs.ext4`
```
mkfs.ext4 /dev/devops-vg/app-data
```
Formats the volume. Think: *"prepare it like a new drive"* — without this, no files can be stored.

### Step 5: Mount
```
mkdir -p /mnt/app-data
mount /dev/devops-vg/app-data /mnt/app-data
```
Makes the storage usable. Think: *"attach disk to folder."* Now `/mnt/app-data` is usable storage.

### Step 6: Verify
```
df -h
```
Shows mounted disks, sizes, and usage.

### Step 7: Extend Volume (the main power move)
```
lvextend -L +1G /dev/devops-vg/app-data
```
Increases size by 1GB — but the filesystem itself is still the old size at this point.

### Step 8: Resize Filesystem
```
resize2fs /dev/devops-vg/app-data
```
Expands the filesystem to actually use the new space — like refreshing it to reflect the change.

### Final Check
```
df -h
```
Size now shows increased. ✅

---

## Full Flow

```
AWS Disk (/dev/nvme1n1)
        ↓
Physical Volume (pvcreate)
        ↓
Volume Group (vgcreate)
        ↓
Logical Volume (lvcreate)
        ↓
Format (mkfs)
        ↓
Mount (mount)
        ↓
Extend (lvextend + resize2fs)
```
