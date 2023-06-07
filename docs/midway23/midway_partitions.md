# Slurm Partitions

Partitions are collections of compute nodes with similar characteristics. Normally, a user submits a job to a partition (via Slurm flag `--partition=<partition>`) and then the job is allocated to any idle compute node within that partition. To get a full list of available partitions, type the following command in the terminal
```
sinfo -o "%20P %5D %14F %4c %8G %8z %26f %N"
```
The typical output will include: 

| Column           | Description                                                         |
|------------------|---------------------------------------------------------------------|
| `AVAIL_FEATURES` | Available features such as CPUs, GPUs, internode interfaces         |
| `NODELIST`       | Compute nodes IDs within the given partition                        |
| `NODES(A/I/O/T)` | Number of nodes by state in the format "allocated/idle/other/total" |
| `S:C:T`          | Number of sockets, cores, and threads                               |

If a user wants to submit their job to the particular compute node, this can be requested by adding the Slurm flag `--nodelist=<compute_node_ID>`. Compute nodes that differ in available features can be allocated by setting an additional constraint `--constraint=<compute_node_feature>`, for example `--constraint=v100` will allocate job to the compute node with NVIDIA V100 GPUs. 

## Shared Partitions
All Midway users can submit jobs to any of the following shared partitions:
<!-- THIS COMMNAD WORKS ON MIDWAY2 BUT NOT ON MIDWAY3 - SHOULD BE FIXED
The list of shared partitions can be invoked by -->
<!-- ```
rcchelp sinfo shared
``` -->
=== "Midway2"
      | Partition  | Nodes | Cores/node | CPU Type  | GPUs/node | GPU Type | Total Memory/node |
      |------------|-------|------------|-----------|-----------|----------|--------------|
      | broadwl    | 8     | 40         | gold-6148 | 4         | v100     | 192 GB       |
      | broadwl    | 2     | 40         | gold-6148 | None      | None     | 192 GB       |
      | broadwl    | 187   | 28         | e5-2680v4 | None      | None     | 64 GB        |
      | broadwl    | 164   | 28         | e5-2680v4 | None      | None     | 64 GB        |
      | broadwl    | 3     | 28         | e5-2680v4 | None      | None     | 64 GB        |
      | broadwl-lc | 14    | 28         | e5-2680v4 | None      | None     | 64 GB        |
      | bigmem2    | 5     | 28         | e5-2680v4 | None      | None     | 512 GB       |
      | gpu2       | 6     | 28         | e5-2680v4 | 2         | k80      | 128 GB       |
      | gpu2       | 1     | 40         | gold-6148 | 4         | v100     | 96 GB        |

===+ "Midway3"
      | Partition | Nodes | Cores/node | CPU Type   | GPUs/node | GPU Type | Total Memory/node |
      |-----------|-------|------------|------------|-----------|----------|--------------|
      | caslake   | 203   | 48         | gold-6248r | None      | None     | 192 GB       |
      | bigmem    | 1     | 48         | gold-6248r | None      | None     | 768 GB       |
      | bigmem    | 1     | 48         | gold-6248r | None      | None     | 1536 GB      |
      | amd-hm    | 1     | 128        | epyc-7702  | None      | None     | 2048 GB      |
      | amd       | 1     | 128        | epyc-7702  | None      | None     | 1024 GB      |
      | amd       | 40    | 128        | epyc-7702  | None      | None     | 256 GB       |
      | gpu       | 5     | 48         | gold-6248r | 4         | v100     | 192 GB       |
      | gpu       | 5     | 48         | gold-6248r | 4         | rtx6000  | 192 GB       |

## Shared Partition QOS

This table details the job limits of each partition, set via a Quality of Service (QOS) accessible via `rcchelp qos`.

=== "Midway2 QOS"

    | Partition | Max Nodes Per User | Max CPUs Per User | Max Jobs Per User | Max Wall Time |
    |-----------|--------------------|-------------------|-------------------|---------------|
    | `broadwl` | 100                | 2800              | 1000              | 36 H          |
    | `gpu2`    | None               | None              | 10                | 36 H          |
    | `bigmem2` | None               | 112               | 5                 | 36 H          |


