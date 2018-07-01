# delay-oom-killer-in-linux-deb-dists
HISTORY:
To get DC/OS running, I ran into the issue that the OOM-Killer in my deb-dist killed one or more vurtual machines completely to free some memory to stay alive, so my generated cluster was never really that usable as a cluster.
I could have reduced the memory amount on each cluster's node, but since I wanted to get, with others, HDFS up and running, this was no option.
My aim was to have a 'mobile' cluster on my 32G Laptop and a memory upgrade is not possible since this was the most I could add.
So I googled around and found many pro's and con's for zswap and zram on itself, but also on running them seperately or together on one machine.
Than, I decided to find How-To's to configure zram and aslo zswap and doing my own investigations.

CONCLUSION/EXPERIENCE:
ZRAM and ZSWAP can do a very good job each with another. It really depends on their/each one's configuration.

AIM:
This repo wants to give you some hints on keeping a system still alive when memory and/or swap space is seemingly fully crowded / filled at the beginning.

It will also give you some possibilities on 'fine-tuning' those meassures with different options; but will of course not give you the possibility to have an 32GB-app running on a 16GB system.

These measures will only delay and keep your system alive/breathable until a special point, but will never avoid oom killing one of your memory intensive proceses.

Sources from where those basic scripts are derived from are also given for reference.

There will be two ways for integratiing the zram option and one way on manually activate zswap on your distribution.

1st)
Lets see how to activate zswap on all latest, but not only, deb-based linux distributions:

- open '/etc/default/grub' as root for editing
- add to this line: 'GRUB_CMDLINE_LINUX_DEFAULT='..' the following boot options at its end:
  'zswap.enabled=1 zswap.compressor=lzo zswap.pool=zbud'
  This will enable zswap automatically without loading the zswap module manually.
- Test these options on an non-productive system and monitor how it behaves

Additionally the compressor-type, percentage of used mem and so an can be changed/added here.
See also:
https://wiki.archlinux.org/index.php/zswap

Above mentioned options should/will work from kernel 3.2.36 onwards.

2nd)
Scripts for using zram on systemv-init and systemd-init like systems:
First you will to have find out, what kind of init-system your dist is running on:
Try these commands to find out:rogiwankenobi@jessie:/etc/systemd/system$ which systemd

'man init' this should guide you directly to the system`s 'systemd' manpage on a systemd-init system.

This should give you the first hint on a systemd-init system.
Additionally you can do:

rogiwankenobi@:/etc/systemd/system$ which systemd
/bin/systemd

Also you can verify this be googling around for your special distro, AND , maybe, you can tell from experience since, e.g., a Centos dist is definetely has a systemd-based init system. 
It is not very cleary to find out, in my eyes.

For Debian you can definately say, since Debian-9 the systemd-init systems is used, while until bebian-8.10, also with a newer kernel from the backports-repo, also systemv-init system can be used; the systemd-system is not completely switched here.

Further hints on How-To for zram integration on systemd-init and systemv-init system you will find in my WIKI part.
