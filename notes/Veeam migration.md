---
tags: [TP]
title: Veeam migration
created: '2020-06-15T14:43:41.279Z'
modified: '2020-06-17T08:37:01.381Z'
---

# Veeam migration 


### prerequisites
- license file
- encryption password (it would be necessary to re-enter all passwords when importing a non-encrypted backup)

--- 
### checklist
- [ ] Mapped logical drives to the __same__ letters on the new server
- [ ] Veeam version is the latest on both servers
- [ ] Veeam is licensed on both servers
--- 

https://www.veeam.com/kb1889
 

Perform the following steps on the old server:
1. Stop and disable all jobs.
1. Manually perform a [configuration backup](https://helpcenter.veeam.com/docs/backup/vsphere/vbr_config_manually.html?ver=100).
    - specify encryption password
    - default directory should be `(\%BackupDirectory%) \VeeamConfigBackup\%BackupServer%`

1. Close Veeam GUI and stop all Veeam Services.

Perform the following steps on the new server:
1. Set up SYSTEM account on MS SQL 2017 with the [privileges required](https://helpcenter.veeam.com/docs/backup/vsphere/required_permissions.html?ver=100#rpvbr) (create any DB)
1. Install Veeam Backup & Replication with a brand new DB. 
    - apply the license file from the old server and install dependencies
    - install as a SYSTEM account, default config
1. Apply the latest patch to Veeam Backup & Replication: http://www.veeam.com/patches.html
1. Make sure all local drives that were being used as repositories on the old server are now attached with the same drive letters on the new server.
1. Perform [configuration backup restore](https://helpcenter.veeam.com/docs/backup/vsphere/vbr_config_restore.html?ver=100):
    - use the password to decrypt

1. Run a test job to make sure everything moved correctly.


