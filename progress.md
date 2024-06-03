# progress

## Q

CheckedPopenLocal get_osd_ra
02:31:31 - INFO     - cbt      - Skipping existing test in /home/lihaohua/cpenv/logs/results/00000000/id-3a41e9ad.
CheckedPopenLocal get_osd_ra
02:31:31 - INFO     - cbt      - Skipping existing test in /home/lihaohua/cpenv/logs/results/00000000/id-e6d6e7a6.
CheckedPopenLocal get_osd_ra
02:31:31 - INFO     - cbt      - Skipping existing test in /home/lihaohua/cpenv/logs/results/00000000/id-3a41e9ad.
CheckedPopenLocal get_osd_ra
02:31:31 - INFO     - cbt      - Skipping existing test in /home/lihaohua/cpenv/logs/results/00000000/id-e6d6e7a6.

## A

delete dir




## Q

communicate  10.91.132.216: bash: line 1: /usr/local/pdsh/bin/rpdcp: No such file or directory


## A

  509  wget https://github.com/grondo/pdsh/archive/pdsh-2.31.tar.gz
  510  pwd
  511  ls
  512  tar xf pdsh-2.31.tar.gz -C /usr/local/src/
  513  cd /usr/local/src/pdsh-pdsh-2.31/
  514  ./configure --prefix=/usr/local/pdsh --with-ssh --with-machines=/usr/local/pdsh/machines --with-dshgroups=/usr/local/pdsh/group --with-rcmd-rank-list=ssh --with-exec && make && make install
  515  echo 'export PATH=/usr/local/pdsh/bin:$PATH' >> /etc/profile
  516  source /etc/profile
  517  pdsh -V
  518  history






## Q

针对ceph health，为啥root可以执行成功，自己的就无法执行成功

lihaohua@cld-osd16-10080:/usr/local/src/pdsh-pdsh-2.31$ /usr/bin/ceph -c /etc/ceph/ceph.conf health
2024-06-03T03:38:22.014+0000 7f97765ff6c0 -1 auth: unable to find a keyring on /etc/ceph/ceph.client.admin.keyring,/etc/ceph/ceph.keyring,/etc/ceph/keyring,/etc/ceph/keyring.bin,: (2) No such file or directory
2024-06-03T03:38:22.014+0000 7f97765ff6c0 -1 AuthRegistry(0x7f977005aee0) no keyring found at /etc/ceph/ceph.client.admin.keyring,/etc/ceph/ceph.keyring,/etc/ceph/keyring,/etc/ceph/keyring.bin,, disabling cephx
2024-06-03T03:38:22.014+0000 7f97765ff6c0 -1 auth: unable to find a keyring on /etc/ceph/ceph.client.admin.keyring,/etc/ceph/ceph.keyring,/etc/ceph/keyring,/etc/ceph/keyring.bin,: (2) No such file or directory
2024-06-03T03:38:22.014+0000 7f97765ff6c0 -1 AuthRegistry(0x7f977005e878) no keyring found at /etc/ceph/ceph.client.admin.keyring,/etc/ceph/ceph.keyring,/etc/ceph/keyring,/etc/ceph/keyring.bin,, disabling cephx
2024-06-03T03:38:22.014+0000 7f97765ff6c0 -1 auth: unable to find a keyring on /etc/ceph/ceph.client.admin.keyring,/etc/ceph/ceph.keyring,/etc/ceph/keyring,/etc/ceph/keyring.bin,: (2) No such file or directory
2024-06-03T03:38:22.014+0000 7f97765ff6c0 -1 AuthRegistry(0x7f97765fe3e0) no keyring found at /etc/ceph/ceph.client.admin.keyring,/etc/ceph/ceph.keyring,/etc/ceph/keyring,/etc/ceph/keyring.bin,, disabling cephx
[errno 2] RADOS object not found (error connecting to the cluster)
lihaohua@cld-osd16-10080:/usr/local/src/pdsh-pdsh-2.31$
lihaohua@cld-osd16-10080:/usr/local/src/pdsh-pdsh-2.31$
lihaohua@cld-osd16-10080:/usr/local/src/pdsh-pdsh-2.31$
lihaohua@cld-osd16-10080:/usr/local/src/pdsh-pdsh-2.31$ su root
Password:
root@cld-osd16-10080:/usr/local/src/pdsh-pdsh-2.31# /usr/bin/ceph -c /etc/ceph/ceph.conf health
HEALTH_ERR 2 scrub errors; Too many repaired reads on 1 OSDs; Possible data damage: 1 pg inconsistent; Degraded data redundancy: 256 pgs undersized; mon is allowing insecure global_id reclaim
root@cld-osd16-10080:/usr/local/s

## A

如果文件权限不允许 lihaohua 用户访问，可以使用 chmod 命令更改权限。例如，要给所有用户添加读权限，可以使用：

sudo chmod a+r /etc/ceph/ceph.client.admin.keyring





