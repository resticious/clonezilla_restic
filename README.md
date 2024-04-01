# Resticlonezillian

Custom [clonezilla](https://clonezilla.org/) image, using [restic](https://restic.net/) to make backups faster and more efficient, effectively turning them into incremental backups. It also simplifies the creation of system backups.

## Introduction
[Clonezilla](https://clonezilla.org/) is a reliable and highly trusted backup solution for system backups. \
It can be used to create images from disks and/or partitions and to restore them based on the images, later. It laso can be used to clone disks or partitions directly. \
It uses [partclone](https://partclone.org/) (and other tools) to clone or create images. It only reads and writes used sectors instead of the whole disk or partition. It also can create compressed images, further saving space at the backup location. \
Clonezilla backups always are "full backups" and they can't be craeted while your system runs. The latter has benefits and downsides; Benefit: More reliability and a cleaner system after restore; Downside: Less comfort. \
Standard clonezilla also is very tiring, asking a lot of questions before running the task. \
Clonezilla itself offers the ability to create custom clonezilla images, for example, to reduce the amount of questions.

[Restic](https://restic.net/) is a fast, secure and extreme storage-efficient solution for file backups. \
It's storage-efficiency is powered by compression and by deduplication using content-definded chunking. \
It's security is powered by encryption. \
The only thing restic isn't good for is system backups, since systems aren't simply files and folders. But restic offers a feature suitable to "resticify" system backups; Reading from stdin for backups and writing to stdout for restore.

**Resticlonezillian** combines clonezilla and restic as follows:
When an image of a partition or disk is created, it will be written to stdout instead of a file, so it can be piped to restic, so restic will create a backup from it. This converts clonezilla backups into beeing incremental. \
The next time creating a backup, restic's deduplication will detect almost all chunks beeing identical and already exesting in older backups(s). Only different chunks, caused by minor changes in your operating system, have to be copied into restc's backups location.

Notice: The speed is not totally comparable with incremental backups, since all data have to be read, but it is faster than a full backup, since less data have to be written.

**Resticlonezillian** also simplifies the process of creating backups or restoring your system as follows:
On startup resticlonezillian will determine required information automatically, based on files and folders, having specific names, existing at specific locations.

Read the [documentation](https://resticlonezillian.documentation.resticious.net) for further information, help and tutorials.

## Download
You can download **Resticlonezillian** on [souceforge.net](https://sourceforge.net/projects/resticlonezillian/)

## Usage

Read the [documentation](https://resticlonezillian.documentation.resticious.net) for how to use **Resticlonezillian**.

## License

### Clonezilla
* Licensed under a [GNU General Public License v2.0](./LICENSE_clonezilla)
* [Source](https://github.com/stevenshiau/clonezilla)
* Maintainer: [Steven Shiau](https://github.com/stevenshiau/)
* Copyright (C) 1989, 1991 Free Software Foundation, Inc.
* My changes: Using custom-ocs to create custom iso, with following differents:
  * Simplification of usage
  * Creating backups directly piping into restic snapshots

### Restic
* Licensed under a [BSD 2-Clause "Simplified" License](./LICENSE_restic).
* [Source](https://github.com/restic/restic)
* Maintainer: [Alexander "fd0" Neumann](https://github.com/fd0)
* Copyright (c) 2014, Alexander Neumann <alexander@bumpern.de>
* My changes: No changes; Simply bundling it with Clonezilla

### Resticlonezillian
Resticlonezillian is licensed under a [GNU General Public License v2.0](./LICENSE).
