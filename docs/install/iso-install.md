---
sidebar_position: 1
keywords:
  - Harvester
  - harvester
  - Rancher
  - rancher
  - ISO Installation
Description: To get the Harvester ISO, download it from the Github releases. During the installation you can either choose to form a new cluster, or join the node to an existing cluster.
---

# ISO Installation

To get the Harvester ISO, download it from the [Github releases.](https://github.com/harvester/harvester/releases)

During the installation you can either choose to form a new cluster, or join the node to an existing cluster.

Note: This [video](https://youtu.be/97ADieBX6bE) shows a quick overview of the ISO installation.

<div class="text-center">
<iframe width="950" height="475" src="https://www.youtube.com/embed/97ADieBX6bE" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>

1. Mount the Harvester ISO disk and boot the server by selecting the `Harvester Installer`.
   ![iso-install.png](iso-install.png)
1. Choose the installation mode by either creating a new Harvester cluster, or by joining an existing one.
1. Choose the installation device that the Harvester will be formatted to.
1. Configure the hostname and select the network interface for the management network, the IP address can either be configured via DHCP or static method.
   ![iso-installed.png](iso-nic-config.png)
1. Configure the `cluster token`. This token will be used for adding other nodes to the cluster.
1. Configure the login password of the host. The default ssh user is `rancher`.
1. (Optional) you can choose to import SSH keys from a remote URL server. Your GitHub public keys can be used with `https://github.com/<username>.keys`.
1. (Optional) If you need to use an HTTP proxy to access the outside world, enter the proxy URL address here, otherwise, leave this blank.
1. (Optional) If you need to customize the host with cloud-init config, enter the HTTP URL here.
1. Confirm the installation options and the Harvester will be installed to your host. The installation may take a few minutes to be complete.
1. Once the installation is complete it will restart the host and a console UI with management URL and status will be displayed. (You can Use F12 to switch between Harvester console and the Shell)
1. The default URL of the web interface is `https://your-host-ip:30443`.
   ![iso-installed.png](iso-installed.png)
1. User will be prompted to set the password for the default `admin` user on the first-time login.
   ![first-login.png](first-log-in.png)

## Troubleshooting

### {partitions} have been written, but we have been unable to inform the kernel of the change...

Check your server user manual, you may need to disable write protection or use a bios-level boot option to specify installation of an operating system and its media.
It may also help to format drives ahead of time, if there was already an operating system installed to the drive.

### Blank screen during isolinux-based installation

For some older machines, the installation media may appear to boot to a blank screen prior to the "Choose installation mode" screen as seen above.  In this case, additional parameters may need to be specified to the bootloader.

ISOlinux: Press TAB during the countdown to "view available boot entries" and initiate a command prompt. If VGA is displayed as a boot entry, specify nomodeset with `vga nomodeset`, and press enter to continue installation.

Grub: Press e to enter a command line, and add the instruction `nomodeset text`

### starting kubernetes: preparing server: init cluster datastore and https: no default routes found in "/proc/net/route" or "/proc/net/ipv6_route"

The installation media may not use the same NIC interface names. In this case, during the bootloader press e
https://github.com/harvester/harvester/issues/1200
