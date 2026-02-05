# # Day 13 – Linux Volume Management (LVM)

## Challenge Tasks

### Task 1: Check Current Storage
Run: `lsblk`, `pvs`, `vgs`, `lvs`, `df -h`

### Task 2: Create Physical Volume
```bash
pvcreate /dev/sdb   # or your loop device
pvs
```
### Task 3: Create Volume Group
```bash
vgcreate devops-vg /dev/sdb
vgs
```
### Task 4: Create Logical Volume
```bash
lvcreate -L 500M -n app-data devops-vg
lvs
```
### Task 5: Format and Mount
```bash
mkfs.ext4 /dev/devops-vg/app-data
mkdir -p /mnt/app-data
mount /dev/devops-vg/app-data /mnt/app-data
df -h /mnt/app-data
```

<img width="973" height="996" alt="image" src="https://github.com/user-attachments/assets/56ac84cb-7483-490a-bd66-a331e01fa24c" />

### Task 6: Extend the Volume
```bash
lvextend -L +200M /dev/devops-vg/app-data
resize2fs /dev/devops-vg/app-data
df -h /mnt/app-data
```

<img width="1003" height="974" alt="image" src="https://github.com/user-attachments/assets/bcdead0b-70b1-45dd-8d24-2d7f4540d229" />

+-------------------------------+
| Application Layer |
| (Apps, Databases, Users) |
+---------------▲---------------+
|
+---------------|---------------+
| Mount Point |
| /, /var, /home, /data |
+---------------▲---------------+
|
+---------------|---------------+
| Filesystem |
| ext4 / xfs |
+---------------▲---------------+
|
+---------------|---------------+
| Logical Volume (LV) |
| /dev/devops-vg/app-data |
+---------------▲---------------+
|
+---------------|---------------+
| Volume Group (VG) |
| devops-vg |
+---------------▲---------------+
|
+---------------|---------------+
| Physical Volume (PV) |
| /dev/sdb1, /dev/nvme1n1|
+---------------▲---------------+
|
+---------------|---------------+
| Partition Table (GPT/MBR) |
| /dev/sdb1, nvme0n1p1 |
+---------------▲---------------+
|
+---------------|---------------+
| Physical Disk / EBS |
| SSD / HDD / AWS EBS |
+-------------------------------+

Disk/EBS
└── Partition
└── PV (pvcreate)
└── VG (vgcreate)
└── LV (lvcreate / lvextend)
└── Filesystem (mkfs / resize2fs)
└── Mount Point

Physical Disk (EBS / SSD)
↓
Partition (/dev/nvme0n1p1)
↓
Physical Volume (PV)
↓
Volume Group (VG)
↓
Logical Volume (LV)
↓
Filesystem (ext4 / xfs)
↓
Mount Point (/mnt/app-data)
