# Foundations

## Linux Kernel Features

- Namespaces
- Control Groups (cgroups)
- Union Mount Filesystem

### Namespaces

- A `namespace` wraps a `global system resource` in an abstraction that makes it appear to the processes within the namespace that they have their own isolated instance of the global resource.
- Changes to the `global resource` are visible to other processes that are members of the namespace, but are invisible to other processes.

### Control Groups (cgroups)

- A Linux Kernel feature which allow processes to be organized into hierarchical groups whose usage of various types of resources can then be limited and monitored.

```shell
cat /proc/cgroups
```

### Union Mount Filesystems (overlayfs)

- Allows files and directories of separate file systems, known as branches, to be transparently overlaid, forming a single coherent file system.
- Contents of directories which have the same path within the merged branches will be seen together in a single merged directory, within the new, virtual file system.

## Why Containers

- Better isolation in a single operating system.
- Reduced environment variances.
- Increase speed of change.