# Home Server
## Overall Setup
### Monitoring (Hard disks)
- Monitor smart status for any reallocated disks
- Monitor overall smart status for OK
- Monitor temperature of disks
- Monitoring power usage of all disks
- Monitoring rpm of disks
- Monitoring I/O of all disks

### Monitoring (Others)
- CPU temperature
- CPU Fan RPM
- Cabinet Fan RPMs
- Cabinet Temperature

### Misc.
- Use NTP to keep time in sync
- Note down all component details like hardisk serial numbers, etc.
- Activate write cache when harddisk supports it
- Logrotate and stuff... (read all crons from /etc backup)


## Utils
```bash
# Start a VNC server
tightvncserver -geometry 1366x768

# Partition using (4K hardisks)
# Verify using: Disk Utility (palimpsest)
gdisks

# Run ansible playbook
ansible-playbook -i hosts -u mitthu homeserver.yml
```

## Encrypted Disks
```bash
# Create key file
# Ref: https://www.martineve.com/2012/11/02/luks-encrypting-multiple-partitions-on-debianubuntu-with-a-single-passphrase/
sudo dd if=/dev/urandom of=/root/newkeyfile bs=1024 count=4

# Add keyfile to an existing luks partition
sudo cryptsetup luksAddKey /dev/sda1 /root/keyfile

# /etc/crypttab entry
# <target name>	<source device>		<key file>	<options>
hdd1	/dev/sda1	/root/keyfile	luks

# Test the /etc/crypttab entry
# Ref: http://askubuntu.com/questions/5861/etc-crypttab-not-working
sudo cryptdisks_start hdd1

# Entry in /etc/fstab
/dev/mapper/hdd1	/media/hdd1	auto	defaults,user	0	0

# Manually start open an encrypted vol
cryptsetup luksOpen /dev/sda1 hdd1
mount /dev/mapper/hdd1 /media/hdd1

# Manually stop an encrypted vol
umount /media/hdd1
cryptsetup luksClose hdd1
```

### Luks backups and restore
```bash
# Ref: https://wiki.archlinux.org/index.php/Dm-crypt/Device_encryption#Backup_and_restore
# Precursor
mkdir -p /srv/backups/luks

# Backup
sudo cryptsetup luksHeaderBackup /dev/sdd1 --header-backup-file /srv/backups/luks/sdd1.img

# Check backup
sudo cryptsetup -v --header /srv/backups/luks/sdd1.img open /dev/sdd1 hdd4test
ls /dev/mapper # Should list hdd4test
sudo cryptsetup luksClose hdd4test

# Restore
sudo cryptsetup luksHeaderRestore /dev/sdd1 --header-backup-file /srv/backups/luks/sdd1.img
```
