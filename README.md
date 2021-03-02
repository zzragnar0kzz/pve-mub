# pve-mub
Proxmox VE multi-user box - configuration and hookscripts for hosting multiple simultaneous virtual machines with hardware passthrough for multiple users

# Hardware configuration
pve-mub is primarily developed for the following hardware configuration:
- AMD Ryzen 9 3950x
- Gigabyte x570 Aorus Ultra
- 128 GB DDR4-3600 (4 x 32 GB)
- 4 TB NVME in zraid (2 TB usable) for PVE and guest disks (2 x 2 TB)
- 32 TB SATA in zraid (24 TB usable) for long-term misc storage (4 x 8 TB)
- Intel 82580 4-port PCIE network adapter
- 2 x EVGA nVidia GeForce RTX 2060 SUPER
