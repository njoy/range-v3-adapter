#  range-v3-adapter
This is Eric Neibler's [ranges](https://github.com/ericniebler/range-v3)---adapted for the NJOY21 build system.

```bash
# This only needs to be done once (per clone)
git remote add ranges https://github.com/ericniebler/range-v3.git

# Do this when you need to update the subtree
git subtree pull --prefix=src ranges master
```

# License
The code contained in this directory is covered by the license contained in the [LICENSE](LICENSE) file. The code in the `src` directory is covered by it's own license which is at the end of the [README file](src/README.md).
