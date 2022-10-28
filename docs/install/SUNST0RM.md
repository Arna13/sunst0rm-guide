# sunst0rm installation

Please make sure to have all dependencies satisfied before the installation part.
If sunst0rm complains about an unsatisfied dependency, please check you have all [dependencies installed](./DEPENDENCIES.md).

If you encounter any problem, please check the [troubleshooting section](../misc/TROUBLESHOOTING.md) before asking for help!

### Getting [sunst0rm](https://github.com/mineek/sunst0rm/)

We will ``git clone`` the ``sunst0rm`` repo and then ``cd`` into it and install the ``pip`` dependencies:
```
git clone https://github.com/mineek/sunst0rm.git
cd sunst0rm
pip3 install -r requirements.txt
```

If the ``pip3`` command fails, you can try running ``python3 -m pip install -r requirements.txt``.

Once all ``pip`` dependencies are satisfied, we can proceed and use ``sunst0rm`` as explained in the [usage guide](../USAGE.md).
