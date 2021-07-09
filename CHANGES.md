# Changes since latest release

-   Support excludes for snapshotting

    There might be situations, where one does not want to snapshot a
    complete directory tree. For these cases, we now support excludes with
    the `--exclude` flag. The argument to this flag is interpreted as a Bash
    glob and will be matched against every subvolume that is about to be
    snapshotted. If there is a match, the subvolume in question and every
    subvolume beneath it will not be snapshotted.

    This flag can be used multiple times, every glob will be tried
    individually on each subvolume.

    Note that this flag has no effect in a delete operation and will
    silently be ignored there.

# Changes in 0.3.0

-   Make subvolumes writable upon deletion

    Deletion fails if a subvolume is readonly. Since we want to delete it
    anyway we can as well set the readonly flag to false.

    Thanks to bar10g <aebirukov@gmail.com> for the patch!

-   Check general existence of target

    If it is just checked whether target is a existing directory, then
    snapshotting will fail when there is a regular file or something other
    than a directory.

-   Check in correct path

    Since many filesystems from several sources may be mounted, it is not
    sufficient to check "/", but we have to check the source subvolumes
    path.

-   Replace awk with cut

    With cut, we have more control over subvolumes with spaces or even tabs
    in their names.

-   Use arrays for subvolume lists

    With arrays, we can safely work with subvolumes that have spaces and
    tabs in their names, and correct quoting is provided by Bash.

-   Support confirmation dialog before deleting snapshots

    This patch was started by bar10g <aebirukov@gmail.com>, thank you for
    that!

    However I made a few modifications as to satisfy general workflows:

    -   Simplify confirmation dialog

        In detail:

        -   just accept y/Y, abort otherwise
        -   thus, replace switch-case with simple if-else
        -   assume "no" as default answer
        -   do not ask in a while loop

    -   Replace conditional execution with early return

        Instead of executing the delete command conditionally, do it at the
        end of the method and add a conditional early return statement
        before.

    -   Add flag for interactive deletion

        With an optional -i flag the script will ask for confirmation before
        deleting anything.

    -   Unset ro bit at the end of the method

        This is to optionally cancel the operation with the -i flag.

# Changes in 0.2.0

-   Do not create a target directory

    This is to better match the behavior of btrfs-tools as they won't create
    a target directoy either.

# Changes in 0.1.0

Initial release
