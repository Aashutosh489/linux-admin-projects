Linux LVM (Logical Volume Management)

1. What is LVM?

LVM (Logical Volume Manager) is a method of managing disk storage space in Linux.
Instead of using a physical disk directly, LVM allows you to combine multiple disks into 
a single storage pool, and then create flexible partitions (called Logical Volumes) on 
top of it.
Advantages of LVM:
ï‚· Resize partitions easily (extend or reduce)
ï‚· Combine multiple disks into one large volume
ï‚· Better disk management for servers
Step 1: Check New Disk on the Server

When you attach a new disk to the Linux system, check if the system detects it.
Command 1:

`lsblk`

Explanation:
Shows block devices (disks and partitions) in a tree structure.
Example output:
NAME MAJ:MIN RM SIZE RO TYPE MOUNTPOINT
sda 8:0 0 40G 0 disk
â”œâ”€sda1 8:1 0 38G 0 part /
â””â”€sda2 8:2 0 2G 0 part [SWAP]
sdb 8:16 0 10G 0 disk
Here sdb is a new 10GB disk (unpartitioned).

Command 2:
`sudo fdisk -l`
Explanation:
Lists all disks and partitions with details like size, type, sector info.
Step 2: Create a Partition on the New Disk (optional)
If the new disk is completely free (like /dev/sdb), create a single LVM partition.

Command:
fdisk /dev/sdb
Inside fdisk:
create new partition
pí ¾í ¾í ¾â†’í ¾primary partition
1 â†’í ¾partition number
(press Enter for default sectors)
tí ¾í ¾í ¾â†’í ¾changeí ¾type
8eí ¾í ¾â†’í ¾LVMí ¾type
wí ¾í ¾í ¾â†’í ¾write and save
Then verify:
lsblk
âœ…You should see /dev/sdb1 created.

Step 3: Create Physical Volume (PV)
A PV is the base layer where LVM starts.
It marks the partition as usable by LVM.
Command:
pvcreate /dev/sdb1
Check PV status:
pvs
pvscan 
pvdisplay
Step 4: Create Volume Group (VG)
Command:
vgcreate vg1 /dev/sdb1
Check VG details:
Vgs
vgscan
vgdisplay
Step 5: Create Logical Volume (LV)
Logical Volumes are like partitions created inside a VG.
Example Command:
lvcreate -L 5G -n lvname vgname
Check LV details:
lvs
lvscan
lvdisplay
Step 6: Format and Mount LV
Format LV with a filesystem and mount it.
mkfs.ext4 lvpath
Mount FS
mkdir /dir1
mount lvpath dir
For Permanent Mount add entry in fstab file
Verify:
df -h
Step 7: Extend Logical Volume (LV)
Letâ€™say/project is running out of space and you want to extend by 2GB.
Command:
lvextend -L +2G /dev/vg_data/lv_project
Then resize filesystem:
sudo resize2fs /dev/vg_data/lv_project
Single Command
lvextend -L +2G /dev/vg_data/lv_project -r
âœ…Check updated size:
df -h
Step 8: Extend Volume Group (VG)
If your VG runs out of free space, you can add another disk.
Attach new disk /dev/sdc
Then:
pvcreate /dev/sdc1
vgextend vg_data /dev/sdc1
Check updated VG info:
vgs
