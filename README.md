# bad-faith-workloads

A collection of bad containers that do bad things

## Directory

The following containers are available in this repository:

### k8s-isolation-*

> From https://github.com/simonkrenger/k8s-isolation

### k8s-isolation-cpuload

The `k8s-isolation-cpuload` container consumes all the CPU that it sees. It checks for the available cores and spawns a process for each core consuming CPU cycles.

### k8s-isolation-memoryeater

The `k8s-isolation-memoryeater` container consumes all memory resources. This will lead to the container typically being OOM killed by the orchestrator.

### k8s-isolation-forkbomb

The `k8s-isolation-forkbomb` container runs a script that forks infinitely. This creates new processes, potentially affecting other workload by using up system resources (e.g. PIDs).

### k8s-isolation-filedescriptors

The `k8s-isolation-filedescriptors` container opens as many file descriptors as possible. The file `/etc/hosts` is used to create the file descriptors. Typically, file descriptors are shared system-wide and not namespaced.

### k8s-isolation-consume-inodes

The `k8s-isolation-consume-inodes` container creates many small files in its working directory, trying to consume all available inodes. When the underlying filesystem is shared between multiple containers, this can lead to the `kubelet` having "DiskPressure"

### k8s-isolation-entropy

The `k8s-isolation-entropy` container consumes randomness by repeatedly querying `/dev/random`. This will deplete the entropy pool for the kernel. Typically, entropy is system-wide and is not namespaced.

### k8s-isolation-logspam

The `k8s-isolation-logspam` container writes a lot of data to `stdout`. Depending on your configuration, this can overwhelm your logging stack or logging infrastructure.
