# cloud-init

wget https://cloud-images.ubuntu.com/noble/current/noble-server-cloudimg-amd64.img
qm create 110 --name ubuntu-cloud-1 --memory 2048 --cores 2 --net0 virtio,bridge=vmbr0
qm importdisk 110 noble-server-cloudimg-amd64.img local-lvm
qm set 110 --scsihw virtio-scsi-pci --scsi0 local-lvm:vm-110-disk-0
qm set 110 --ide2 local-lvm:cloudinit
qm set 110 --boot c --bootdisk scsi0
qm set 110 --serial0 socket --vga serial0
qm cloudinit dump 110 user
