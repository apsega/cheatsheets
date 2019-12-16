# virsh commands

## quemu-img

create disk:

```bash
qemu-img create -f qcow2 <name>-disk1.qcow2 200G
```

## virt-install

with additional disk from PXE:

```bash
virt-install \
  --autostart \
  --name <name> \
  --ram 8192 \
  --disk path=/var/lib/libvirt/images/<name>.qcow2,bus=virtio,format=qcow2 \
  --disk path=/var/lib/libvirt-volumes/<name>-disk1.qcow2,bus=virtio,format=qcow2 \
  --vcpus 4 \
  --noautoconsole \
  --os-type linux \
  --os-variant rhel7 \
  --graphics vnc,listen=0.0.0.0,password=<password>,port=<port> \
  --pxe \
  --network bridge=br0,mac=<mac:address>
```

with additional disk from HD image:

```bash
virt-install \
  --autostart \
  --name <name> \
  --ram 4096 \
  --disk path=/var/lib/libvirt/images/<name>.qcow2,bus=virtio,format=qcow2,size=50 \
  --vcpus 4 \
  --noautoconsole \
  --os-type linux \
  --os-variant rhel7 \
  --graphics vnc,listen=0.0.0.0,password=<password>,port=<port> \
  --network bridge=br0,mac=<mac:address> \
  --boot hd
```

## Increase Guest Disk Size

1. Detach disk

```bash
virsh detach-disk <instance_name> --target vdb
qemu-img resize <instance_name>-disk1.qcow2 +100G
```

2. Attach disk

```bash
virsh edit <instance_name>
virsh attach-disk <instance_name> --source /var/lib/libvirt-volumes/<instance_name>-disk1.qcow2 --target vdb --subdriver qcow2  --persistent
```

3. Resize block size

```bash
fdisk /dev/vdc
p, d, n, p, 1, 2048, max, w
```

4. Resize partition size

```bash
xfs_growfs /dev/vdb1
```

[Back to main](README.md)