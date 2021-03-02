# pve-mub
Proxmox VE multi-user box - configuration and hookscripts for hosting multiple simultaneous virtual machines with hardware passthrough for multiple users

# The Standard Disclaimer™
pve-mub (hereafter "THE SOFTWARE") is provided AS-IS, without any warranty, express or implied. Notwithstanding provisions in the license, any risk from use of THE SOFTWARE is assumed by the user, and the author and/or owner of THE SOFTWARE is hereby held blameless for any damages or any other liability arising from use of THE SOFTWARE.

# Hardware configuration
pve-mub is primarily developed for the following hardware configuration:
- AMD Ryzen 9 3950x (16c/32t)
- Gigabyte x570 Aorus Ultra
- 128 GB DDR4-3600 RAM (4 x 32 GB)
- 4 TB NVME in zraid (2 TB usable) for PVE and guest disks (2 x 2 TB)
- 32 TB SATA in zraid (24 TB usable) for long-term misc storage (4 x 8 TB)
- Intel 82580 4-port PCIE network adapter
- 2 x EVGA nVidia GeForce RTX 2060 SUPER


This hardware supports a number of end-user virtual machines limited by the number of available GPUs, each configured with:
- 8 virtual CPUs
- 24 GB RAM
- 320 GB system disk
- 1 physical network port
- 1 physical GPU
- a subset of the host's physical USB ports
