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
