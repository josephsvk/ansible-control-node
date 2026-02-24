# vypis pve zfs 

zfs list -o name,mountpoint,canmount,encryption,keystatus -r Secure
zfs get -r compression,atime,recordsize,sync,logbias,xattr,acltype Secure | sed -n '1,200p'