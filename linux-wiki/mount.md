# The mount command

Below is a reference to the help command built-in to mount:

Information pulled from this YouTube [video](https://www.youtube.com/watch?v=-HycpQEFESY)

```bash
mount -h

Usage:
 mount [-lhV]
 mount -a [options]
 mount [options] [--source] <source> | [--target] <directory>
 mount [options] <source> <directory>
 mount <operation> <mountpoint> [<target>]

Mount a filesystem.

Options:
 -a, --all               mount all filesystems mentioned in fstab
 -c, --no-canonicalize   dont canonicalize paths
 -f, --fake              dry run; skip the mount(2) syscall
 -F, --fork              fork off for each device (use with -a)
 -T, --fstab <path>      alternative file to /etc/fstab
 -i, --internal-only     dont call the mount.<type> helpers
 -l, --show-labels       show also filesystem labels
 -n, --no-mtab           dont write to /etc/mtab
     --options-mode <mode>
                         what to do with options loaded from fstab
     --options-source <source>
                         mount options source
     --options-source-force
                         force use of options from fstab/mtab
 -o, --options <list>    comma-separated list of mount options
 -O, --test-opts <list>  limit the set of filesystems (use with -a)
 -r, --read-only         mount the filesystem read-only (same as -o ro)
 -t, --types <list>      limit the set of filesystem types
     --source <src>      explicitly specifies source (path, label, uuid)
     --target <target>   explicitly specifies mountpoint
 -v, --verbose           say what is being done
 -w, --rw, --read-write  mount the filesystem read-write (default)
 -N, --namespace <ns>    perform mount in another namespace

 -h, --help              display this help
 -V, --version           display version

Source:
 -L, --label <label>     synonym for LABEL=<label>
 -U, --uuid <uuid>       synonym for UUID=<uuid>
 LABEL=<label>           specifies device by filesystem label
 UUID=<uuid>             specifies device by filesystem UUID
 PARTLABEL=<label>       specifies device by partition label
 PARTUUID=<uuid>         specifies device by partition UUID
 <device>                specifies device by path
 <directory>             mountpoint for bind mounts (see --bind/rbind)
 <file>                  regular file for loopdev setup

Operations:
 -B, --bind              mount a subtree somewhere else (same as -o bind)
 -M, --move              move a subtree to some other place
 -R, --rbind             mount a subtree and all submounts somewhere else
 --make-shared           mark a subtree as shared
 --make-slave            mark a subtree as slave
 --make-private          mark a subtree as private
 --make-unbindable       mark a subtree as unbindable
 --make-rshared          recursively mark a whole subtree as shared
 --make-rslave           recursively mark a whole subtree as slave
 --make-rprivate         recursively mark a whole subtree as private
 --make-runbindable      recursively mark a whole subtree as unbindable

For more details see mount(8).
```

When mounting a filesystem to your linux operating system you first need to make ssure that you create a directory to mount to and make sure that the group using the filesystem has permissions to access it:

```bash
# Make a directory with the name directory-name, this could be named anything
sudo mkdir /directory-name

# Create permission entries for a group of users that need read access to this directory
# In this example the group would be group-name, that would be changed to match the target group
sudo chown -R :group-name /directory-name

# Now to give that group write access to the drive if changes need to be made
sudo chmod -R g+w /directory-name

# Now, list the block devices connected to your device to find the drive you are trying to mount
lsblk

# Now mount the drive from the location listed in lsblk to your directory you made earlier
sudo mount /dev/your-drive-id /directory-name
```

> some commands used in this section are documented elsewhere in the wiki. Links below

> you can also learn a lot about these commands by running ```man command-name``` in your linux terminal. Don't forget, this will open a file up in less, which you will just need to press q to exit!
## Supplemental Links
1. [The mount command](../linux-wiki/mount.md)
1. [Various permission commands](../linux-wiki/permissions.md)
1. [The mount command documentation from GNU](https://www.gnu.org/software/coreutils/manual/html_node/chmod-invocation.html#chmod-invocation)
1. [Enumerating devices on your system](../linux-wiki/enumerating-devices.md)

