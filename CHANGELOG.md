# Azure HPC Cache updates

This page documents feature changes in [Azure HPC Cache](https://docs.microsoft.com/azure/hpc-cache/), as well as updates to its underlying operating system.

Cache administrators are notified of operating system updates with a banner in the cache's **Overview** page in order to allow them to schedule the update for a convenient time. Other HPC Cache features and improvements, including changes to the portal GUI, are applied automatically.

Read about the OS update process in [Manage your cache - Upgrade cache software](https://docs.microsoft.com/azure/hpc-cache/hpc-cache-manage?tabs=azure-portal#upgrade-cache-software).

## Features update - 2021-09-30

The update rolled out the week of September 27, 2021 include these changes:

* Updated mount instructions

  * The cache **Mount instructions** page now emphasizes the need to mount clients to all available IP addresses in the cache, and gives alternate mount commands with the IP addresses that were not selected in the **Cache mount address** field.

    Read [Use the mount instructions utility](https://docs.microsoft.com/azure/hpc-cache/hpc-cache-mount#use-the-mount-instructions-utility) to learn more.

* Storage target updates

  * Individual storage targets now show operational states in the Azure portal. Cache administrators can use this information to understand when a storage target is busy processing an operation, temporarily inaccessible because it is moving cached data to back-end storage, or ready to support client requests.

  This change gives administrators more insight into workflows, and helps them make informed decisions when suspending or deleting a storage target.

  Read more in [View and manage storage targets](https://docs.microsoft.com/azure/hpc-cache/manage-storage-targets?tabs=azure-portal)

* [Azure Private Endpoint](https://docs.microsoft.com/azure/private-link/private-endpoint-overview) support for NFS, blob, and NFS-mounted blob storage targets

* Support for [Qumolo on Azure as a Service](https://qumulo.com/azure/)

## OS update - 2021-09-01

The OS update released on September 1 includes security updates and various performance improvements.

Additional information:

* Bug fix - Fixed a permission error that could cause a failure when trying to change group
ownership to a group that’s outside the first 16 groups on the extended group ID list.
This problem occurred when the file’s mode bits did not include group write access.
