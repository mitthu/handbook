# Migration
## Rsync (hd1 =to=> hd2)
```bash
rsync -avr --exclude-from=/srv/exclude /mnt/hd1/hd1/ /mnt/hd2/hd2/
```