===+ "Midway3 QOS"

    | Partition | Max Nodes Per User | Max CPUs Per User | Max Jobs Per User | Max Wall Time |
    |-----------|--------------------|-------------------|-------------------|---------------|
    | `caslake` | 100                | 4800              | 1000              | 36 H          |
    | `gpu`     | None               | None              | 500               | 36 H          |
    | `bigmem`  | 96                 | 192               | 10                | 36 H          |
    | `amd`     | 64                 | 128               | 200               | 36 H          |

If your research requires a temporary exception to a particular limit, you may apply for a special allocation. Special allocations are evaluated on an individual basis and may or may not be granted.



## Institutional Partitions
Faculty and their group members can take advantage of institutional partitions dedicated to research within UChicago divisions, departments, and institutions:

* ssd, ssd-gpu:   Social Science Research       
> SSD Faculty (By default) and their group members ([Apply](https://rcc.uchicago.edu/accounts-allocations/join-different-pi-account){:target="_blank"}) 
* kicp, kicp-gpu: Cosmological Physics Research 
> KICP Faculty (By default) and their group members ([Apply](https://rcc.uchicago.edu/accounts-allocations/join-different-pi-account){:target="_blank"})



<!-- === "Midway2 NEED TO CHECK WITH KATHY"
      | Partition | Nodes  | CPUs |
      | --------- | -------| -----|
      | broadwl   |   8    |  40  |
      | broadwl   |   2    |  40  |
      | broadwl   |   187  |  28  |
      | broadwl   |   164  |  28  |
      | broadwl   |   3    |  28  |
      | broadwl-lc|   14   |  28  |
      | bigmem2   |   5    |  28  |
      | gpu2      |   6    |  28  |
      | gpu2      |   1    |  40  | -->

===+ "Midway3"
      | Partition | Nodes | Cores/Node | CPU Type   | GPUs | GPU Type | Total Memory/node |
      |-----------|-------|------|------------|------|----------|--------------|
      | ssd       | 18    | 48   | gold-6248r | None | None     | 192 GB       |
      | ssd-gpu   | 1     | 32   | gold-6346  | 4    | a100     | 256 GB       |
      | kicp      | 6     | 48   | gold-6248r | None | None     | 192 GB       |
      | kicp-gpu  | 1     | 32   | gold-5218  | 4    | v100     | 192 GB       |



## Institutional Partition QOS

This table details the job limits of each partition, set via a Quality of Service (QOS) accessible via `rcchelp qos`. 

<!-- === "Midway2 QOS"

    | Partition | Max Nodes Per User| Max CPUs Per User  | Max Jobs Per User| Max Wall Time | 
    | --------- | ----------------- | ------------------ | ---------------- | ------------- |
    | `broadwl` | 100               |            2800    |             1000 |  36 H         |
    | `gpu2`    | None              |            None    |             10   |  36 H         |
    | `bigmem2` | None              |            112     |             5    |  36 H         | -->


===+ "Midway3 QOS"

    | Partition | AllowAccount | QOS     | Max Wall Time |
    |-----------|--------------|---------|---------------|
    | ssd       | ssd          | ssd     | 36 H          |
    | ssd       | ssd-stu      | ssd-stu | 36 H          |
    | ssd-gpu   | ssd          | ssd     | 36 H          |
    | ssd-gpu   | ssd-stu      | ssd-stu | 36 H          |
    | kicp      | kicp         | kicp    | 48 H          |
    | kicp-gpu  | kicp         | kicp    | 48 H          |

!!! note
    QOS for private and institutional partitions can be changed upon owner's request.


## Private Partitions
These partitions are typically associated with a research group with access approved by PI. They can be shared with other PIs or researchers across the University of Chicago and also with external collaborators who have midway accounts ([Apply](https://rcc.uchicago.edu/accounts-allocations/join-different-pi-account){:target="_blank"}). Private partitions can be purchased via [RCC Cluster Partnership Program](https://rcc.uchicago.edu/support-and-services/cluster-partnership-program){:target="_blank"} to better accomodate the needs of a research group.

## Do I Have Access to a Partition?
To check if you have access to a partition, first determine which groups your account belongs to: 
```
groups
```
and then check AllowAccounts field in the partion summary: 
```
scontrol show partition <partition_name>
```
If AllowAccount is set to All then it is a shared partition available to all users. Otherwise, it is an institutional or private partition and one of your groups must match the AllowAccounts field in order to submit SLURM jobs to that partition. 

