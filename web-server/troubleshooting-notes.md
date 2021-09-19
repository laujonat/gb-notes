# Troubleshooting Notes

In this scenario, I was unable to connect to my Digitalocean droplet via SSH  
  
Things I have tried

### Web Recovery Console

1. Power off the droplet and boot from the [recovery ISO](https://www.digitalocean.com/docs/droplets/resources/recovery-iso/)
2. Choose **6** for interactive shell \(don't mount or chroot\)
3. In the interactive shell,
   1. Mount the filesystem: "`mount /dev/vda1 /mnt`"
   2. Bind mount /dev: "`mount --bind /dev /mnt/dev`
   3. Bind mount /proc: "`mount --bind /proc /mnt/proc`"
   4. Bind mount /sys: "`mount --bind /sys /mnt/sys`"
   5. Chroot: "`chroot /mnt`"
   6. Update and upgrade: "`apt update`" and "`apt upgrade`"
4. Exit the interactive shell and restart the droplet to boot from main hard disk

Note that when using "`apt update`", previously broken installation automatically restarted.



### Ensure `/etc/resolve.conf` is present

```text
sudo apt-get install --reinstall resolvconf
```

[resolve.conf](https://bash.cyberciti.biz/guide//etc/resolv.conf) 

```text
nameserver 208.67.222.222 
nameserver 208.67.220.220
```





