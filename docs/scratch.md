# Temporary storage performance-hierarchy
The temporary storage options are listed below.

## Each compute node's local `/tmp` directory
Sophia compute nodes are *ephemeral* meaning they fetch a minimal
[CentOS](https://www.centos.org/) installation at each reboot which then runs in the node's memory.
This means that the underlying [XFS](https://www.kernel.org/doc/html/latest/admin-guide/xfs.html)
file system runs on the compute node's random access memory
hardware with orders of magnitude higher bandwidth and lower latency compared with disk drives.
Thus, e.g. to eliminate I/O as the limiting factor in a application performance benchmark
experiment, a Sophia user can run test code from the `/tmp` directory on up to
32 MPI processes on a single Sophia node with 32 physical cores.

The RAM-based storage provides approximately 64GB capacity per node (minus OS usage).

## Each compute node's local `/scratch` directory
Each compute node is equipped with a 1TB spinning disk mounted at
`/scratch`. This provides significantly more storage space than the
RAM-based `/tmp` directory, while still offering good I/O performance
for local storage needs. This storage is node-local and is ideal for
larger temporary datasets that will not fit in RAM but do not require
shared access across nodes.

## Burst buffer
Two servers with
[NVMe disks](https://www.samsung.com/semiconductor/global.semi.static/Brochure_Samsung_PM1725a_NVMe_SSD_1805.pdf) - Sophia's burst buffer nodes - are connected to
Sophia compute nodes via the HPC cluster's Mellanox EDR Infiniband interconnect,
and each server connects to the Ceph file system via bonded 10Gbps connections
(i.e. 20Gbps).
Sophia's burst buffer runs the [BeeGFS file system](https://www.beegfs.io), striping data written from 
compute nodes across BeeGFS storage targets.
The storage resource is mounted on `/work` on Sophia's head node and all compute nodes and 
provides approximately 50TB of shared storage space accessible from all nodes.

## Automatic Temporary Directory Management

To simplify temporary storage usage and ensure proper cleanup, we have implemented automatic
temporary directory management through predefined SLURM variables:

* `$TMPRAM` - Points to `/tmp/users/$SLURM_JOB_UID/$SLURM_JOB_ID`
* `$TMPDISK` - Points to `/scratch/users/$SLURM_JOB_UID/$SLURM_JOB_ID`
* `$TMPSHARE` - Points to `/work/users/$SLURM_JOB_UID/$SLURM_JOB_ID`

These directories are automatically created when your job starts and deleted when your job
completes, regardless of whether the job completes successfully or fails. This eliminates
the need for manual cleanup and helps maintain system performance.

## Usage Example

```bash
#!/bin/bash
#SBATCH [your job parameters]

# Use RAM-based storage for very fast I/O
./fast_io_program --workdir=$TMPRAM

# Use local disk for larger datasets
cp large_input.dat $TMPDISK/
./analysis_program --input=$TMPDISK/large_input.dat --output=$TMPDISK/results.dat
cp $TMPDISK/results.dat $HOME/results/

# Use shared storage for multi-node access
mpirun -n 64 ./parallel_sim --output=$TMPSHARE/simulation_output/
```

**Important**: Any data you wish to keep must be copied to your home directory or permanent
storage before your job ends, as the temporary directories will be automatically removed.
