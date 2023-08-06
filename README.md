## Issue

The command `apt-add-repository` does not work correctly when there are no `.list` files on the system. Either `/etc/apt/sources.list` or any `.list` file in `/etc/apt/sources.list.d/` with at least one line in it (this can be a comment) is required for the command to work.

The Debian bookworm docker images (`debian:bookworm` and `debian:bookworm-slim`) ship with no `.list` files. The default repository is configured in `/etc/apt/sources.list.d/debian.sources`. Debian `bullseye` ships with `.list` files and does not have this issue.

This will break some CI pipelines that use the `bookworm` docker images and later use `apt-add-repository`. An example of this is the [LLVM install script](https://apt.llvm.org/#llvmsh).

See `bullseye`, `issue` and `issue-minimal` for examples.

## Workaround

The workaround is to create a `/etc/apt/sources.list` file (even with only 1 comment line) or add a `.list` file to `/etc/apt/sources.list.d/`.

See `workaround-1` and `workaround-2`.

## Fix

A low risk fix is to have add-apt-repository create the `/etc/apt/sources.list` if there are no sources. The `save()` function already does this.

```
--- apt-add-repository-0.99.30-4
+++ apt-add-repository
@@ -36,6 +36,9 @@
         gettext.textdomain("software-properties")
         self.distro = get_distro()
         self.sourceslist = SourcesList()
+        if len(self.sourceslist.list) == 0:
+            self.sourceslist.save()
+            self.sourceslist = SourcesList()
         self.distro.get_sources(self.sourceslist)

     def parse_args(self, args):
```
