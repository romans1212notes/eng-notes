# How it works
## Three Phases
* enlist: https://docs.ubuntu.com/maas/2.1/en/nodes-add
  *  maas/contrib/preseeds_v2/enlist_userdata - cloud-init config, maybe for enlistment
* commision:
  * https://docs.ubuntu.com/maas/2.1/en/nodes-commission 
  * https://github.com/maas/maas/blob/master/docs/development/notes/anatomy-of-recommissioning-in-maas-2.0.rst
* deploy: https://docs.ubuntu.com/maas/2.1/en/installconfig-nodes-deploy

Within each stage, the first 4 steps are common:
1. DHCP server is contacted
2. kernel and initrd are received over TFTP
3. machine boots
4. initrd mounts a Squashfs image ephemerally over iSCSI

## Tools
* cloud-init: https://cloudinit.readthedocs.io/en/latest/
* curtin for installation

## API
https://docs.ubuntu.com/maas/2.2/en/api

## kernel, initrd, squashfs
* decompress squashfs
  *  sudo unsquashfs -f -d /media/location1 /media/location2/file.squashfs
  * https://askubuntu.com/questions/437880/extract-a-squashfs-to-an-existing-directory

## ISCI with squashfs
* kernel_opts.py
  * compose_purpose_opts()
* provisioningserver/templates/pxe/config.ephemeral.amd64.generic.template

## Files
* /var/lib/maas/boot-resources/
  * snapshot-201709xx-xxxxxx
  * current -> 
  * cache
* /var/lib/maas/dhcp/dhcpd.leases
* /var/log/maas/
  * maas.log
  * rackd.log
  * regiond.log

## services
maas-regiond, maas-rackd

## Images
https://docs.ubuntu.com/maas/2.1/en/installconfig-images

MAAS supports the images it generates for stable Ubuntu releases and for CentOS 6.6 and CentOS 7. Ubuntu Advantage is needed in order to use Windows, RHEL and SUSE images or in order to build a custom image for any operating system.
