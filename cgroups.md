# cgroups

## Basics

List cgroups version in system:

```bash
# grep cgroup /proc/filesystems
nodev	cgroup
nodev	cgroup2
```

Check cgroups mounts and which version is in use:

```bash
# grep cgroup /proc/mounts
tmpfs /sys/fs/cgroup tmpfs ro,seclabel,nosuid,nodev,noexec,mode=755 0 0
cgroup /sys/fs/cgroup/systemd cgroup rw,nosuid,nodev,noexec,relatime,xattr,release_agent=/usr/lib/systemd/systemd-cgroups-agent,name=systemd 0 0
cgroup /sys/fs/cgroup/freezer cgroup rw,nosuid,nodev,noexec,relatime,freezer 0 0
cgroup /sys/fs/cgroup/net_cls,net_prio cgroup rw,nosuid,nodev,noexec,relatime,net_cls,net_prio 0 0
cgroup /sys/fs/cgroup/devices cgroup rw,nosuid,nodev,noexec,relatime,devices 0 0
cgroup /sys/fs/cgroup/perf_event cgroup rw,nosuid,nodev,noexec,relatime,perf_event 0 0
cgroup /sys/fs/cgroup/cpu,cpuacct cgroup rw,nosuid,nodev,noexec,relatime,cpu,cpuacct 0 0
cgroup /sys/fs/cgroup/blkio cgroup rw,nosuid,nodev,noexec,relatime,blkio 0 0
cgroup /sys/fs/cgroup/memory cgroup rw,nosuid,nodev,noexec,relatime,memory 0 0
cgroup /sys/fs/cgroup/hugetlb cgroup rw,nosuid,nodev,noexec,relatime,hugetlb 0 0
cgroup /sys/fs/cgroup/cpuset cgroup rw,nosuid,nodev,noexec,relatime,cpuset 0 0
cgroup /sys/fs/cgroup/pids cgroup rw,nosuid,nodev,noexec,relatime,pids 0 0
coreos core # grep cgroup /proc/filesystems
```

Find in which cgroups is process:

```bash
# cat /proc/<pid>/cgroup
11:pids:/docker/df14dfa0d309064fdd21c5d6dce6b67a66813c515c8b1ff25814a5238c6a0c8b
10:cpuset:/docker/df14dfa0d309064fdd21c5d6dce6b67a66813c515c8b1ff25814a5238c6a0c8b
9:hugetlb:/docker/df14dfa0d309064fdd21c5d6dce6b67a66813c515c8b1ff25814a5238c6a0c8b
8:memory:/docker/df14dfa0d309064fdd21c5d6dce6b67a66813c515c8b1ff25814a5238c6a0c8b
7:blkio:/docker/df14dfa0d309064fdd21c5d6dce6b67a66813c515c8b1ff25814a5238c6a0c8b
6:cpu,cpuacct:/docker/df14dfa0d309064fdd21c5d6dce6b67a66813c515c8b1ff25814a5238c6a0c8b
5:perf_event:/docker/df14dfa0d309064fdd21c5d6dce6b67a66813c515c8b1ff25814a5238c6a0c8b
4:devices:/docker/df14dfa0d309064fdd21c5d6dce6b67a66813c515c8b1ff25814a5238c6a0c8b
3:net_cls,net_prio:/docker/df14dfa0d309064fdd21c5d6dce6b67a66813c515c8b1ff25814a5238c6a0c8b
2:freezer:/docker/df14dfa0d309064fdd21c5d6dce6b67a66813c515c8b1ff25814a5238c6a0c8b
1:name=systemd:/docker/df14dfa0d309064fdd21c5d6dce6b67a66813c515c8b1ff25814a5238c6a0c8b
```

Find in which cgroups is container managed by Kubernetes:

```bash
# docker inspect <container_name> -f "{{.HostConfig.CgroupParent}}"
kubepods-burstable-podb2f644bf_2e38_11ea_a279_52540053c585.slice
```

## cgroups stats

Docker container or Linux process cgroups memory stats:

```bash
cat /sys/fs/cgroup/memory/docker/<container_id>/memory.stat
```

Kubernetes managed pod cgroups memory stats:

```bash
cat /sys/fs/cgroup/memory/kubepods.slice/kubepods-burstable.slice/<CgroupParent>/memory.stat
```

[Back to main](README.md)
