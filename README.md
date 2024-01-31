## NFS
Network File System (NFS) is mechanism for shared storage files. There are two separates:

- NfS Server
- NFS Client

### ➤ NFS Server

✦ Setup

✦ Configuration

#### Install NFS Kernel Server
```
sudo apt-get update && sudo apt-get install nfs-kernel-server
```

#### Check NFS Kernel Server Status
```
sudo systemctl status nfs-kernel-server
```

#### After installed, there's default directory /etc/exports. Rename file and Create a new one
```
sudo mv /etc/exports /etc/exports.original
```

#### Create directory you gonna export. Below is example:
```
sudo mkdir /exports/shared/log_manager/sessions
sudo mkdir /exports/shared/log_manager/cache
```

#### New file "/etc/exports" look like this - Configuration
```
#========== - Log Management Project - White list IP Address Client
/exports/shared/log_manager/sessions 172.xx.xx.00(rw,no_subtree_check) 172.xx.xx.01(rw,no_subtree_check)
/exports/shared/log_manager/cache 172.xx.xx.00(rw,no_subtree_check) 172.xx.xx.01(rw,no_subtree_check)
```

#### Restart NFS Kernel Server
```
sudo systemctl restart nfs-kernel-server
```
##
### ➤ NFS Client

✦ Setup

✦ Mounts

