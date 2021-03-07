# pve-mub
Proxmox VE multi-user box - configuration and hookscripts for hosting multiple simultaneous virtual machines with hardware passthrough for multiple users
## PVE Configuration
stub
## Hookscripts
`pve-mub-hooks` is a set of hookscripts that perform a variety of actions at various lifecycle phases of a VM, including:
- Post-start:
  - Pin guest vCPUs to a set of specific host cores
  - Pin interrupts from any PCI devices which have been passed through to a guest to a set of specific host cores
  - Limited ability to adjust the host scheduler's policy and priority values for threads associated with a guest
  - Define or disable the host's halt poll period
### Installation
1. The current version of the hookscript is located [here](https://github.com/zzragnar0kzz/pve-mub/blob/main/pve-mub-hooks). Download it using your preferred method, and place it in the PVE host's local storage, for example `/var/lib/vz`, or a subfolder therein.
2. Verify that the execute bit is set on the hookscript file; you may need to set this manually.
### Configuration
Examples in this section will use `123` as the target VM's ID, and `local:/snippets/pve-mub-hooks` as the hookscript's path. Adjust these to your needs.
1. Configure the target VM to use the hookscript: `qm set 123 -hookscript local:snippets/pve-mub-hooks`
2. Create a hookscript configuration file for the target VM. This file must have a name matching the target VM's ID, with a `.hookconf` extension. A sample configuration file is located [here](https://github.com/zzragnar0kzz/pve-mub/blob/main/sample.hookconf). Download it using your preferred method, and rename it so that it matches the target VM's ID. Place it in the same location where the target VM's configuration file can be found; for example, if the target VM's configuration file is located at `/etc/pve/qemu-server/123.conf`, then the hookscript configuration file should be located at `/etc/pve/qemu-server/123.hookconf`.
3. Change settings in the hookscript configuration file as needed for the target VM. A brief description of all valid options can be found in the sample configuration file, with examples of their usage.
4. Launch the target VM; if it is already running, it may need to be rebooted, or shutdown and restarted, from the host.
### Known Issues
- The path to VM configuration files, and thus hookscript configuration files, is currently hardcoded to `/etc/pve/qemu-server`; this needs to be changed.

# Credits
- Proxmox forum thread [CPU pinning?](https://forum.proxmox.com/threads/cpu-pinning.67805/); specifically, [this post](https://forum.proxmox.com/threads/cpu-pinning.67805/#post-304715) for inspiration in regards to vCPU pinning and isolating configuration options in a separate file.
- Proxmox forum thread [How to set Linux scheduling priority of a VM on start?](https://forum.proxmox.com/threads/how-to-set-linux-scheduling-priority-of-a-vm-on-start.47185/) and a [related Reddit thread](https://www.reddit.com/r/Proxmox/comments/9gv8js/how_to_set_linux_scheduling_priority_of_a_vm_on/) for inspiration in regards to scheduler policy/priority and expanding beyond a single hook.
- [Proxmox VE Helpers](https://github.com/ayufan/pve-helpers) for inspiration in regards to pinning device interrupts and setting the halt poll time.

# Hardware configuration
pve-mub is primarily developed for the following hardware configuration:
- AMD Ryzen 9 3950x (16c/32t)
- Gigabyte x570 Aorus Ultra
- 128 GB DDR4-3600 RAM (4 x 32 GB)
- 4 TB NVME SSD in zraid (~ 2 TB usable) for PVE and guest disk images (2 x 2 TB)
- 32 TB SATA HDD in zraid (~ 24 TB usable) for miscellaneous storage (4 x 8 TB)
- Intel 82580 4-port PCIE network adapter
- 2 x EVGA nVidia GeForce RTX 2060 SUPER


This hardware supports a number of simultaneous end-user virtual machines limited by host IOMMU groupings and by the number of available GPUs. Each such VM is configured with:
- 8 virtual CPUs
- 24 GB RAM
- 320 GB system disk image
- 1 physical network port
- 1 physical GPU
- a subset of the host's physical USB ports


Remaining hardware resources are available to ancilliary virtual machines and services, and to the host.

The PVE host configuration can likely be adapted to other hardware; YMMV with the results of such endeavors.

# The Standard Disclaimer™
pve-mub © 2021 Jeff Guziak. All rights reserved.


pve-mub is provided under the terms of the [GNU General Public License v3.0](https://github.com/zzragnar0kzz/pve-mub/blob/main/LICENSE).


pve-mub (hereafter "THE SOFTWARE") is provided AS-IS, WITHOUT ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE. Notwithstanding any provisions contained in the license, IN NO EVENT SHALL THE AUTHOR, OWNER, COPYRIGHT HOLDER, AND/OR CONTRIBUTORS BE HELD LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THE SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.


As determined by the AUTHOR, OWNER, and/or COPYRIGHT HOLDER of THE SOFTWARE at their sole discretion, helpful solicitations of any kind regarding THE SOFTWARE will be given due consideration, and unhelpful solicitations of any kind will be summarily ignored.
