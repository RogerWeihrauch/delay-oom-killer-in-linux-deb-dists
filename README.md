# delay-oom-killer-in-linux-deb-dists
repo on meassures to avoid / delay the out-of-memory killer in (mainly) deb-based linux distributions

This repo may give you some hints on keeping a system still alive when memory and/or swap space is seemingly fully crowded / filled.

It will also give you some possibilities on 'fine-tuning' those meassures with different options; but will of course not give you the possibility to have an 32GB-app running on a 16GB system.

These measures will only delay/avoid oom killing one of your memory intensive proceses.

Sources from where those basic scripts are derived from are also given for reference.

There will be two ways for integratiing the zram option and one way on manually activate zswap on your distribution.

1st)
Lets see how to activate zswap on all latest, but not only, deb-based linux distributions:

- open '/etc/default/grub' as root for editing
- change the line 'DEFAULT_GRUB_LINE' into:
  '

-work to be done-
