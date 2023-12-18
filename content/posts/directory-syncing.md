---
title: "Directory Syncing"
date: 2023-12-18T10:54:16+01:00
---

Syncing the contents of a directory with a directory on a remote host can
ge done with a simple `rsync` command:

```shell
rsync \
  --verbose \
  --recursive \
  --delete \
  source-dir host:destination-dir
```

The `--verbose` option is optional of course, but if you want to know what
files `rsync` is copying and/or deleting, you'll have to turn on the verbose
output.

To include subdirectories in the sync, use `--recursive`.

And `--delete` will cause `rsync` to delete files in the destination directory
if they are not present in the source directory.

There's one small pitfall to keep in mind: for the deletion to work properly,
you have to specify the source as a directory and not a file list via globbing
or so. So don't do this in combination with the `--delete` option:

```shell
rsync --recursive --delete source-dir/* host:destination-dir
```

This style of using `rsync` works great for publishing the files for a
relatively small static website where a sophisticated build and publishing
pipeline would be overkill.

Note that for creating backups, the `--archive` option is probably more
suitable.
