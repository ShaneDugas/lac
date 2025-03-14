<div class="flex-container">
        <img src="https://github.com/ProfessionalLinuxUsersGroup/img/blob/main/Assets/Logos/ProLUG_Round_Transparent_LOGO.png?raw=true" width="64" height="64"></img>
    <p>
        <h1>Unit 3 Lab - LVM Fundamentals</h1>
    </p>
</div>

## Module 1: System Preparation and Basic Disk Operations

---

### Exercise 1.1: Environment Verification

Command line tools for disk wiping and/or partitioning in Linux:

- **fdisk:** A command-line utility ideal for MBR disks.
- **gdisk:** Similar to fdisk but for GPT disks.
- **parted:** A versatile tool that supports both MBR and GPT disks.

```bash
# Check system version
cat /etc/redhat-release

# Verify available disks
fdisk -l | grep -i xvd

# Check current disk usage
df -h

# Verify no existing LVM configuration
pvs
vgs
lvs
```

### Exercise 1.2: Disk Preparation

```bash
# Check disk status
lsblk /dev/xvdb
lsblk /dev/xvdc
lsblk /dev/xvdd

# Clear any existing partitions (if needed)
fdisk /dev/xvdb %3C< EOF
d
w
EOF

# Repeat for other disks if necessary
```

## Module 2: LVM Basics

---

### Exercise 2.1: Creating Physical Volumes

```bash
# Create individual PV
pvcreate /dev/xvdb

# Verify PV creation
pvs
pvdisplay /dev/xvdb

# Practice: Create remaining PVs
pvcreate /dev/xvdc
pvcreate /dev/xvdd

# Challenge: Create multiple PVs using a loop
for disk in b c d; do
    pvcreate /dev/xvd$disk
done
```

### Exercise 2.2: Volume Group Management

```bash
# Create a basic VG with one PV
vgcreate testvg1 /dev/xvdb

# Verify VG creation
vgs
vgdisplay testvg1

# Extend VG with additional PV
vgextend testvg1 /dev/xvdc

# Check VG size changes
vgs
```

## Module 3: Logical Volumes and File Systems

---

### Exercise 3.1: Basic LV Creation

```bash
# Create small LV
lvcreate -L 1G -n lvtest1 testvg1

# Verify LV creation
lvs
lvdisplay /dev/testvg1/lvtest1

# Create LV using percentage
lvcreate -l 50%FREE -n lvtest2 testvg1
Exercise 3.2: File System Operations
# Create ext4 filesystem
mkfs.ext4 /dev/testvg1/lvtest1

# Create mount point
mkdir /mnt/lvtest1

# Mount manually
mount /dev/testvg1/lvtest1 /mnt/lvtest1

# Verify mount
df -h /mnt/lvtest1
```

## Module 4: LVM Operations and Management

---

### Exercise 4.1: LV Expansion

```bash
# Expand LV
lvextend -L +500M /dev/testvg1/lvtest1

# Expand filesystem to match
resize2fs /dev/testvg1/lvtest1

# Verify new size
df -h /mnt/lvtest1
```

### Exercise 4.2: Persistent Mounting

```bash
# Add to fstab
echo "/dev/testvg1/lvtest1 /mnt/lvtest1 ext4 defaults 0 0" >> /etc/fstab

# Test fstab entry
umount /mnt/lvtest1
mount -a

# Verify mount persisted
df -h /mnt/lvtest1
```

## Practice Challenge

---

### Complete LVM Implementation

#### Create a production-like setup:

1. Create PVs using all available disks
2. Create a VG named 'prodvg'
3. Create two LVs:
   - 'apps_lv' (2GB)
   - 'data_lv' (remaining space)
4. Format with ext4
5. Mount with persistence
6. Verify all components

# PART 2: LVM with RAID

## Module 1: Understanding LVM RAID

---

### Exercise 1.1: LVM RAID Concepts

```bash
# View available RAID types
man lvmraid

# Check system RAID capabilities
dmsetup targets | grep raid
```

### Exercise 1.2: System Preparation

```bash
# Remove existing LVM configurations
# Save any important data before proceeding
umount /space 2>/dev/null
sed -i '/VolGroupTest/d' /etc/fstab

# Remove existing LVM structure
lvremove -f /dev/mapper/VolGroupTest-lv_test 2>/dev/null
vgremove -f VolGroupTest 2>/dev/null
pvremove /dev/xvd{b,c,d} 2>/dev/null

# Verify clean state
pvs
vgs
lvs
```

## Module 2: Basic RAID Configuration

---

### Exercise 2.1: Creating RAID-Ready Physical Volumes

```bash
# Create PVs individually to understand the process
pvcreate /dev/xvdb
pvcreate /dev/xvdc
pvcreate /dev/xvdd

# Verify PV creation
pvs
pvdisplay
```

### Exercise 2.2: Volume Group for RAID

```bash
# Create VG with all PVs
vgcreate VolGroupRAID /dev/xvdb /dev/xvdc /dev/xvdd

# Examine VG details
vgs
vgdisplay VolGroupRAID
```

## Module 3: RAID 5 Implementation

---

### Exercise 3.1: Creating RAID 5 Logical Volume

