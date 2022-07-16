# Troubleshooting

Read this troubleshooting guide before asking in the discord or opening an issue!

## Errors with sunst0rm

### FileExistsError: File Exists: './work/...'
This error happens on some version of sunst0rm, the solution is as simple as removing the ``work`` folder inside your ``sunst0rm`` folder.

You can remove it with Finder or with ``rm -rf ./work``. If it says the resource is busy, you might have ``sunst0rm`` still running or a ramdisk mounted on the system, eject the mounted drive from finder and try to delete again, it should now work.