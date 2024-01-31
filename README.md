## NFS
Network File System (NFS) is mechanism for shared storage files. There are two separates:

- NfS Server
- NFS Client

### ➤ NFS Server

✦ Setup

✦ Configuration

#### 🔵 Install NFS Kernel Server
```
sudo apt-get update && sudo apt-get install nfs-kernel-server
```

#### 🔵 Check NFS Kernel Server Status
```
sudo systemctl status nfs-kernel-server
```

#### 🔵 After installed, there's default directory /etc/exports. Rename file and Create a new one
```
sudo mv /etc/exports /etc/exports.original
```

#### 🔵 Create directory you gonna export. Below is example:
```
sudo mkdir /exports/shared/log_manager/sessions
sudo mkdir /exports/shared/log_manager/cache
```

#### 🔵 New file "/etc/exports" look like this - Configuration
```
#========== - Log Management Project - White list IP Address Client
/exports/shared/log_manager/sessions 172.xx.xx.00(rw,no_subtree_check) 172.xx.xx.01(rw,no_subtree_check)
/exports/shared/log_manager/cache 172.xx.xx.00(rw,no_subtree_check) 172.xx.xx.01(rw,no_subtree_check)
```

#### 🔵 Restart NFS Kernel Server
```
sudo systemctl restart nfs-kernel-server
```
##
### ➤ NFS Client

✦ Setup

✦ Mounts

#### 🔵 Install NFS Client (Your Client Server) - Ubuntu or Debian
```
sudo apt-get update && apt-get install nfs-common
```

#### 🔵 Showmount export of Server - Export List
```
showmount --exports <IP_NFS_SERVER>
```
#### ✍️ *Note: Have to improve Security or prevent risky when use nfs to export list directory*

#### 🔵 Create mount directory for Client. Example below
```
sudo mkdir /mnt/nfs/<your_project_name>/sessions
sudo mkdir /mnt/nfs/<your_project_name>/cache
```

#### 🔵 Manually mounting an NFS Share/export - Based on Export List
```
sudo mount <IP_NFS_SERVER>:/exports/shared/log_manager/sessions /mnt/nfs/<your_project_name>/sessions
sudo mount <IP_NFS_SERVER>:/exports/shared/log_manager/cache /mnt/nfs/<your_project_name>/cache
```
#### ✍️ *This way could keep configuration temporarily. After rebooting server, it's all reset.*

#### 🔵 Verify Mounting
```
sudo df -h
cat /mnt/nfs/<your_project_name>/sessions
cat /mnt/nfs/<your_project_name>/cache
```

#### ✍️ *If no longer needed, umount them*
```
umount /mnt/nfs/<your_project_name>/sessions && /mnt/nfs/<your_project_name>/cache
```

#### 🔵 This is good practice to automatically mount NFS Share/export and keep permanently
```
sudo nano /etc/fstab
```
Content of File 👇
```
#============= Log Management Project
<IP_NFS_SERVER>:/exports/shared/log_manager/sessions   /mnt/nfs/<your_project_name>/sessions   nfs   rw,relatime,acl    0 1
<IP_NFS_SERVER>:/exports/shared/log_manager/cache   /mnt/nfs/<your_project_name>/cache   nfs   rw,relatime,acl    0 1
```

#### 🔵 Run mount command
```
sudo mount -a
```
##
<h3>☑️It's all done. Please follow this guide👆</h3>

##
