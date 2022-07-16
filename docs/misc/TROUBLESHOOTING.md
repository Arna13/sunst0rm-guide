# Troubleshooting

Read this troubleshooting guide before asking in the discord or opening an issue!

## Errors restoring with sunst0rm

### FileExistsError: File Exists: './work/...'
This error happens on some version of sunst0rm, the solution is as simple as removing the ``work`` folder inside your ``sunst0rm`` folder.

You can remove it with Finder or with ``rm -rf ./work``. If it says the resource is busy, you might have ``sunst0rm`` still running or a ramdisk mounted on the system, eject the mounted drive from finder and try to delete again, it should now work.

### TypeError: can only concatenate str (not "NoneType") to str
The main reason for this error is typing the boardconfig in caps. You need to type it in lowercase for it to work correctly.
If this issue still happens, try to remove quotes ( '' ) from the command.

### sunstorm.py: error: unrecognized argument: true
Some older versions of sunst0rm required to type ``true`` on its input after some arguments, like ``-r true`` or ``--kpp true``. The use of true after any argument is no longer required and will cause this error. Simply remove ``true`` from your command and you should be fine.

## Errors using the boot.sh script

### Gray display with no verbose after running boot.sh
This usually means you prepared boot incorrectly, and its failing to boot.

Some fixes for this issue could be:
  - Using ``--kpp`` on A9 or lower devices. You need to use this flag in the restore and the boot preparation command, but not in the ``boot.sh``. A10+ devices must not use this.
  - If you have an A10 device, use ``boot-a10.sh`` instead of normal ``boot.sh``