```bash
# Create RAID 5 LV using percentage of space
lvcreate --type raid5 -l 100%FREE -n lv_raid5 VolGroupRAID

# Examine RAID 5 configuration
lvs -a -o +devices
lvdisplay VolGroupRAID/lv_raid5
```

### Exercise 3.2: File System Operations

```bash
# Create XFS filesystem
mkfs.xfs /dev/VolGroupRAID/lv_raid5

# Create and prepare mount point
mkdir -p /space
chmod 755 /space

# Configure persistent mount
echo "/dev/VolGroupRAID/lv_raid5 /space xfs defaults 0 0" >> /etc/fstab
mount -a

# Verify mount
df -h /space
```

## Module 4: RAID Monitoring and Management

---

### Exercise 4.1: RAID Status Monitoring

```bash
# View RAID status
lvs -a -o +raid_sync_action,raid_mismatch_count

# Check detailed RAID info
lvdisplay VolGroupRAID/lv_raid5 -m

# Monitor RAID synchronization
while true; do
    lvs -a -o +raid_sync_action,sync_percent
    sleep 5
    clear
done
```

### Exercise 4.2: Performance Testing

```bash
# Write speed test
dd if=/dev/zero of=/space/test_file bs=1M count=1000 conv=fdatasync

# Read speed test
dd if=/space/test_file of=/dev/null bs=1M

# Clean up test file
rm -f /space/test_file
```

## Practice Challenge

---

## Complete RAID 5 Implementation

### Build a production-ready RAID 5 setup:

1. Create appropriate PVs
2. Create a VG named 'prodraid'
3. Create RAID 5 LV utilizing available space
4. Format with XFS
5. Configure persistent mounting
6. Implement basic monitoring
7. Document configuration

# PART 3: MDADM RAID

## Module 1: MDADM Foundations

---

### Exercise 1.1: Environment Setup

```bash
# Install mdadm package
dnf install mdadm -y

# Verify installation
mdadm --version

# Check current RAID arrays (if any)
cat /proc/mdstat
```

### Exercise 2.2: System Preparation

```bash
# Remove any existing configurations
umount /space 2>/dev/null
sed -i '/VolGroupTest/d' /etc/fstab

# Clear existing LVM
lvremove -f /dev/mapper/VolGroupTest-lv_test 2>/dev/null
vgremove -f VolGroupTest 2>/dev/null
pvremove /dev/xvd{b,c,d} 2>/dev/null

# Stop any existing RAID arrays
mdadm --stop /dev/md0 2>/dev/null
mdadm --zero-superblock /dev/xvd{b,c,d} 2>/dev/null
```

## Module 2: Basic RAID Operations

---

### Exercise 2.1: Creating a RAID 5 Array

```bash
# Create RAID 5 array
mdadm --create /dev/md0 --level=5 --raid-devices=3 /dev/xvdb /dev/xvdc /dev/xvdd

# Monitor creation progress
watch cat /proc/mdstat

# Examine RAID details
mdadm --detail /dev/md0
```

### Exercise 2.2: RAID Array Management

```bash
# View array status
cat /proc/mdstat

# Get detailed information
mdadm --detail /dev/md0

# Check array components
mdadm --examine /dev/xvd{b,c,d}
```

## Module 3: LVM Integration

---

### Exercise 3.1: LVM on RAID

```bash
# Create PV on RAID array
pvcreate /dev/md0

# Create VG
vgcreate VolGroupTest /dev/md0

# Create LV
lvcreate -l 100%FREE -n lv_test VolGroupTest

# Verify LVM structure
pvs
vgs
lvs
```

### Exercise 3.2: File System Setup

```bash
# Create XFS filesystem
mkfs.xfs /dev/VolGroupTest/lv_test

# Create mount point
mkdir -p /space
chmod 755 /space

# Configure mount
echo "/dev/VolGroupTest/lv_test /space xfs defaults 0 0" >> /etc/fstab
mount -a

# Verify mount
df -h /space
```

## Module 4: RAID Persistence and Monitoring

---

### Exercise 4.1: Making RAID Persistent

```bash
# Save RAID configuration
mdadm --detail --scan > /etc/mdadm.conf

# Verify configuration file
cat /etc/mdadm.conf

# Test configuration
mdadm --assemble --scan
```

### Exercise 4.2: Performance Testing

```bash
# Write performance test
dd if=/dev/zero of=/space/test_file bs=1M count=1000 conv=fdatasync

# Read performance test
dd if=/space/test_file of=/dev/null bs=1M

# Cleanup
rm -f /space/test_file
```

## Module 5: RAID Management Skills

---

### Exercise 5.1: RAID Monitoring

```bash
# Check RAID status
mdadm --detail /dev/md0

# Monitor sync progress
watch -n 1 cat /proc/mdstat

# View event log
journalctl | grep md0
```

### Exercise 5.2: RAID Array Maintenance

```bash
# Check array health
echo check > /sys/block/md0/md/sync_action

# View results
mdadm --detail /dev/md0
```

## Exercise 6.1: Production Setup

---

### Build a complete RAID 5 with LVM setup:

1. Create RAID 5 array with mdadm
2. Configure RAID persistence
3. Implement LVM on top of RAID
4. Create and mount XFS filesystem
5. Configure monitoring
6. Document configuration
7. Test performance
8. Create maintenance procedures
