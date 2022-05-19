# Azure HPC Cache updates

This page documents feature changes in [Azure HPC Cache](https://docs.microsoft.com/azure/hpc-cache/), as well as updates to its underlying operating system.

Cache administrators are notified of operating system updates with a banner in the cache's **Overview** page in order to allow them to schedule the update for a convenient time. Other HPC Cache features and improvements, including changes to the portal GUI, are applied automatically.

Read about the OS update process in [Manage your cache - Upgrade cache software](https://docs.microsoft.com/azure/hpc-cache/hpc-cache-manage?tabs=azure-portal#upgrade-cache-software).

## OS update - 2022-05-19

This update was scheduled for April but did not roll out to all HPC Cache systems because a regression was found. If your cache receives two software upgrade notifications in quick succession, apply both.

This software change adds support for future HPC Cache features, updates some internal software packages, and fixes bugs including these:

* Fixed an issue that made it harder to detect back-end file changes with the cache usage model "Read heavy, infrequent writes"
* Minor bug fixes related to the Cache Priming feature, which is in preview

## OS update - 2022-03-07

OS software rolled out in the second week of March, 2022, includes internal bug fixes and software support for upcoming features. It also fixes these issues that affected some HPC Cache systems:

* Fixed a network driver issue that caused a problem when used with the newest Azure hardware. The problem was seen when using a new Mellanox network interface.
* Resolved a soft-deadlock issue that could cause client operations to stall after certain operation sequences were sent to the same parent and child directories.

## Features update - 2022-01-25

The update rolled out during the last week of January, 2022, included these new features:

* Cache invalidation by storage target

  The new invalidate feature lets you tell the cache to discard all cached files from a particular storage target. The next time a client requests that information, it will be read from the back-end storage system.

   Read [Invalidate cache contents](https://docs.microsoft.com/azure/hpc-cache/manage-storage-targets?tabs=azure-portal#invalidate-cache-contents-for-a-storage-target) for details, including a caution about using this feature with write caching.

* Cache priming (public preview)

  The new priming feature lets you load specific content into the cache before it's requested. This means that you can populate the cache with your expected working files ahead of time, and start your compute task with faster responses. <!--reduce read latency from the beginning of your compute task? -->

  Learn more at [Pre-load files in Azure HPC Cache (preview)](https://docs.microsoft.com/azure/hpc-cache/prime-cache).

* Additional Azure regions

  Azure HPC Cache is now available in Central India and Sweden Central.

* Availability zone support

  For caches created in Azure regions that support Availability zones, you can choose which zone will host cache resources.

* Refresh DNS available for more storage types

  To better support storage targets that use Azure storage private endpoints, an IP refresh control now appears on the [storage target management](https://docs.microsoft.com/azure/hpc-cache/manage-storage-targets?tabs=azure-portal#update-ip-address) page for Azure Blob and NFS-mounted blob storage targets as well as for NFS storage targets that use DNS. A DNS refresh is needed if you change settings on a private endpoint used for a storage target.

  Additional information about working with private endpoints also was added to the [storage prerequisites documentation](https://docs.microsoft.com/azure/hpc-cache/hpc-cache-prerequisites#work-with-private-endpoints).

* Bug fixes:

  * Addressed cache throughput spikes
  * Fixed a bad request associated with blob storage DNS refresh
  * Corrected a repeated error message and an incorrect error message seen when adding an NFS-mounted blob storage target
  * Aligned the cache creation timeout with the overall timeout
  * Fixed an issue that caused a restarted cache to come up in degraded state

## Features update - 2021-12-07

An update in December 2021 included these changes:

* New Azure regions - Added support for HPC Cache in Germany West Central and West US 3
* Operations on a storage target are blocked while the target is being created
* A change to the DNS address list no longer results in a degraded state
* Corrected an error message for a storage target flush operation
* Modified an alert about multiple NFS-mounted blob storage targets
* Fixed an issue that caused a cache to show Transitioning state instead of Healthy
* Various security and compliance updates
* Documentation improvements

## OS update - 2021-12-02

The OS update rolled out in early December included general stability improvements and updates to internal software packages.

## OS update - 2021-10-13

The OS update released on October 13 included these improvements and bug fixes:

* Fixed a timing issue that could prevent a newly created HPC Cache from serving data.

* Simplified an internal configuration database to prevent jobs from becoming stuck and requiring manual intervention.

* Fixed a defect that could leave DNS poller alerts active after the related storage target had been removed. This issue could cause the Azure HPC Cache to go to Degraded state.

* A probe was added to monitor the health of NFS TCP connections to NAS systems.

  * If NULL RPCs cannot succeed on a connection for 20 minutes, then the connection will no longer be used for new NFS operations.

  * If there are pending NFS operations on that unhealthy connection, then reconnect attempts will be made after a delay. After each unsuccessful reconnect attempt, the delay will increase, up to a maximum of one hour. The delay is designed to allow firewall state to time out.

  This change applies only to NAS-backed storage targets that are created after applying this software update. Other storage targets are unaffected.

  Connectivity conditions might take up to three hours to clear. Defective or misconfigured firewalls can extend this time indefinitely. The TCP connection parameters in the condition will aid in firewall troubleshooting.

## Features update - 2021-09-30

The update rolled out the week of September 27, 2021 included these changes:

* Updated mount instructions

  * The cache **Mount instructions** page now emphasizes the need to mount clients to all available IP addresses in the cache, and gives alternate mount commands with the IP addresses that were not selected in the **Cache mount address** field.

    Read [Use the mount instructions utility](https://docs.microsoft.com/azure/hpc-cache/hpc-cache-mount#use-the-mount-instructions-utility) to learn more.

* Storage target updates

  * Individual storage targets now show operational states in the Azure portal. Cache administrators can use this information to understand when a storage target is busy processing an operation, temporarily inaccessible because it is moving cached data to back-end storage, or ready to support client requests.

  This change gives administrators more insight into workflows, and helps them make informed decisions when suspending or deleting a storage target.

  Read more in [View and manage storage targets](https://docs.microsoft.com/azure/hpc-cache/manage-storage-targets?tabs=azure-portal)

* [Azure Private Endpoint](https://docs.microsoft.com/azure/private-link/private-endpoint-overview) support for NFS, blob, and NFS-mounted blob storage targets

## OS update - 2021-09-01

The OS update released on September 1 included security updates and various performance improvements.

Additional information:

* Bug fix - Fixed a permission error that could cause a failure when trying to change group
ownership to a group that’s outside the first 16 groups on the extended group ID list.
This problem occurred when the file’s mode bits did not include group write access.
