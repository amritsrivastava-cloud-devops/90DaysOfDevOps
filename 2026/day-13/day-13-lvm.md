# Day 13 – Linux Volume Management (LVM)

### Commands Used 
- pvcreate /dev/<select-your-disk> (Creates physical volume)
- vgcreate volume-group-name /dev/<select-your-disk> (Creates volume group)
- lvcreate -L size(G,M) -n logic-volume-name volume-group-name (Creates logical volume)
- mkfs.ext4 (format logical volume)
- mkdir -p /mnt/logic-volume-name
- mount (mount your disk)
- umount (unmount your disk)
- lvextend (extend volume )
- resize2fs (apply extend to filesystem)
- lsblk (list block devices)
- df -h (file system usages)

### Challenge Tasks

#### Task 1: Check Current Storage
Run: `lsblk`, `pvs`, `vgs`, `lvs`, `df -h`

#### Task 2: Create Physical Volume
```bash
pvcreate /dev/sdb   # or your loop device
pvs
```
#### Task 3: Create Volume Group
```bash
vgcreate devops-vg /dev/sdb
vgs
```
#### Task 4: Create Logical Volume
```bash
lvcreate -L 500M -n app-data devops-vg
lvs
```
#### Task 5: Format and Mount
```bash
mkfs.ext4 /dev/devops-vg/app-data
mkdir -p /mnt/app-data
mount /dev/devops-vg/app-data /mnt/app-data
df -h /mnt/app-data
```

<img width="973" height="996" alt="image" src="https://github.com/user-attachments/assets/56ac84cb-7483-490a-bd66-a331e01fa24c" />

#### Task 6: Extend the Volume
```bash
lvextend -L +200M /dev/devops-vg/app-data
resize2fs /dev/devops-vg/app-data
df -h /mnt/app-data
```

<img width="1003" height="974" alt="image" src="https://github.com/user-attachments/assets/bcdead0b-70b1-45dd-8d24-2d7f4540d229" />


