# Changes since latest release

-   Make subvolumes writable upon deletion

    Deletion fails if a subvolume is readonly. Since we want to delete it
    anyway we can as well set the readonly flag to false.

    Thanks to bar10g <aebirukov@gmail.com> for the patch!

# Changes in 0.2.0

-   Do not create a target directory

    This is to better match the behavior of btrfs-tools as they won't create
    a target directoy either.

# Changes in 0.1.0

Initial release
